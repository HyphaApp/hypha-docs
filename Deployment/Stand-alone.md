# OTF Application Installation Process

## Standalone Server/VPS

This process was tested on Ubuntu 18.04LTS. It should work on any Debian-based system.


### Get the code

`git clone git@github.com:OpenTechFund/hypha.git [your-site-directory]`


### Basic installation steps.

These are the basic packages needed before you can start the installation process.

- python3-pip and python3-venv - install using  `sudo apt-get install python3-pip python3-venv`
- postgresql (version 11.x or 12.x) use `sudo apt-get install postgresql postgresql-contrib postgresql-server-dev-11`
- to install nodejs (version v12.x), use nodesource. Add the PPA to your sources list by running this script: `curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -` then `sudo apt-get install nodejs`

### Python virtual environment

Create the virtual environment, specify the python binary to use and the directory. Then source the activate script to activate the virtual environment. The last line tells Django what settings to use.

~~~~
$ python3 -m venv venv/hypha
$ source venv/hypha/bin/activate
$ export DJANGO_SETTINGS_MODULE=hypha.settings.production
~~~~

Inside your activated virtual environment you will use plain `python` and `pip` commands. Everything inside the virtual environment is python 3 since we specified that when we created it.

### Install Python packages

Next, install the required packages using:

~~~~
$ pip install -r requirements.txt
~~~~

### Install Node packages

All the needed Node packages are listed in `package.json`. Install them with this command.

~~~~
$ npm install
~~~~

You will also need the gulp task manager. On some systems you might need to run this command with `sudo`.

~~~~
$ npm install -g gulp-cli
~~~~

### The Postgres database

Postgresql is the database used. Start the server you installed above using `sudo service postgresql start`, then log into the postgres superuser, `sudo su - postgres` and enter the postgresql cli with `psql`. In the CLI, use these commands:

- `CREATE DATABASE hypha;`
- `CREATE USER [linux username] WITH SUPERUSER LOGIN;`
- Also, make sure that this user has trust access in pg_hba.conf.

These settings can be restricted later as required.


### Running the app

The application needs a secret key: `export SECRET_KEY='SOME SECRET KEY HERE'`.

To begin with, set the `export SECURE_SSL_REDIRECT=false` to prevent SSL redirect. When you've set up SSL for your server, you can change that setting later.

Then use the following commands to test run the server:

- `gulp deploy`
- `python manage.py collectstatic --noinput`
- `python manage.py createcachetable`
- `python manage.py migrate --noinput`
- `python manage.py clear_cache --cache=default --cache=wagtailcache`
- `python manage.py createsuperuser`
- `python manage.py wagtailsiteupdate server.domain apply.server.domain 80`
- `python manage.py runserver` (runs development server at http://127.0.0.1:8000)

You should see the home page of the server. That's great. You can stop the server, and then we can then take the next steps.


### Deploy with nginx/gunicorn

Make sure gunicorn is installed (it should be). Do a test run with gunicorn: `gunicorn --bind 0.0.0.0:<some port> hypha.wsgi:application` This might not work. It's OK if it doesn't work - you can go on anyway.

To make gunicorn start automatically with systemd see <https://docs.gunicorn.org/en/stable/deploy.html#systemd>.

Set up DNS so that server.domain and apply.server.domain point to the server you've installed the application. Install nginx if you haven't already (`sudo apt-get install nginx`). You'll need to add two new config files for nginx in /etc/nginx/sites-available:

public

```
server {
    listen 80;
    server_name server.domain;

    location ^~/media/(.*)$ {
        alias /path/to/hypha/media/;
    }

    location ^~/static/(.*)$ {
        alias /path/to/hypha/static/;
    }

    location / {
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_pass http://unix:/run/gunicorn.sock;
    }

}
```

apply

```
server {
    listen 80;
    server_name apply.server.domain;

    location ^~/media/(.*)$ {
        alias /path/to/hypha/media/;
    }

    location ^~/static/(.*)$ {
        alias /path/to/hypha/static/;
    }

    location / {
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_pass http://unix:/run/gunicorn.sock;
    }
}
```

Then, symlink these to sites-enabled: `sudo ln -s /etc/nginx/sites-available/public /etc/nginx/sites-enabled && sudo ln -s /etc/nginx/sites-available/apply /etc/nginx/sites-enabled`. Then restart nginx using `sudo systemctl restart nginx`.

**You should then be able to access your application at http://server.domain and http://apply.server.domain.** 

### Adding SSL using a Let's Encrypt certificate.

It's very easy to add SSL via a Let's Encrypt certificate.

See instructions at <https://certbot.eff.org>.

Follow the instructions, and you're done.

### Administration

The Django Administration panel is connected to the 'apply' domain: so access that via http://apply.server.domain/django-admin/ (use the email address and password you set in the `python manage.py createsuperuser` step above.)

The Apply dashboard is here: http://apply.server.domain/dashboard/. The Apply Wagtail admin: http://apply.server.domain/admin

### settings

Here is a list of settings that can be set as environment variables or in a `hypha/settings/local.py` file. 

**None optional:**

```
API_BASE_URL:                                  https://apply.example.org/api
CACHE_CONTROL_MAX_AGE:                         14400
COOKIE_SECURE:                                 true
DJANGO_SETTINGS_MODULE:                        hypha.settings.production
EMAIL_HOST:                                    apply.example.org
ORG_EMAIL:                                     hello@example.org
ORG_GUIDE_URL:                                 https://guide.example.org/
ORG_LONG_NAME:                                 Long name of your organisation
ORG_SHORT_NAME:                                Short org name
PRIMARY_HOST:                                  www.example.org
PROJECTS_AUTO_CREATE:                          false
PROJECTS_ENABLED:                              true
SECRET_KEY:                                    [KEY]
SEND_MESSAGES:                                 true
SERVER_EMAIL:                                  app@apply.example.org
```

**Optional:**

```
ANYMAIL_WEBHOOK_SECRET:                        [KEY]
AWS_ACCESS_KEY_ID:                             [KEY]
AWS_DEFAULT_ACL:                               None
AWS_MIGRATION_ACCESS_KEY_ID:                   [KEY]
AWS_MIGRATION_BUCKET_NAME:                     backup.example.org
AWS_MIGRATION_SECRET_ACCESS_KEY:               [KEY]
AWS_PRIVATE_BUCKET_NAME:                       private.example.org
AWS_PUBLIC_BUCKET_NAME:                        public.example.org
AWS_PUBLIC_CUSTOM_DOMAIN:                      public.example.org
AWS_QUERYSTRING_EXPIRE:                        600
AWS_SECRET_ACCESS_KEY:                         [KEY]
AWS_STORAGE_BUCKET_NAME:                       public.example.org
BASIC_AUTH_ENABLED:                            true
BASIC_AUTH_LOGIN:                              [USER]
BASIC_AUTH_PASSWORD:                           [PASS]
BASIC_AUTH_WHITELISTED_HTTP_HOSTS:             www.example.org,apply.example.org
CLOUDFLARE_API_ZONEID:                         [KEY]
CLOUDFLARE_BEARER_TOKEN:                       [KEY]
MAILCHIMP_API_KEY:                             [KEY]-us10
MAILCHIMP_LIST_ID:                             [ID]
MAILGUN_API_KEY:                               [KEY]
SEND_READY_FOR_REVIEW:                         false
SLACK_DESTINATION_ROOM:                        #notify
SLACK_DESTINATION_ROOM_COMMENTS:               #notes
SLACK_DESTINATION_URL:                         https://slackbot-example.org/incoming/[KEY]
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY:                 [KEY]
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET:              [KEY]
SOCIAL_AUTH_GOOGLE_OAUTH2_WHITELISTED_DOMAINS: example.org
```

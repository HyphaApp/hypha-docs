# base.py

Here are the configuration parameters in base.py. These are largely django and wagtail settings. Those in _italics_ should be kept as they are, unless you have a compelling reason to change them.

_PROJECT\_DIR = os.path.dirname(os.path.dirname(os.path.abspath(**file**)))_ The directory the project is in _BASE\_DIR = os.path.dirname(PROJECT\_DIR)_ The base directory of the project _APP\_NAME = env.get('APP\_NAME', 'hypha')_ The name of the application

DEBUG = False/True : This will display detailed error pages when errors are encountered. Make `True` only in development/testing environments.

_SECRET\_KEY = env\['SECRET\_KEY']_ The secret key should be a large random value, unique to one deployment, and not committed to source control _ALLOWED\_HOSTS = env\['ALLOWED\_HOSTS'].split(',')_ These are the hosts that this django installation is allowed to serve.

## Organisation name and e-mail address, used in e-mail templates etc. These are hypha-specific settings

ORG\_LONG\_NAME = env.get('ORG\_LONG\_NAME', 'Acme Corporation') ORG\_SHORT\_NAME = env.get('ORG\_SHORT\_NAME', 'ACME') ORG\_EMAIL = env.get('ORG\_EMAIL', 'info@example.org') ORG\_GUIDE\_URL = env.get('ORG\_GUIDE\_URL', 'https://guide.example.org/')

## Email settings

_EMAIL\_HOST = env\['EMAIL\_HOST']_ Name of host for emails being sent

_EMAIL\_PORT = int(env\['EMAIL\_PORT'])_ Port used for sending emails _EMAIL\_HOST\_USER = env\['EMAIL\_HOST\_USER']_ Username for sending emails _EMAIL\_HOST\_PASSWORD = env\['EMAIL\_HOST\_PASSWORD']_ Password for sending emails _EMAIL\_USE\_TLS = True_ Use TLS encryption _EMAIL\_USE\_SSL = True_ Use SSL encryption _EMAIL\_SUBJECT\_PREFIX = env\['EMAIL\_SUBJECT\_PREFIX']_ Prefix for all subject lines _SERVER\_EMAIL = DEFAULT\_FROM\_EMAIL = env\['SERVER\_EMAIL']_ Default from address for emails

## Application definition _These are django configurations_

Details on these configurations can be found [here](https://docs.djangoproject.com/en/stable/ref/settings/)

_INSTALLED\_APPS = \[ ... add any additional apps here]_ _MIDDLEWARE = \[... add any additional middleware here]_ _ROOT\_URLCONF = 'hypha.urls'_ _TEMPLATES = \[ ... add any additional templates here]_ _FORM\_RENDERER = 'django.forms.renderers.TemplatesSetting'_ _WSGI\_APPLICATION = 'hypha.wsgi.application'_

## Database

Find documentation on access to databases [here](https://docs.djangoproject.com/en/stable/ref/settings/#databases)

DATABASES = { ... }

## Cache _These settings should be left as they are unless you know to change them._

## Password validation _These settings should be left as they are unless you know to change them._

Information about password validation [here](https://docs.djangoproject.com/en/stable/ref/settings/#auth-password-validators)

## Number of days that password reset and account activation links are valid (default 3).

_PASSWORD\_RESET\_TIMEOUT\_DAYS = 8_

## Internationalization

Info on internationalization [here](https://docs.djangoproject.com/en/stable/topics/i18n/)

LANGUAGE\_CODE = 'en-gb' TIME\_ZONE = 'UTC' USE\_I18N = True USE\_L10N = False USE\_TZ = True DATE\_FORMAT = 'N j, Y' DATETIME\_FORMAT = 'N j, Y, H:i' SHORT\_DATE\_FORMAT = 'Y-m-d' SHORT\_DATETIME\_FORMAT = 'Y-m-d H:i' DATETIME\_INPUT\_FORMATS = \[ ... ]

## Static files (CSS, JavaScript, Images)

Information on static file handling [here](https://docs.djangoproject.com/en/stable/howto/static-files/)

_STATICFILES\_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'_ _STATICFILES\_DIRS = \[]_ _STATIC\_ROOT = env.get('STATIC\_DIR', os.path.join(BASE\_DIR, 'static'))_ _STATIC\_URL = env.get('STATIC\_URL', '/static/')_ _MEDIA\_ROOT = env.get('MEDIA\_DIR', os.path.join(BASE\_DIR, 'media'))_ _MEDIA\_URL = env.get('MEDIA\_URL', '/media/')_

## Users

_AUTH\_USER\_MODEL = 'users.User'_ _WAGTAIL\_USER\_EDIT\_FORM = 'hypha.apply.users.forms.CustomUserEditForm'_ _WAGTAIL\_USER\_CREATION\_FORM = 'hypha.apply.users.forms.CustomUserCreationForm'_ _WAGTAIL\_USER\_CUSTOM\_FIELDS = \['full\_name']_ Custom fields added to wagtail user forms _WAGTAIL\_PASSWORD\_MANAGEMENT\_ENABLED = False_ _WAGTAILUSERS\_PASSWORD\_ENABLED = False_ _WAGTAILUSERS\_PASSWORD\_REQUIRED = False_ _LOGIN\_URL = 'users\_public:login'_ _LOGIN\_REDIRECT\_URL = 'dashboard:dashboard'_ _AUTHENTICATION\_BACKENDS = ( ... add any additional backends here)_

## Logging

_LOGGING = { ... }_

## Wagtail settings

See information on Wagtail settings [here](https://docs.wagtail.io/en/stable/reference/settings.html)

_WAGTAIL\_SITE\_NAME = 'hypha'_ _WAGTAILIMAGES\_IMAGE\_MODEL = 'images.CustomImage'_ _WAGTAILIMAGES\_FEATURE\_DETECTION\_ENABLED = False_ _WAGTAILADMIN\_RICH\_TEXT\_EDITORS = { ... add any additional editors here }_ _WAGTAILEMBEDS\_RESPONSIVE\_HTML = True_ _PASSWORD\_REQUIRED\_TEMPLATE = 'password\_required.html'_ _DEFAULT\_PER\_PAGE = 20_ _ESI\_ENABLED = False_

## Custom hypha settings

_ENABLE\_STYLEGUIDE = False_ _DEBUGTOOLBAR = False_ If the django plug-in `django-debug-toolbar` is enabled ([see dev.py](base.py.md)), `True` would turn it on. Do not do this in production environments.

### Staff e-mail domain _Should probably remain as is_ This setting can come from environment variables, or be specified in an array in this file.

### Social Auth _These settings should probably remain as is_

_SOCIAL\_AUTH\_URL\_NAMESPACE = 'social'_ This is a setting of the plugin [social-auth-app-django](https://python-social-auth.readthedocs.io/en/latest/configuration/django.html)

### Set the Google OAuth2 credentials in ENV variables or local.py

To create or modify Google OAuth2 credentials go [here](https://console.developers.google.com/apis/credentials)

For info on pipelines see [this](http://python-social-auth.readthedocs.io/en/latest/pipeline.html?highlight=pipelines#authentication-pipeline)

_SOCIAL\_AUTH\_PIPELINE = ( ... )_

### Bleach Settings - Settings for the plugin django-bleach _Should remain as is unless you know what to change_

Info on the plugin django-bleach [here](https://django-bleach.readthedocs.io/en/latest/)

### File Field settings

_FILE\_ALLOWED\_EXTENSIONS = \['doc', 'docx', 'odp', 'ods', 'odt', 'pdf', 'ppt', 'pptx', 'rtf', 'txt', 'xls', 'xlsx']_

### Accept attribute in input tag of type file needs filename extensions, starting with a period ('.') character.

_FILE\_ACCEPT\_ATTR\_VALUE = ', '.join(\['.' + ext for ext in FILE\_ALLOWED\_EXTENSIONS])_

### Hijack Settings - These settings are for the plugin django-hijack _Should remain as is_

Documentation on django-hijack, which allows admins to work on behalf of users without their credentials is [here](https://github.com/django-hijack/django-hijack)

_HIJACK\_LOGIN\_REDIRECT\_URL = '/dashboard/'_ _HIJACK\_LOGOUT\_REDIRECT\_URL = '/account/'_ _HIJACK\_DECORATOR = 'hypha.apply.users.decorators.superuser\_decorator'_

### Messaging Settings - these settings are for messaging integration, like Slack. Most should probably be set via environment. _Should remain as is unless you know what to change_

### Celery config - these settings are for python celery _Should remain as is unless you know what to change_

### S3 configuration _Should remain as is unless you know what to change_

### Settings to connect to the Bucket from which we are migrating data

_AWS\_MIGRATION\_BUCKET\_NAME = env.get('AWS\_MIGRATION\_BUCKET\_NAME', '')_ Name of bucket to move data to _AWS\_MIGRATION\_ACCESS\_KEY\_ID = env.get('AWS\_MIGRATION\_ACCESS\_KEY\_ID', '')_ Access key for the S3 user _AWS\_MIGRATION\_SECRET\_ACCESS\_KEY = env.get('AWS\_MIGRATION\_SECRET\_ACCESS\_KEY', '')_ Secret Key for S3 user

### Mailchimp integration

_MAILCHIMP\_API\_KEY = env.get('MAILCHIMP\_API\_KEY')_ _MAILCHIMP\_LIST\_ID = env.get('MAILCHIMP\_LIST\_ID')_

### Basic auth settings _Should remain as is unless you know what to change_

### Security configuration _Should remain as is unless you know what to change_

Information about security configuration [here](https://docs.djangoproject.com/en/stable/ref/middleware/#module-django.middleware.security)

### Referrer-policy header settings _Should remain as is unless you know what to change_

Information about this [here](https://django-referrer-policy.readthedocs.io/en/1.0/)

### Webpack bundle loader _Should remain as is unless you know what to change_

When disabled (set to `False`), all included bundles are silently ignored.

### Django countries package provides ISO 3166-1 countries which does not contain Kosovo. _Should remain as is unless you know what to change_

### Rest Framework configuration _Should remain as is unless you know what to change_

### Projects Feature Flag _Should remain as is unless you know what to change_

### Salesforce integration _Should remain as is unless you know what to change_

### django-file-form settings _Should remain as is unless you know what to change_

### Ensure FILE\_FORM\_UPLOAD\_DIR exists: _Should remain as is unless you know what to change_

### Store temporary files on S3 too (files are still uploaded to local filesystem first) _Should remain as is unless you know what to change_

### Matomo tracking _Should remain as is unless you know what to change_

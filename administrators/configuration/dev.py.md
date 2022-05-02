# dev.py

## Debug settings - gives detailed debug pages when errors happen

DEBUG = True/False (Generally True during development)

**SECURITY WARNING: don't run with debug turned on in production!**

## Secret Key

SECRET\_KEY = 'SOMESECRETKEYHERE'

**SECURITY WARNING: keep the secret key used in production secret!**

WAGTAIL\_CACHE = True/False (Generally False during development)

ALLOWED\_HOSTS = An array with the set of hosts that are allowed by django. Generally: `['apply.localhost', 'localhost', '127.0.0.1', 'hypha.test', 'apply.hypha.test']`

BASE\_URL = URL to reach django app. Generally: `'http://localhost:8000'`

EMAIL\_BACKEND = Backend email service. Generally: `'django.core.mail.backends.console.EmailBackend'`

AUTH\_PASSWORD\_VALIDATORS = The list of validators that are used to check the strength of user’s passwords. Generally: `[]` See [this](https://docs.djangoproject.com/en/3.2/topics/auth/passwords/#password-validation) for more details.

INSTALLED\_APPS = Any additional apps to install for development. Generally: `INSTALLED_APPS + [ 'wagtail.contrib.styleguide', ]`

SECURE\_SSL\_REDIRECT = True/False - Always redirect to SSL. Generally `False` during development.

## E-mail to local files. - Send any emails to local files instead of out

if LOCAL\_FILE\_EMAIL: EMAIL\_BACKEND = 'django.core.mail.backends.filebased.EmailBackend' EMAIL\_FILE\_PATH = BASE\_DIR + '/var/mail'

## Local logging to file. _You can likely leave this as is_

## Debug Toolbar

More info on the Django debug toolbar is [here](https://django-debug-toolbar.readthedocs.io/en/latest/index.html)

## Disable toolbars

We disable all panels by default here since some of them (SQL, Template, Profiling) can be very CPU intensive for this site. However disabled panels can be easily toggled on in the UI.

## Testing the apis from postman - _leave as is unless you have a compelling reason not to._

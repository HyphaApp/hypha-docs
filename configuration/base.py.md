# base.py configuration parameters

Here are the configuration parameters in base.py. These are largely django and wagtail settings. Those in *italics* should be kept as they are, unless you have a compelling reason to change them.

*PROJECT_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))* The directory the project is in
*BASE_DIR = os.path.dirname(PROJECT_DIR)* The base directory of the project
*APP_NAME = env.get('APP_NAME', 'hypha')* The name of the application

DEBUG = False/True : This will display detailed error pages when errors are encountered. Make `True` only in development/testing environments.

*SECRET_KEY = env['SECRET_KEY']* The secret key should be a large random value, unique to one deployment, and not committed to source control
*ALLOWED_HOSTS = env['ALLOWED_HOSTS'].split(',')* These are the hosts that this django installation is allowed to serve.

## Organisation name and e-mail address, used in e-mail templates etc. These are hypha-specific settings

ORG_LONG_NAME = env.get('ORG_LONG_NAME', 'Acme Corporation')
ORG_SHORT_NAME = env.get('ORG_SHORT_NAME', 'ACME')
ORG_EMAIL = env.get('ORG_EMAIL', 'info@example.org')
ORG_GUIDE_URL = env.get('ORG_GUIDE_URL', 'https://guide.example.org/')

## Email settings
*EMAIL_HOST = env['EMAIL_HOST']* Name of host for emails being sent

*EMAIL_PORT = int(env['EMAIL_PORT'])* Port used for sending emails
*EMAIL_HOST_USER = env['EMAIL_HOST_USER']* Username for sending emails
*EMAIL_HOST_PASSWORD = env['EMAIL_HOST_PASSWORD']* Password for sending emails
*EMAIL_USE_TLS = True* Use TLS encryption
*EMAIL_USE_SSL = True* Use SSL encryption
*EMAIL_SUBJECT_PREFIX = env['EMAIL_SUBJECT_PREFIX']* Prefix for all subject lines
*SERVER_EMAIL = DEFAULT_FROM_EMAIL = env['SERVER_EMAIL']* Default from address for emails

## Application definition *These are django configurations*

Details on these configurations can be found [here](https://docs.djangoproject.com/en/stable/ref/settings/)

*INSTALLED_APPS = [ ... add any additional apps here]*
*MIDDLEWARE = [... add any additional middleware here]*
*ROOT_URLCONF = 'hypha.urls'*
*TEMPLATES = [ ... add any additional templates here]*
*FORM_RENDERER = 'django.forms.renderers.TemplatesSetting'*
*WSGI_APPLICATION = 'hypha.wsgi.application'*

## Database
Find documentation on access to databases [here](https://docs.djangoproject.com/en/stable/ref/settings/#databases)

DATABASES = { ... }

## Cache *These settings should be left as they are unless you know to change them.*

## Password validation *These settings should be left as they are unless you know to change them.*

Information about password validation [here](https://docs.djangoproject.com/en/stable/ref/settings/#auth-password-validators)


## Number of days that password reset and account activation links are valid (default 3).
*PASSWORD_RESET_TIMEOUT_DAYS = 8*

## Internationalization

Info on internationalization [here](https://docs.djangoproject.com/en/stable/topics/i18n/)

LANGUAGE_CODE = 'en-gb'
TIME_ZONE = 'UTC'
USE_I18N = True
USE_L10N = False
USE_TZ = True
DATE_FORMAT = 'N j, Y'
DATETIME_FORMAT = 'N j, Y, H:i'
SHORT_DATE_FORMAT = 'Y-m-d'
SHORT_DATETIME_FORMAT = 'Y-m-d H:i'
DATETIME_INPUT_FORMATS = [ ... ]

## Static files (CSS, JavaScript, Images)

Information on static file handling [here](https://docs.djangoproject.com/en/stable/howto/static-files/)

*STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'*
*STATICFILES_DIRS = []*
*STATIC_ROOT = env.get('STATIC_DIR', os.path.join(BASE_DIR, 'static'))*
*STATIC_URL = env.get('STATIC_URL', '/static/')*
*MEDIA_ROOT = env.get('MEDIA_DIR', os.path.join(BASE_DIR, 'media'))*
*MEDIA_URL = env.get('MEDIA_URL', '/media/')*

## Users

*AUTH_USER_MODEL = 'users.User'*
*WAGTAIL_USER_EDIT_FORM = 'hypha.apply.users.forms.CustomUserEditForm'*
*WAGTAIL_USER_CREATION_FORM = 'hypha.apply.users.forms.CustomUserCreationForm'*
*WAGTAIL_USER_CUSTOM_FIELDS = ['full_name']* Custom fields added to wagtail user forms
*WAGTAIL_PASSWORD_MANAGEMENT_ENABLED = False*
*WAGTAILUSERS_PASSWORD_ENABLED = False*
*WAGTAILUSERS_PASSWORD_REQUIRED = False*
*LOGIN_URL = 'users_public:login'*
*LOGIN_REDIRECT_URL = 'dashboard:dashboard'*
*AUTHENTICATION_BACKENDS = ( ...  add any additional backends here)*

## Logging
*LOGGING = { ... }*



## Wagtail settings

See information on Wagtail settings [here](https://docs.wagtail.io/en/stable/reference/settings.html)

*WAGTAIL_SITE_NAME = 'hypha'*
*WAGTAILIMAGES_IMAGE_MODEL = 'images.CustomImage'*
*WAGTAILIMAGES_FEATURE_DETECTION_ENABLED = False*
*WAGTAILADMIN_RICH_TEXT_EDITORS = { ... add any additional editors here }*
*WAGTAILEMBEDS_RESPONSIVE_HTML = True*
*PASSWORD_REQUIRED_TEMPLATE = 'password_required.html'*
*DEFAULT_PER_PAGE = 20*
*ESI_ENABLED = False*



## Custom hypha settings

*ENABLE_STYLEGUIDE = False*
*DEBUGTOOLBAR = False* If the django plug-in `django-debug-toolbar` is enabled ([see dev.py]()), `True` would turn it on. Do not do this in production environments.

### Staff e-mail domain *Should probably remain as is*  This setting can come from environment variables, or be specified in an array in this file. 

### Social Auth *These settings should probably remain as is*
*SOCIAL_AUTH_URL_NAMESPACE = 'social'* This is a setting of the plugin [social-auth-app-django](https://python-social-auth.readthedocs.io/en/latest/configuration/django.html)

### Set the Google OAuth2 credentials in ENV variables or local.py

To create or modify Google OAuth2 credentials go [here](https://console.developers.google.com/apis/credentials)

For info on pipelines  see [this](http://python-social-auth.readthedocs.io/en/latest/pipeline.html?highlight=pipelines#authentication-pipeline)

*SOCIAL_AUTH_PIPELINE = ( ... )*

### Bleach Settings - Settings for the plugin django-bleach *Should remain as is unless you know what to change*

Info on the plugin django-bleach [here](https://django-bleach.readthedocs.io/en/latest/)

### File Field settings
*FILE_ALLOWED_EXTENSIONS = ['doc', 'docx', 'odp', 'ods', 'odt', 'pdf', 'ppt', 'pptx', 'rtf', 'txt', 'xls', 'xlsx']*

### Accept attribute in input tag of type file needs filename extensions, starting with a period ('.') character.
*FILE_ACCEPT_ATTR_VALUE = ', '.join(['.' + ext for ext in FILE_ALLOWED_EXTENSIONS])*

### Hijack Settings - These settings are for the plugin django-hijack *Should remain as is*

Documentation on django-hijack, which allows admins to work on behalf of users without their credentials is [here](https://github.com/django-hijack/django-hijack)

*HIJACK_LOGIN_REDIRECT_URL = '/dashboard/'*
*HIJACK_LOGOUT_REDIRECT_URL = '/account/'*
*HIJACK_DECORATOR = 'hypha.apply.users.decorators.superuser_decorator'*

### Messaging Settings - these settings are for messaging integration, like Slack. Most should probably be set via environment. *Should remain as is unless you know what to change*

### Celery config - these settings are for python celery *Should remain as is unless you know what to change*

### S3 configuration *Should remain as is unless you know what to change*

### Settings to connect to the Bucket from which we are migrating data
*AWS_MIGRATION_BUCKET_NAME = env.get('AWS_MIGRATION_BUCKET_NAME', '')* Name of bucket to move data to
*AWS_MIGRATION_ACCESS_KEY_ID = env.get('AWS_MIGRATION_ACCESS_KEY_ID', '')* Access key for the S3 user
*AWS_MIGRATION_SECRET_ACCESS_KEY = env.get('AWS_MIGRATION_SECRET_ACCESS_KEY', '')* Secret Key for S3 user

### Mailchimp integration
*MAILCHIMP_API_KEY = env.get('MAILCHIMP_API_KEY')*
*MAILCHIMP_LIST_ID = env.get('MAILCHIMP_LIST_ID')*

### Basic auth settings *Should remain as is unless you know what to change*


### Security configuration *Should remain as is unless you know what to change*

Information about security configuration [here](https://docs.djangoproject.com/en/stable/ref/middleware/#module-django.middleware.security)


### Referrer-policy header settings *Should remain as is unless you know what to change*

Information about this [here](https://django-referrer-policy.readthedocs.io/en/1.0/)


### Webpack bundle loader *Should remain as is unless you know what to change*

When disabled (set to `False`), all included bundles are silently ignored.

###  Django countries package provides ISO 3166-1 countries which does not contain Kosovo. *Should remain as is unless you know what to change*

### Rest Framework configuration *Should remain as is unless you know what to change*

### Projects Feature Flag *Should remain as is unless you know what to change*

### Salesforce integration *Should remain as is unless you know what to change*

### django-file-form settings *Should remain as is unless you know what to change*

### Ensure FILE_FORM_UPLOAD_DIR exists: *Should remain as is unless you know what to change*

### Store temporary files on S3 too (files are still uploaded to local filesystem first) *Should remain as is unless you know what to change*

### Matomo tracking *Should remain as is unless you know what to change*


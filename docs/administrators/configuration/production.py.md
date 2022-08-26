# production.py configuration settings

## Disable debug mode
DEBUG = False - In production, this should always be `False`

## Configuration from environment variables

`env = os.environ.copy()` This line copies any configuration from environment variables

Alternatively, you can set these in a local.py file on the server with:
```
try:
     from .local import *  # noqa
except ImportError:
    pass
```

## Mailgun configuration.

Configuration for Mailgun. Mailgun API reference is [here](https://documentation.mailgun.com/en/latest/api_reference.html#api-reference)

## Sentry configuration.

If you are using Sentry. Details on Sentry DSN [here](https://docs.sentry.io/product/sentry-basics/dsn-explainer/?utm_source=google&utm_medium=cpc&utm_campaign=11194763167&utm_content=g&utm_term=&gclid=CjwKCAjw-sqKBhBjEiwAVaQ9a8AQ__8o2-dBNVbNF9Mqj5GPgQVWAjBc4L1FTVdxSl5dtcNATilwPxoCkCgQAvD_BwE)


## Heroku configuration.

Set ON_HEROKU to `true` in Config Vars or via Heroku cli`'heroku config:set ON_HEROKU=true`.

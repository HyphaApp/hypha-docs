# production.py

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

Configuration for Mailgun. Mailgun API reference is [here](https://documentation.mailgun.com/en/latest/api\_reference.html#api-reference)

## Sentry configuration.

If you are using Sentry. Details on Sentry DSN [here](https://docs.sentry.io/product/sentry-basics/dsn-explainer/?gclid=CjwKCAjw-sqKBhBjEiwAVaQ9a8AQ\_\_8o2-dBNVbNF9Mqj5GPgQVWAjBc4L1FTVdxSl5dtcNATilwPxoCkCgQAvD\_BwE)

## Heroku configuration.

Set ON\_HEROKU to `true` in Config Vars or via Heroku cli`'heroku config:set ON_HEROKU=true`.

# example.py

These settings aren't at this time loaded anywhere. But at some point, they could be included with an include statement in a different settings file (like test.py or production.py), in the same way as local.py is included:

```
try:
     from .example import *  # noqa
except ImportError:
    pass
```

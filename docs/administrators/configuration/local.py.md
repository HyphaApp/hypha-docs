# local.py configuration settings

The settings in this file is included in other files with the following code:

```
try:
     from .local import *  # noqa
except ImportError:
    pass
```
Copy `local.py.example` to `local.py` and uncomment whatever settings you want to include in your Django install.

# Hypha/Django/Wagtail Configuration options

Under hypha/settings/ there are several python configuration files:

* [base.py](base.py.md) – Base settings file. Other settings file start by loading this in.
* [dev.py](dev.py.md) – This is settings for development work.
* [example.py](example.py.md) – Example settings, not loaded anywhere. (This file should be expanded to cover more settings.)
* [local.py.example](example.py.md) – Copy and rename to "local.py" and it will be loaded by both production and dev settings. Main use is to allow developers an easy way to set and test settings. Can also be used in production but environment variables are the preferred and more secure way.
* [production.py](production.py.md) – This is settings for production use.
* [test.py](test.py.md) – This is the settings file for running tests.

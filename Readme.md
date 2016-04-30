# Heroku Buildpack: Python + NLTK
![python](https://cloud.githubusercontent.com/assets/51578/13712821/b68a42ce-e793-11e5-96b0-d8eb978137ba.png)

This buildpack is identical to the official [python](https://github.com/heroku/heroku-buildpack-python), but also installs any NLTK corpora/packages desired. Desired packages should be defined in `.nltk_packages` in the root of the repo. Packages will only be downloaded if both this file exists and `nltk` is installed among your dependencies.

The `.nltk_packages` file can contain either space-separated packages, or one package on each line.

See it in Action
----------------

Deploying a Python application couldn't be easier:

    $ echo "punkt brown" > .nltk_packages
    $ ls -a
    .nltk_packages Procfile  requirements.txt  web.py

    $ heroku create --buildpack https://github.com/megacool/heroku-buildpack-python-nltk

    $ git push heroku master
    ...
    -----> Python app detected
         $ pip install -r requirements.txt
    -----> Downloading NLTK packages punkt brown
    [nltk_data] Downloading package punkt to /app/nltk_data...
    [nltk_data]   Unzipping tokenizers/punkt.zip.
    [nltk_data] Downloading package brown to
    [nltk_data]     /app/nltk_data...
    [nltk_data]   Unzipping taggers/brown.zip.
    -----> Discovering process types
           Procfile declares types -> (none)

A `requirements.txt` file must be present at the root of your application's repository.

You can also specify the latest production release of this buildpack for upcoming builds of an existing application:

    $ heroku buildpacks:set https://github.com/megacool/heroku-buildpack-python-nltk


Specify a Python Runtime
------------------------

Specific versions of the Python runtime can be specified with a `runtime.txt` file:

    $ cat runtime.txt
    python-3.5.1

Runtime options include:

- `python-2.7.11`
- `python-3.5.1`
- `pypy-5.0.1` (unsupported, experimental)

Other [unsupported runtimes](https://github.com/heroku/heroku-buildpack-python/tree/master/builds/runtimes) are available as well. Use at your own risk. 

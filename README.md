# Django project template

This is a simple Django 2.0+ project template with my preferred setup. Most Django project templates make way too many assumptions or are just way too complicated. I try to make the least amount of assumptions possible while still trying provide a useful setup. Most of my projects are deployed to Heroku, so this is optimized for that but is not necessary.

> Forked from [skorokithakis/django-project-template](https://github.com/skorokithakis/django-project-template)

## Features

- Latest Django (hopefully).
- Uses [Pipenv](https://github.com/kennethreitz/pipenv) - the best packaging tool.
- [django-extensions](http://django-extensions.readthedocs.org) for the various useful commands and things.
- [ShortUUID](https://github.com/skorokithakis/shortuuid), because I end up using it most of the time.
- Secure by default (various things won't work on production without TLS).
- Runs under docker-compose by default, with a PostgreSQL and Redis instance (configured as a cache and session
  backend).
- Can also run outside of docker-compose using SQLite, for when you aren't using Postgres-specific features yet.
- Other things I'm forgetting now.


## Installation

Installing the template is easy, you don't really have to do much:

```bash
django-admin.py startproject \
  --template=https://github.com/thanpolas/django-project-template/archive/master.zip \
  --extension py,cfg,yml,ini \
  project_name
```

That's it! You're ready to run the project with `docker-compose` and add that "container expert" bullet point to your CV:

```bash
$ docker-compose up
```

You should be able to access your project under [http://localhost/](http://localhost/). I like it running on port 80, and you can assign a different hostname in your `/etc/hosts` if you want it to look a bit better.

If you don't want to bother with `docker-compose` yet, you can run it locally:

```bash
$ pipenv install --dev
$ ./manage.py migrate
$ ./manage.py runserver_plus
```

Then you can access your project at [http://localhost:8080/](http://localhost:8080/).


## Dokku deployment

The template comes with most of the things you need to deploy it on Dokku. You will need to set up a Postgres database,
a Redis instance and a TLS certificate first, though. For instructions, see my post on [deploying Django projects on
Dokku](https://www.stavros.io/posts/deploy-django-dokku/).


## Production deployment tips

You're going to need to add some secrets for production. That's fine, as long as you don't commit them in any repo. The project is structured such that all secrets can be passed as environment variables (see the settings file for the variable names).

You can also specify any secret keys or settings in a `local_settings.py`, which will override your `settings.py`
variables. I usually use that for local development.

## License

* Copyright © Thanasis Polychronakis, Stavros Korokithakis. Licensed under the [MIT license](https://opensource.org/licenses/MIT).

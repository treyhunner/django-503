Django 503
==========

An app to show 503 error page, while your django site is on maintenance.

Sometimes you just need to temporarily stop your site to do some maintenance,
maybe to run migrations, update packages, or something like that. Quick and easy solution is to set up
a 503 error page for all requests. It should show human-friendly text for your site visitors,
saying that site will be back online very soon, while you're working on it at the moment.
After maintenance is over you can promptly turn 503 error page off.

``503 Service Unavailable`` is a valid http response:

    The server is currently unable to handle the request due to a temporary overloading or maintenance of the server.
    The implication is that this is a temporary condition which will be alleviated after some delay.

It works well with search engine crawlers, your page index will stay intact if your maintenance doesn't last far too long.

Installation
------------

Django-503 works with python>=2.5 and django>=1.2
Recommended way to install is pip::

  pip install django-503


* Add ``django_503`` to ``INSTALLED_APPS`` in settings.py::

    INSTALLED_APPS = (...
                      'django_503',
                      ...
                     )

* Add ``'django_503.middleware.MaintenanceMiddleware'`` to your ``MIDDLEWARE_CLASSES``
after session and auth middlewares like this::

    MIDDLEWARE_CLASSES = (
        ...
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        ...
        'django_503.middleware.MaintenanceMiddleware',
    )

* Run ``python manage.py syncdb``

* Make sure you use ``admin.autodiscover()`` to enable project ``admin.py``.

Usage
-----

You can turn on maintenance mode by changing app config via django admin interface.
It's located at url ``/admin/django_503/config/`` relative your site URL .
Setting `mainteneance` to True will turn 503 error page for regular users.
Admins will see a warning on top of every html page, stating site is on maintenance now,
so that they can still access site and not forget to switch 503 mode off.


Template overriding
~~~~~~~~~~~~~~~~~~~
* To change 503 error page looks you should override ``503.html`` template.
* To change admin warning message you should override ``admin_warning.html`` template.

Tests
-----

To run app testsuite use::

  python setup.py test django-503
  

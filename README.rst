=================
Scrapy-UserAgents
=================

.. image:: https://img.shields.io/pypi/v/scrapy-useragents.svg
   :target: https://pypi.python.org/pypi/scrapy-useragents
   :alt: PyPI Version

.. image:: https://img.shields.io/travis/grammy-jiang/scrapy-useragents/master.svg
   :target: http://travis-ci.org/grammy-jiang/scrapy-useragents
   :alt: Build Status

.. image:: https://img.shields.io/badge/wheel-yes-brightgreen.svg
   :target: https://pypi.python.org/pypi/scrapy-useragents
   :alt: Wheel Status

.. image:: https://img.shields.io/codecov/c/github/grammy-jiang/scrapy-useragents/master.svg
   :target: http://codecov.io/github/grammy-jiang/scrapy-useragents?branch=master
   :alt: Coverage report

.. .. image:: https://img.shields.io/github/downloads/grammy-jiang/scrapy-useragents/total.svg
   :target: https://github.com/grammy-jiang/scrapy-useragents
   :alt: Downloads

.. image:: https://img.shields.io/pypi/dm/scrapy-useragents.svg
   :target: https://github.com/grammy-jiang/scrapy-useragents
   :alt: Downloads

Overview
========

Scrapy is a great framework for web crawling. This downloader middleware
provides a user-agent rotation based on the settings in settings.py, spider,
request.

Requirements
============

* Tests on Python 2.7 and Python 3.5, but it should work on other version higher
  then Python 3.3

* Tests on Linux, but it's a pure python module, it should work on other
  platforms with official python supported, e.g. Windows, Mac OSX, BSD

Installation
============

The quick way::

    pip install scrapy-useragents

Or put this middleware just beside the scrapy project.

Documentation
=============

In setting.py, for example::

    # -----------------------------------------------------------------------------
    # USER AGENT
    # -----------------------------------------------------------------------------

    DOWNLOADER_MIDDLEWARES.update({
        'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
        'scrapy_useragents.downloadermiddlewares.useragents.UserAgentsMiddleware': 500,
    })

    USER_AGENTS = [
        ('Mozilla/5.0 (X11; Linux x86_64) '
         'AppleWebKit/537.36 (KHTML, like Gecko) '
         'Chrome/57.0.2987.110 '
         'Safari/537.36'),  # chrome
        ('Mozilla/5.0 (X11; Linux x86_64) '
         'AppleWebKit/537.36 (KHTML, like Gecko) '
         'Chrome/61.0.3163.79 '
         'Safari/537.36'),  # chrome
        ('Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:55.0) '
         'Gecko/20100101 '
         'Firefox/55.0'),  # firefox
        ('Mozilla/5.0 (X11; Linux x86_64) '
         'AppleWebKit/537.36 (KHTML, like Gecko) '
         'Chrome/61.0.3163.91 '
         'Safari/537.36'),  # chrome
        ('Mozilla/5.0 (X11; Linux x86_64) '
         'AppleWebKit/537.36 (KHTML, like Gecko) '
         'Chrome/62.0.3202.89 '
         'Safari/537.36'),  # chrome
        ('Mozilla/5.0 (X11; Linux x86_64) '
         'AppleWebKit/537.36 (KHTML, like Gecko) '
         'Chrome/63.0.3239.108 '
         'Safari/537.36'),  # chrome
    ]

Settings Reference
------------------

USER_AGENTS
~~~~~~~~~~~

A list of User-Agent to use when crawling, unless overridden (Yes, headers still
can be specified in Spider or Request, but in spider the attribute name changes
from useragent to useragents, while Request still remain the same).

The middleware will rotate this list by function cycle from the module
itertools.

**Be careful this middleware can't handle the situation that the
COOKIES_ENABLED is True, and the website binds the cookies with
User-Agent, it may cause unpredictable result of the spider. This problem will
be solved in the future.**

TODO
====

* Read User-Agent from a backend, e.g. MongoDB, MySQL, or even a file saved on
  the local disk.

* Rotate User-Agent binding with cookies, keep the consistence

* Add meta key for User-Agent selection based on each request

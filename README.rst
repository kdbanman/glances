===============================
Glances - An eye on your system
===============================


.. image:: https://img.shields.io/pypi/v/glances.svg
    :target: https://pypi.python.org/pypi/Glances
.. image:: https://img.shields.io/github/stars/nicolargo/glances.svg
    :target: https://github.com/nicolargo/glances/
    :alt: Github stars
.. image:: https://travis-ci.org/nicolargo/glances.svg?branch=master
    :target: https://travis-ci.org/nicolargo/glances
.. image:: https://circleci.com/gh/nicolargo/glances/tree/develop.svg?style=svg
    :target: https://circleci.com/gh/nicolargo/glances/tree/develop
.. image:: https://img.shields.io/scrutinizer/g/nicolargo/glances.svg
    :target: https://scrutinizer-ci.com/g/nicolargo/glances/
.. image:: https://api.flattr.com/button/flattr-badge-large.png
    :target: https://flattr.com/thing/484466/nicolargoglances-on-GitHub

Follow Glances on Twitter: `@nicolargo`_ or `@glances_system`_

**Glances** is a cross-platform curses-based system monitoring tool
written in Python.

.. image:: https://raw.githubusercontent.com/nicolargo/glances/develop/docs/_static/screencast.gif

Requirements
============

- ``python 2.7,>=3.3`` (tested with version 2.7, 3.3, 3.4, 3.5)
- ``psutil>=2.0.0``
- ``setuptools``

Optional dependencies:

- ``bottle`` (for Web server mode)
- ``py3sensors`` (for hardware monitoring support) [Linux-only]
- ``hddtemp`` (for HDD temperature monitoring support) [Linux-only]
- ``batinfo`` (for battery monitoring support) [Linux-only]
- ``pymdstat`` (for RAID support) [Linux-only]
- ``pysnmp`` (for SNMP support)
- ``zeroconf`` (for the autodiscover mode)
- ``netifaces`` (for the IP plugin)
- ``influxdb`` (for the InfluxDB export module)
- ``statsd`` (for the StatsD export module)
- ``pystache`` (for the action script feature)
- ``docker-py`` (for the Docker monitoring support) [Linux-only]
- ``matplotlib`` (for graphical/chart support)
- ``pika`` (for the RabbitMQ/ActiveMQ export module)
- ``bernhard`` (for the Riemann export module)
- ``py-cpuinfo`` (for the Quicklook CPU info module)
- ``scandir`` (for the Folders plugin) [Only for Python < 3.5]

*Note for Python 2.6 users*

Since version 2.7, Glances no longer support Python 2.6. Please upgrade
to at least Python 2.7/3.3+ or downgrade to Glances 2.6.2 (latest version
with Python 2.6 support).

*Note for CentOS Linux 6 and 7 users*

Python 2.7, 3.3 and 3.4 are now available via SCLs. See:
https://lists.centos.org/pipermail/centos-announce/2015-December/021555.html.

Installation
============

Several method to test/install Glances on your system. Choose your weapon !

Glances Auto Install script: the total way
------------------------------------------

To install both dependencies and latest Glances production ready version
(aka *master* branch), just enter the following command line:

.. code-block:: console

    curl -L https://bit.ly/glances | /bin/bash

or

.. code-block:: console

    wget -O- https://bit.ly/glances | /bin/bash

*Note*: Only supported on some GNU/Linux distributions. If you want to
support other distributions, please contribute to `glancesautoinstall`_.

PyPI: The simple way
--------------------

Glances is on ``PyPI``. By using PyPI, you are sure to have the latest
stable version.

To install, simply use ``pip``:

.. code-block:: console

    pip install glances

*Note*: Python headers are required to install `psutil`_. For example,
on Debian/Ubuntu you need to install first the *python-dev* package.
For Fedora/CentOS/RHEL install first *python-devel* package. For Windows,
just install PsUtil from the binary installation file.

You can also install the following libraries in order to use optional
features (like the Web interface, exports modules, sensors...):

.. code-block:: console

    pip install bottle requests batinfo https://bitbucket.org/gleb_zhulik/py3sensors/get/tip.tar.gz zeroconf netifaces pymdstat influxdb elasticsearch potsdb statsd pystache docker-py pysnmp pika py-cpuinfo bernhard cassandra scandir

To upgrade Glances to the latest version:

.. code-block:: console

    pip install --upgrade glances

If you need to install Glances in a specific user location, use:

.. code-block:: console

    export PYTHONUSERBASE=~/mylocalpath
    pip install --user glances

Docker: the funny way
---------------------

A Glances container is available. It will include the latest development HEAD version. You can use it to monitor your server and all your others containers !

Get the Glances container:

.. code-block:: console

    docker pull nicolargo/glances

Run the container in console mode:

.. code-block:: console

    docker run -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host -it docker.io/nicolargo/glances

Run the container in Web server mode (notice the GLANCES_OPT environment variable setting parameters for the glances startup command) :

.. code-block:: console

    docker run -d -p 61208:61208 -e GLANCES_OPT="-w" -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host docker.io/nicolargo/glances

Additionally, If you want to use your own glances.conf file, you can create your
own Dockerfile:

.. code-block:: console

    FROM nicolargo/glances
    COPY glances.conf /glances/conf/glances.conf
    CMD python -m glances -C /glances/conf/glances.conf $GLANCES_OPT

Alternatively, you can specify something along the same lines with docker run options:

.. code-block:: console

    docker run -v ./glances.conf:/glances/conf/glances.conf -v /var/run/docker.sock:/var/run/docker.sock:ro --pid host -it docker.io/nicolargo/glances

Where ./glances.conf is a local directory containing your glances.conf file.

GNU/Linux
---------

At the moment, packages exist for the following GNU/Linux distributions:

- Arch Linux
- Debian
- Fedora/CentOS/RHEL
- Gentoo
- Slackware (SlackBuild)
- Ubuntu
- Void Linux

So you should be able to install it using your favorite package manager.
Be aware that the Glances version can not be the latest one using this method.

FreeBSD
-------

To install the binary package:

.. code-block:: console

    # pkg install py27-glances

To install Glances from ports:

.. code-block:: console

    # cd /usr/ports/sysutils/py-glances/
    # make install clean

OS X
----

OS X users can install Glances using ``Homebrew`` or ``MacPorts``.

Homebrew
````````

.. code-block:: console

    $ brew install python
    $ pip install glances

MacPorts
````````

.. code-block:: console

    $ sudo port install glances

Windows
-------

Install `Python`_ for Windows (Python 2.7.9+ and 3.4+ ship with pip) and
then just:

.. code-block:: console

    $ pip install glances

You can also install the following libraries in order to use optional
features (like the Web interface, exports modules, sensors...):

.. code-block:: console

    pip install bottle requests zeroconf netifaces influxdb elasticsearch potsdb statsd pystache pysnmp pika py-cpuinfo bernhard cassandra scandir

Source
------

To install Glances from source:

.. code-block:: console

    $ wget https://github.com/nicolargo/glances/archive/vX.Y.tar.gz -O - | tar xz
    $ cd glances-*
    # python setup.py install

*Note*: Python headers are required to install psutil. For example,
on Debian/Ubuntu you need to install first the *python-dev* package.

Chef
----

An awesome ``Chef`` cookbook is available to monitor your infrastructure: https://supermarket.chef.io/cookbooks/glances (thanks to Antoine Rouyer)

Puppet
------

You can install Glances using ``Puppet``: https://github.com/rverchere/puppet-glances

Usage
=====

For the standalone mode, just run:

.. code-block:: console

    $ glances

For the Web server mode, run:

.. code-block:: console

    $ glances -w

and enter the URL ``http://<ip>:61208`` in your favorite web browser.

For the client/server mode, run:

.. code-block:: console

    $ glances -s

on the server side and run:

.. code-block:: console

    $ glances -c <ip>

on the client one.

You can also detect and display all Glances servers available on your
network or defined in the configuration file:

.. code-block:: console

    $ glances --browser

and RTFM, always.

Documentation
=============

For complete documentation have a look at the readthedocs_ website.

If you have any question (after RTFM!), please post it on the official Q&A `forum`_.

Gateway to other services
=========================

Glances can export stats to: ``CSV`` file, ``InfluxDB``, ``Cassandra``,
``OpenTSDB``, ``StatsD``, ``ElasticSearch``, ``RabbitMQ`` and  ``Riemann`` server.

How to contribute ?
===================

If you want to contribute to the Glances project, read this `wiki`_ page.

There is also a chat dedicated to the Glances developers:

.. image:: https://badges.gitter.im/Join%20Chat.svg
        :target: https://gitter.im/nicolargo/glances?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge

Author
======

Nicolas Hennion (@nicolargo) <nicolas@nicolargo.com>

License
=======

LGPL. See ``COPYING`` for more details.

.. _psutil: https://github.com/giampaolo/psutil
.. _glancesautoinstall: https://github.com/nicolargo/glancesautoinstall
.. _@nicolargo: https://twitter.com/nicolargo
.. _@glances_system: https://twitter.com/glances_system
.. _Python: https://www.python.org/getit/
.. _readthedocs: https://glances.readthedocs.io/
.. _forum: https://groups.google.com/forum/?hl=en#!forum/glances-users
.. _wiki: https://github.com/nicolargo/glances/wiki/How-to-contribute-to-Glances-%3F

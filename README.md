[![Build Status](https://travis-ci.org/douban/code.png?branch=master)](https://travis-ci.org/douban/code)

Douban CODE
===========

* Website: <http://douban-code.github.io>
* Guide: <http://douban-code.github.io/pages/getting-started.html>

Dependency
----------
- libmc <https://github.com/douban/libmc>
- Python 2.7+
- pip >= 1.4.1

Docker Installation
-------------------

You can use [code](https://registry.hub.docker.com/u/dongweiming/code/)

```
$docker pull dongweiming/code
```

or just build locally(recommended):

```
$cd code
$docker build -t code .
```

And launch a bash shell inside the container:

```
$docker run -d -p 8080:8000 code gunicorn -w 2 -b 0.0.0.0:8000 app:app  # start app
5cf0d1f6a421c53d54662df77dd142978d24b8c76fd72ce1c106506458e1304a
$boot2docker ip
192.168.59.103
# go web http://192.168.59.103:8080
$docker run -t -i code /bin/bash
```

Vagrant Installation(Recommended)
--------------------

```
$cd code
$vagrant up
$vagrant ssh
# In ubuntu. we use `supervisor` monitor and control CODE and other services.
#You just go web http://localhost:8200
```

Quick Installation
------------------
Currently supports the following systems:

* gentoo
* ubuntu/debian
* centos/redhat/fedora
* opensuse
* archlinux

You only to execute:

```
$bash <(curl -s https://raw.githubusercontent.com/douban/code/master/scripts/install_code.sh)
```

Then install & run `supervisor` to monitor and control all services of code.

```
pip install supervisor
sudo wget -O /etc/init.d/supervisor https://raw.githubusercontent.com/Supervisor/initscripts/master/ubuntu
sudo chmod +x /etc/init.d/supervisor
sudo cp scripts/supervisord.conf /etc/supervisord.conf
sudo cp scripts/code.conf /etc/supervisor/conf.d/code.conf
sudo /etc/init.d/supervisor start
# go web http://localhost:8200
```

Notes: The install script in `scripts` subdirectory, for example ubuntu/debian,
You can see `scripts/ubuntu.sh`

FAQ
----

1. single http daemon
 - `gunicorn -b 127.0.0.1:8001 app:app` # git http daemon

2. vilya.config.DOMAIN
 - if you run 'gunicorn -b IP:PORT app:app', the DOMAIN should be 'http://IP:PORT'


License
-------
CODE is under Revised BSD License.
See the [LICENSE file](https://github.com/douban/code/blob/master/LICENSE) for the full license text.

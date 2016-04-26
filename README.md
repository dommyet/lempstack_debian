# LEMP stack configuration files

The **lempstack** repository provides configuration files to allow administrators to easily set up a secure LEMP web server.

Both [PHP5](http://php.net/) and [PHP7](http://php.net/) are supported, there are also configurations for [fail2ban](http://www.fail2ban.org/), [goaccess](https://goaccess.io/) and [munin](http://munin-monitoring.org/).

## APT Repository Settings

These configurations should be able to run smoothly on **Debian testing**. Assume you are a Linode user, below is an example of  `/etc/apt/sources.list`.

```
deb http://mirrors.linode.com/debian/ testing main
deb http://mirrors.linode.com/debian/ testing-updates main
deb http://mirrors.linode.com/debian-security/ testing/updates main
```

After the modification you need to run a dist-upgrade.

```
apt-get update
apt-get dist-upgrade
```

Most of the configurations could also run without problem on **Debian stable**. However some functions are unavailable because the specific version of software provided by **Debian stable** does not support them, for example, [**NGINX**](http://nginx.org/) provided in **Debian stable** does not support HTTP/2. Assume you are running **Debian stable** but you want to install [**NGINX**](http://nginx.org/) from **Debian testing** repository, you could do the following.

```
echo 'APT::Default-Release "jessie";' > /etc/apt/apt.conf.d/99defaultrelease
apt-get update
apt-get -t testing install nginx
```

## Logjam Attack

To aviod [**Logjam attack**](https://weakdh.org/) you **SHOULD** run the following command to generate your own dhparam, the file provided is just an example and you **SHOULD NOT** use it. The generation process is going to take a long time (a few minutes).

```
openssl dhparam -out /etc/ssl/private/dhparam.pem 4096
```

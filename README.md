# LEMP stack configuration files

The **lempstack** repository provides configuration files to allow administrators to easily set up a secure LEMP web server.

Both [PHP5](http://php.net/) and [PHP7](http://php.net/) are supported, there are also configurations for [fail2ban](http://www.fail2ban.org/), [goaccess](https://goaccess.io/) and [munin](http://munin-monitoring.org/).

## APT Repository Settings

These configurations should be able to run smoothly on current **Debian stable** with some newer packages installed from **Debian testing**.

In order to set up two repositories properly and make the stable one as default, we could create a configuration file to set default release.

```
echo 'APT::Default-Release "jessie";' > /etc/apt/apt.conf.d/99defaultrelease
```

And below is an example of  `/etc/apt/sources.list`, assuming you are a Linode user.

```
deb http://mirrors.linode.com/debian/ jessie main
deb http://mirrors.linode.com/debian/ jessie-updates main
deb http://mirrors.linode.com/debian-security/ jessie/updates main
deb http://mirrors.linode.com/debian/ testing main
deb http://mirrors.linode.com/debian/ testing-updates main
deb http://mirrors.linode.com/debian-security/ testing/updates main
```

Now you could install packages from **Debian stable** just like before, for example.

```
apt-get update
apt-get install iptables-persistent
```

To install packages from **Debian testing**, for example the newer version of [**nginx**](http://nginx.org/) that supports HTTP/2, you could do the following.

```
apt-get update
apt-get -t testing install nginx
```

## Logjam Attack

To aviod [**Logjam attack**](https://weakdh.org/) you **SHOULD** run the following command to generate your own dhparam, the file provided is just an example and you **SHOULD NOT** use it. The generation process is going to take a long time (a few minutes).

```
openssl dhparam -out /etc/ssl/private/dhparam.pem 4096 && chmod 0640 /etc/ssl/private/dhparam.pem
```

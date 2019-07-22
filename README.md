# LEMP stack configuration files for Debian

The **lempstack_debian** repository provides configuration files for setting up a secure LEMP web server on Debian.

Both [php5](http://php.net/) and [php7](http://php.net/) are supported, there are also configurations for [fail2ban](http://www.fail2ban.org/), [goaccess](https://goaccess.io/) and [munin](http://munin-monitoring.org/).

## APT Repository Settings

### Debian testing ( Recommended )

Below is an example of  `/etc/apt/sources.list`, please refer to [Debian SourceList](https://wiki.debian.org/SourcesList/).

```
deb http://deb.debian.org/debian testing main
deb http://deb.debian.org/debian-security/ testing/updates main
deb http://deb.debian.org/debian testing-updates main
```

### Debian stable

Using these configurations on current **Debian stable** would generally work. However, minor issues might be expected.

Below is an example of  `/etc/apt/sources.list`, please refer to [Debian SourceList](https://wiki.debian.org/SourcesList/).

```
deb http://deb.debian.org/debian stable main
deb http://deb.debian.org/debian-security/ stable/updates main
deb http://deb.debian.org/debian stable-updates main
```

### Using Debian testing packages on Debian stable

Using new packages from **Debian testing** on **Debian stable** would generally work. However, minor issues might be expected.

Put all six sources above into `/etc/apt/sources.list`, and tell the system to install packages from **Debian stable** as default.

```
echo 'APT::Default-Release "stable";' > /etc/apt/apt.conf.d/99defaultrelease
```

Now packages could be installed from **Debian stable** like normal. To install packages from **Debian testing**, use `-t` to specify the desired release.

```
sudo apt-get update
sudo apt-get -t testing install nginx
```

## Logjam Attack

To aviod [**Logjam attack**](https://weakdh.org/) the following command **SHOULD** be executed to generate your own dhparam. The provided example **SHOULD NOT** be used.

The generation process is going to take a long time (a few minutes).

```
sudo openssl dhparam -out /etc/ssl/private/dhparam.pem 4096 && sudo chmod 0640 /etc/ssl/private/dhparam.pem
```

## Performance and fine tune

These configurations are designed to run on low performance servers, typically those with 1-2 vCPU(s) and 1-2 GB of RAM.

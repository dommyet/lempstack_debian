# LEMP stack configuration files

The **lempstack** repository provides configuration files to allow administrators to easily set up a secure LEMP web server.

Both [php5](http://php.net/) and [php7](http://php.net/) are supported, there are also configurations for [fail2ban](http://www.fail2ban.org/), [goaccess](https://goaccess.io/) and [munin](http://munin-monitoring.org/).

## APT Repository Settings

For a proper setup you need to configurate your package source.

### Debian testing ( Recommended )

The provided configurations should be able to run smoothly on **Debian testing**, it is also the recommended version.

And below is an example of  `/etc/apt/sources.list`, assuming you are a Linode user.

```
deb http://mirrors.linode.com/debian/ testing main
deb http://mirrors.linode.com/debian/ testing-updates main
deb http://mirrors.linode.com/debian-security/ testing/updates main
```

### Debian stable

You might encounter minor problems while running these configurations on current **Debian stable**, but generally it will work.

However you should keep in mind that packages provided by **Debian stable** are relatively old.

- **php7** is not provided
- **nginx** comes without HTTP/2 support

And below is an example of  `/etc/apt/sources.list`, assuming you are a Linode user.

```
deb http://mirrors.linode.com/debian/ jessie main
deb http://mirrors.linode.com/debian/ jessie-updates main
deb http://mirrors.linode.com/debian-security/ jessie/updates main
```

### Debian stable plus testing

Obtaining newer packages from **Debian testing** on **Debian stable** is one solution, generally it will work without problem.

Put all six sources above into `/etc/apt/sources.list`, and tell the system to install packages from **Debian stable** as default.

```
echo 'APT::Default-Release "jessie";' > /etc/apt/apt.conf.d/99defaultrelease
```

Now you could install packages from **Debian stable** just like normal, to install from **Debian testing**, use `-t` to specify the release you want.

```
apt-get update
apt-get -t testing install nginx
```

## Logjam Attack

To aviod [**Logjam attack**](https://weakdh.org/) you **SHOULD** run the following command to generate your own dhparam, the file provided is just an example and you **SHOULD NOT** use it. The generation process is going to take a long time (a few minutes).

```
openssl dhparam -out /etc/ssl/private/dhparam.pem 4096 && chmod 0640 /etc/ssl/private/dhparam.pem
```

## Performance and fine tune

These configurations are designed to run on low performance servers, typically those with 1 vCPU and 1-2 GB of RAM.

I put most of the important parameters in the beginning of each configuration files, and there are also useful comments. The administrator should look into these configurations and adjust them according to your situation.
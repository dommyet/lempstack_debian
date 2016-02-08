# LEMP stack configuration files #

This repository holds LEMP stack configuration files for production environment.
All configurations in this repository were tested on [Debian testing](https://www.debian.org/releases/testing/).

## Notes ##

- To prevent [Logjam attack](https://weakdh.org/) please issue `openssl dhparam -out /etc/ssl/private/dhparam.pem 2048` in terminal.

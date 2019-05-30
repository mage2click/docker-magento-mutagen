<h1 align="center">mage2click/docker-magento-mutagen</h1> 

<div align="center">
  <p>Mage2click Docker Configuration for Magento with <a href="https://mutagen.io" target="_blank">mutagen.io</a> sync for files inspired by <a href="https://twitter.com/markshust" target="_blank">Mark Shust</a>'s <a href="https://github.com/markshust/docker-magento" target="_blank">markshust/docker-magento</a> project</p>
  <a href="https://github.com/magento/magento2" target="_blank"><img src="https://img.shields.io/badge/magento-2.X-brightgreen.svg?logo=magento&longCache=true" alt="Supported Magento Versions" /></a>
  <a href="https://hub.docker.com/r/mage2click/magento-nginx/" target="_blank"><img src="https://img.shields.io/docker/pulls/mage2click/magento-nginx.svg?label=nginx%20docker%20pulls" alt="Docker Hub Pulls - Nginx" /></a>
  <a href="https://hub.docker.com/r/mage2click/magento-php-versions/" target="_blank"><img src="https://img.shields.io/docker/pulls/mage2click/magento-php-versions.svg?label=php%20docker%20pulls" alt="Docker Hub Pulls - PHP" /></a>
  <a href="https://hub.docker.com/r/mage2click/magento-varnish/" target="_blank"><img src="https://img.shields.io/docker/pulls/mage2click/magento-varnish.svg?label=varnish%20docker%20pulls" alt="Docker Hub Pulls - Varnish" /></a>
  <a href="https://hub.docker.com/r/mage2click/magento-elasticsearch/" target="_blank"><img src="https://img.shields.io/docker/pulls/mage2click/magento-elasticsearch.svg?label=elasticsearch%20docker%20pulls" alt="Docker Hub Pulls - Elasticsearch" /></a>
  <a href="https://hub.docker.com/r/mage2click/magento-proxy/" target="_blank"><img src="https://img.shields.io/docker/pulls/mage2click/magento-proxy.svg?label=proxy%20docker%20pulls" alt="Docker Hub Pulls - Proxy" /></a>
  <a href="https://github.com/mage2click/docker-magento-mutagen/graphs/commit-activity" target="_blank"><img src="https://img.shields.io/badge/maintained%3F-yes-brightgreen.svg" alt="Maintained - Yes" /></a>
  <a href="https://github.com/mage2click/docker-magento-mutagen/blob/master/LICENSE.md" target="_blank"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License MIT"/></a>
  <a href="https://join.slack.com/t/magentocommeng/shared_invite/enQtNDUzMDg4Mzc4NTY3LWEyOThjMzY5Zjk2ZGVjZWZmNTU4ZjJkYmQzMWNjY2MwMzRlNDM0ODMyZTVmM2NjODIwOTNjZWQ4NTM2ZjU2YmE" target="_blank"><img src="https://img.shields.io/badge/chat-%23mutagen--sync%20in%20Slack-brightgreen.svg" alt="chat #mutagen-sync in Slack"/></a>
  <a href="https://twitter.com/intent/follow?screen_name=mage2_click" target="_blank"><img src="https://img.shields.io/twitter/follow/mage2_click.svg?style=social" /></a>
</div>

## Table of contents

- [Docker Hub](#docker-hub)
- [Usage](#usage)
- [Prerequisites](#prerequisites)
- [Mutagen.io](#mutagen)
- [Automated Setup](#automated-setup)
- [Magento 1](#Magento1)
- [Magento 2](#Magento2)
- [Credits](#credits)
- [License](#license)

## Docker Hub

View Dockerfiles:

- [mage2click/magento-nginx (Docker Hub)](https://hub.docker.com/r/mage2click/magento-nginx/)
  - 1.13
      - [`latest`, `1.13`](https://github.com/mage2click/magento-nginx/tree/1.13)

- [mage2click/magento-php-versions (Docker Hub)](https://hub.docker.com/r/mage2click/magento-php-versions/)
  - 7.2
      - [`latest`, `7.2-fpm-mailhog`](https://github.com/mage2click/magento-php-versions/tree/master/7.2/official/fpm-mailhog)
      - [`7.2-fpm`](https://github.com/mage2click/magento-php-versions/tree/master/7.2/official/fpm) 
  - 7.1
      - [`7.1-fpm-mailhog`](https://github.com/mage2click/magento-php-versions/tree/master/7.1/official/fpm-mailhog)
      - [`7.1-fpm`](https://github.com/mage2click/magento-php-versions/tree/master/7.1/official/fpm)
  - 7.0
      - [`7.0-fpm-mailhog`](https://github.com/mage2click/magento-php-versions/tree/master/7.0/official/fpm-mailhog)
      - [`7.0-fpm`](https://github.com/mage2click/magento-php-versions/tree/master/7.0/official/fpm)
  - 5.6
      - [`5.6-fpm-mailhog`](https://github.com/mage2click/magento-php-versions/tree/master/5.6/official/fpm-mailhog)
      - [`5.6-fpm`](https://github.com/mage2click/magento-php-versions/tree/master/5.6/official/fpm)
      
- [mage2click/magento-elasticsearch (Docker Hub)](https://hub.docker.com/r/mage2click/magento-elasticsearch)
  - 6.7.2
      - [`latest`, `6.7.2`](https://github.com/mage2click/magento-elasticsearch/tree/master/6.7.2/official)
  - 5.6
      - [`5.6`](https://github.com/mage2click/magento-elasticsearch/tree/master/5.6/official)
  - 2.4    
      - [`2.4`](https://github.com/mage2click/magento-elasticsearch/tree/master/2.4/official)
            
- [mage2click/magento-varnish (Docker Hub)](https://hub.docker.com/r/mage2click/magento-varnish)
  - 4.1
    - [`latest`, `4.1`](https://github.com/mage2click/magento-varnish/)
    
- [mage2click/magento-proxy (Docker Hub) - based on Nginx, used for envs with Varnish](https://hub.docker.com/r/mage2click/magento-proxy)
  - 1.13-0
    - [`latest`, `1.13-0`](https://github.com/mage2click/magento-proxy/)  
## Usage

This configuration is intended to be used as a Docker-based development environment for Magento 2.

Folders:
- `compose`: sample setups with Docker Compose
- `lib`: files used in one line setup scripts

## Prerequisites

This setup assumes you are running Docker on a computer with at least 6GB of allocated RAM, a dual-core, and an SSD hard drive. [Download & Install Docker Desktop for Mac (Community Edition)](https://hub.docker.com/editions/community/docker-ce-desktop-mac).

This configuration has been tested on macOS.

## Mutagen
This version of Docker-based development environment with mutagen sync is working fine even if it still under development, it requires the <a href="https://mutagen.io/" target="_blank">mutagen.io</a> to be installed on your system. See the <a href="https://mutagen.io/documentation/installation/" target="_blank">mutagen.io/documentation/installation</a> or use  <a href="https://brew.sh/" target="_blank">Homebrew</a> to install it on macOS

```bash
brew install havoc-io/mutagen/mutagen
```

## Automated Setup
### [Magento1](M1.md)
### [Magento2](M2.md)


## Misc Info

### Database

The hostname of each service is the name of the service within the `docker-compose.yml` file. So for example, MySQL's (based on [MariaDB:10.3](https://mariadb.com/kb/en/library/changes-improvements-in-mariadb-103/) [Docker image](https://hub.docker.com/_/mariadb)) hostname is `db` (not `localhost`) when accessing it from within a Docker container. Elasticsearch's hostname is `elasticsearch`.

Here's an example of how to connect to the MySQL cli tool of the Docker instance:

```
bin/cli mysql -h db -umagento -pmagento magento
```

You can use the `bin/clinotty` helper script to import a database. This example uses the root MySQL user, and looks for the `dbdump.sql` file in your local host directory:

```
bin/clinotty mysql -hdb -umagento -pmagento magento < dbdump.sql
```

### Composer Authentication

Get your authentication keys for Magento Marketplace. For more information about Magento Marketplace authentication, see the [DevDocs](http://devdocs.magento.com/guides/v2.3/install-gde/prereq/connect-auth.html).  

The setup script will prompt you to provide authentication information!

To manually configure authentication, copy `src/auth.json.sample` to `src/auth.json`. Then, update the username and password values with your Magento public and private keys, respectively. Finally, copy the file to the container by running `bin/copytocontainer auth.json`.

### Redis

Redis is now the default cache and session storage engine, and is automatically configured & enabled when running `bin/setup` on new installs.

Use the following lines to enable Redis on existing installs:

**Enable for Cache:**

`bin/magento setup:config:set --cache-backend=redis --cache-backend-redis-server=redis --cache-backend-redis-db=0`

**Enable for Full Page Cache:**

`bin/magento setup:config:set --page-cache=redis --page-cache-redis-server=redis --page-cache-redis-db=1`

**Enable for Session:**

`bin/magento setup:config:set --session-save=redis --session-save-redis-host=redis --session-save-redis-log-level=4 --session-save-redis-db=2`

You may also monitor Redis by running: `bin/redis redis-cli monitor`

For more information about Redis usage with Magento, see the <a href="https://devdocs.magento.com/guides/v2.3/config-guide/redis/redis-session.html" target="_blank">DevDocs</a>.


### Xdebug & PHPStorm
Please see the detailed instructions of how to configure and use it on our Wiki page [Xdebug & PHPStorm](https://github.com/mage2click/docker-magento-mutagen/wiki/Xdebug-&-PHPStorm)
## Credits

### Mark Shust

<a href="https://u.magento.com/certification/directory/dev/883/" target="_blank">Certified Magento Developer & Architect</a> and <a href="http://www.zend.com/en/yellow-pages/ZEND014633" target="_blank">Zend Certified Engineer</a>, and available for consulting & development of your next project 🤓. You can read technical articles on my blog at <a href="https://markshust.com" target="_blank">markshust.com</a> or contact me directly at <a href="mailto:mark@shust.com">mark@shust.com</a>.  
<a href="https://courses.markshust.com/p/setup-magento-2-development-environment-docker" target="_blank">Mark Shust's Free Course about Setup a Magento 2 Development Environment with Docker</a>

### Nexcess

A special thanks goes out to <a href="https://www.nexcess.net/" target="_blank">Nexcess</a> for hosting <a href="http://pubfiles.nexcess.net/magento/ce-packages/" target="_blank">public archives of every version of Magento</a> 💙. I've used their Magento hosting services in the past also (both <a href="https://www.nexcess.net/magento/hosting/" target="_blank">shared</a> and <a href="https://www.nexcess.net/magento/enterprise-hosting/" target="_blank">enteprise</a> offerings) and they're great, ...highly recommended!

### Willem Wigman
Implemented Varnish support with https proxy <a href="https://github.com/wigman" target="_blank">Willem Wigman</a>

### Max Uroda
<a href="https://u.magento.com/certification/directory/dev/1122780/" target="_blank">Certified Magento Developer (M1CDP+ / M2CAD)</a>, WebDeveloper interested in Magento/Magento2, Docker, JS, Varnish, PWA  
<a href="https://twitter.com/u_maxx" target="_blank">@u_maxx</a>  
<a href="https://maxuroda.pro" target="_blank">maxuroda.pro</a> 

### Dmitry Shkoliar
<a href="https://www.zend.com/en/yellow-pages/ZEND026786" target="_blank">Zend Certified PHP Engineer</a>, Magento2, Docker, PWA, Varnish, JS, HTML5, Mobile, iOS, Android  
<a href="https://twitter.com/shkoliar" target="_blank">@shkoliar</a>  
<a href="https://shkoliar.com" target="_blank">shkoliar.com</a>  


## License

[MIT](https://github.com/mage2click/docker-magento-mutagen/blob/master/LICENSE.md)

## Maintainers

* [Dmitry Shkoliar](https://github.com/shkoliar) 
* [Max Uroda](https://github.com/u-maxx)
* Feel free to create new GitHub issue with feature request or PR with feature/bugfix :) 

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
- [Custom CLI Commands](#custom-cli-commands)
- [Misc Info](#misc-info)
- [Credits](#credits)
- [License](#license)

## Docker Hub

Please see available Dockerfiles on our [Docker Hub Wiki page](https://github.com/mage2click/docker-magento-mutagen/wiki/Docker-Hub)

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

Run one of the commands below from the directory you want to install your project to. Existing projects can be imported as well.

### Interactive mode

```bash
curl -s https://raw.githubusercontent.com/mage2click/docker-magento-mutagen/master/lib/setup | bash -s -- -i
```

The `-i` flag above (shorthand of `--interactive`) defines that setup script must be launched in interactive mode.  
Simply follow the steps during setup initialisation to configure resulted Magento development environment.

### One-line mode 

```bash
curl -s https://raw.githubusercontent.com/mage2click/docker-magento-mutagen/master/lib/setup | bash -s -- --domain=magento2.test
```

The `--domain=magento2.test` above defines the hostname to use.  
Script accepts also other parameters and flags to configure resulted Magento development environment.

Parameters:  
- `--domain=<domain>` Domain to use for the project, default is `magento2.test`.
- `--php-version=<version>` PHP version to use for the project, default is `7.2`. Currently supported PHP versions: `7.0`, `7.1` and `7.2`.
- `--elasticsearch-version=<version>` Elasticsearch version to use for the project, default is `6.7.2`. Currently supported Elasticsearch versions: `2.4`, `5.6` and `6.7.2`. All versions have the [analysis-phonetic](https://www.elastic.co/guide/en/elasticsearch/plugins/master/analysis-phonetic.html) plugin installed.
- `--magento-archive=<path>` Full path to downloaded Magento zip-archive to use in setup (optional).
- `--magento-project=<path>` Full path to the existing Magento project to use in setup (optional).
- `--magento-db=<path>` Full path to sql-file with database dump to use in setup (optional).
- `--magento-version=<version>` Magento version to download from the official repository, default is `2.3.1`. If `--magento-archive` parameter is specified, this will be skipped.

Flags:
- `--composer` Use \`composer install\` command during the setup process.
- `--varnish` Use Varnish cache.
- `--mailhog` Use MailHog email testing tool.
- `--rabbitmq` Use RabbitMQ message-broker.
- `--cron` Use cron service.
- `-i`, `--interactive` Start interactive setup.
- `-h`, `--help` Show usage information.

### Usage info output

```bash
curl -s https://raw.githubusercontent.com/mage2click/docker-magento-mutagen/master/lib/setup | bash -s -- -h
```

The `-h` flag above (shorthand of `--help`) defines that setup script must only output usage information. This command won't start the installation process.


## Custom CLI Commands

- `bin/bash`: Drop into the bash prompt of your Docker container. The `phpfpm` container should be mainly used to access the filesystem within Docker.
- `bin/dev-urn-catalog-generate`: Generate URN's for PHPStorm and remap paths to local host. Restart PHPStorm after running this command.
- `bin/cli`: Run any CLI command without going into the bash prompt. Ex. `bin/cli ls`
- `bin/clinotty`: Run any CLI command with no TTY. Ex. `bin/clinotty chmod u+x bin/magento`
- `bin/composer`: Run the composer binary. Ex. `bin/composer install`
- `bin/copyfromcontainer`: Copy folders or files from container to host. Ex. `bin/copyfromcontainer vendor`
- `bin/copytocontainer`: Copy folders or files from host to container. Ex. `bin/copytocontainer --all`
- `bin/fixowns`: This will fix filesystem ownerships within the container.
- `bin/fixperms`: This will fix filesystem permissions within the container.
- `bin/grunt`: Run the grunt binary. Note that this runs the version from the node_modules directory for project version parity. Ex. `bin/grunt exec`
- `bin/magento`: Run the Magento CLI. Ex: `bin/magento cache:flush`
- `bin/mr`: Run [n98-magerun2.phar](https://github.com/netz98/n98-magerun2) inside the php-fpm container.
- `bin/mutagen`: Mutagen sync related commands. Accepts params `start`, `stop` or `flush [html|vendor]`. If `flush` has extra param `html` or `vendor`, only corresponded session will be flushed. Ex. `bin/mutagen start`
- `bin/node`: Run the node binary. Ex. `bin/node --version`
- `bin/npm`: Run the npm binary. Ex. `bin/npm install`
- `bin/redis`: Run a command from the redis container. Ex `bin/redis redis-cli monitor`
- `bin/remove`: Remove all stopped service containers. Accepts params `-v` or `--volumes` to remove volumes.
- `bin/restart`: Restarts all service containers. If one or more service names specified, only corresponded service containers will be restarted.
- `bin/restart-nginx`: Restart the app container (nginx) to apply new changes to nginx.conf files (src/nginx.conf).
- `bin/root`: Run any CLI command as root without going into the bash prompt. Ex `bin/root apt-get install nano`
- `bin/rootnotty`: Run any CLI command as root with no TTY. Ex `bin/rootnotty chown -R app:app /var/www/html`
- `bin/self-update`: Alias for bin/update.
- `bin/selfupdate`: Alias for bin/update.
- `bin/start`: Start all containers, good practice to use this instead of `docker-compose up -d`, as it may contain additional helpers.
- `bin/status`: Check the container status.
- `bin/stop`: Stop all containers.
- `bin/update`: Update the contents of the bin folder with the latest changes from the master branch and/or Docker images along with the rebuilding of corresponding containers and\or mutagen (only if needed). Accepts optional arguments `-v|--version=<version>` (to specify version tag or branch path to fetch from, default is `master`, affects only bin scripts), `-i|--images` updates only Docker images along with the rebuilding of corresponding containers, `-m|--mutagen` updates only mutagen (only if needed), `-a|--all` updates bin scripts, Docker images along with the rebuilding of corresponding containers and mutagen (if needed). 
- `bin/varnish`: Run commands in the Varnish container. Ex `bin/varnish varnishlog -q 'ReqURL ~ "^/$"'` to monitor requests to homepage, or `bin/vanirsh varnishlog -g request -q 'ReqMethod eq "PURGE"'` to monitor PURGE requests.
- `bin/xdebug`: Disable or enable Xdebug by removing/adding corresponding .so line from/to .ini file in the PHP-FPM container.  Accepts params `disable` or `enable`. Ex. `bin/xdebug enable`. Xdebug extension is installed but disabled by default, as well as remote connections and autostart are disabled. Use our `bin/setup/xdebug` command to get xdebug.* ini settings configured, or you can specify any xdebug.* settings via `pub/.user.ini` file inside the magento project folder.

## Setup and Configuration CLI Commands

- `bin/setup/elasticsearch`: Enable Elasticsearch as Search Engine (6.7.2 by default, see [Magento 2.3.1 Supported versions](https://devdocs.magento.com/guides/v2.3/config-guide/elasticsearch/es-overview.html#es-spt-versions) for more info).
    #### Flags:
    - `2.4`: enable Elasticsearch 2.4
    - `5.6`: enable Elasticsearch 5.6
    - `6.7.2` or no flag: enable Elasticsearch 6.7.2
    
- `bin/setup/download`: Download & extract specific Magento version to the `src` directory. Ex. `bin/setup/download 2.3.1`
- `bin/setup/import`: Copy files of existing Magento project to the `src` directory. Ex. `bin/setup/import /path/to/magento/project`
- `bin/setup/redis`: Enable Redis for Backend Cache, Page Cache and Session.
- `bin/setup/start`: Run the Magento setup process to install Magento from the source code, with the optional parameter `--domain=<domain>` (defaults to `magento2.test`) and optional `--composer` flag. Ex. `bin/setup/start --domain=magento2.test` 
- `bin/setup/unzip`: Extract downloaded Magento zip-archive to the `src` directory. Ex. `bin/setup/unzip /path/to/magento.zip`
    #### Varnish:
    - `bin/setup/varnish` Varnish-related configurations and VCL-related actions   
        #### Flags: 
        - `--configure`: Apply required settings to enable Varnish as Caching Application for Full Page Cache and handle cache invalidations correctly
        - `--generate-vcl`: Generate the default.vcl file with the default Varnish config, save it to the var/default.vcl and copy from the phpfpm container to ./src/var/default.vcl .
        - `--list-vcl`: Show info from varnish container with the list of loaded VCLs, and active vcl.
        #### Parameters: 
        - `--apply-vcl`: Apply the specified VCL file with Varnish config (or default.vcl if no argument specified), with automated copying it from the ./src/var/ folder to the varnish container, also showing additional info about the list of loaded VCLs and active VCL before and after execution of this command.
        - `--copy-vcl`: Copy the specified file (or default.vcl if no argument specified) from the ./src/var/ folder to the varnish container. 
        - `--use-vcl`: Use the specified VCL (you should specify one of the names from the bin/setup/varnish --list-vcl output - for example "boot") as active config for varnish container.
- `bin/setup/n98-magerun2`: Install [n98-magerun2.phar](https://github.com/netz98/n98-magerun2) to the /usr/local/bin/ folder inside the php-fpm container.
- `bin/setup/xdebug`: Enable remote debugging via set of xdebug.* ini settings in .user.ini file. Please see the detailed instructions of how to configure and use it on our Wiki page [Xdebug & PHPStorm](https://github.com/mage2click/docker-magento-mutagen/wiki/Xdebug-&-PHPStorm) 
## Misc Info

### Admin Panel
The admin panel URL is auto-generated by the setup script. You can find the URL by using the `bin/magento info:admin` command. The default username is `john.smith` and the default password is `password123`.

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

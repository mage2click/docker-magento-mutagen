<h1 align="center">mage2click/docker-magento-mutagen</h1> 

<div align="center">
  <p>Mage2click Docker Configuration for Magento with <a href="https://mutagen.io" target="_blank">mutagen.io</a> sync for files inspired by <a href="https://twitter.com/markshust" target="_blank">Mark Shust</a>'s <a href="https://github.com/markshust/docker-magento" target="_blank">markshust/docker-magento</a> project</p>
  <a href="https://github.com/magento/magento2" target="_blank"><img src="https://img.shields.io/badge/magento-2.X-brightgreen.svg?logo=magento&longCache=true" alt="Supported Magento Versions" /></a>
  <a href="https://hub.docker.com/r/mage2click/magento-nginx/" target="_blank"><img src="https://img.shields.io/docker/pulls/mage2click/magento-nginx.svg?label=nginx%20docker%20pulls" alt="Docker Hub Pulls - Nginx" /></a>
  <a href="https://hub.docker.com/r/mage2click/magento-php/" target="_blank"><img src="https://img.shields.io/docker/pulls/mage2click/magento-php.svg?label=php%20docker%20pulls" alt="Docker Hub Pulls - PHP" /></a>
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
- [Quick Setup](#quick-setup)
- [Custom CLI Commands](#custom-cli-commands)
- [Misc Info](#misc-info)
- [Credits](#credits)
- [License](#license)
- [TBD](#tbd)

## Docker Hub

View Dockerfiles:

- [mage2click/magento-nginx (Docker Hub)](https://hub.docker.com/r/mage2click/magento-nginx/)
  - 1.13
      - [`latest`, `1.13`](https://github.com/mage2click/magento-nginx/tree/1.13)

- [mage2click/magento-php (Docker Hub)](https://hub.docker.com/r/mage2click/magento-php//)
  - 7.2
      - [`latest`, `7.2-fpm-mailhog`](https://github.com/mage2click/magento-php/tree/7.2-fpm-mailhog)
      - [`7.2-fpm`](https://github.com/mage2click/magento-php/tree/7.2-fpm) 
  - 7.1
      - [`7.1-fpm-mailhog`](https://github.com/mage2click/magento-php/tree/7.1-fpm-mailhog)
      - [`7.1-fpm`](https://github.com/mage2click/magento-php/tree/7.1-fpm)

## Usage

This configuration is intended to be used as a Docker-based development environment for Magento 2.

Folders:
- `compose`: sample setups with Docker Compose
- `lib`: files used in one line setup scripts

## Prerequisites

This setup assumes you are running Docker on a computer with at least 4GB of allocated RAM, a dual-core, and an SSD hard drive. [Download & Install Docker Community Edition](https://www.docker.com/community-edition#/download).

This configuration has been tested on macOS.
### Mutagen
This version of Docker-based development environment with mutagen sync is working fine even if it still under development, it requires the <a href="https://mutagen.io/" target="_blank">mutagen.io</a> to be installed on your system. See the <a href="https://mutagen.io/documentation/installation/" target="_blank">mutagen.io/documentation/installation</a> or use  <a href="https://brew.sh/" target="_blank">Homebrew</a> to install it on macOS
```bash
brew install havoc-io/mutagen/mutagen
```
## Quick Setup

### Automated Setup (New Project)

> macOS Only

Run this automated one-liner from the directory you want to install your project to:

```bash
curl -s https://raw.githubusercontent.com/mage2click/docker-magento-mutagen/master/lib/onelinesetup | bash -s -- magento2.test 2.3.1
```

or use the following command to install from the zip file downloaded from magento.com :

```bash
curl -s https://raw.githubusercontent.com/mage2click/docker-magento-mutagen/master/lib/onelinesetup | bash -s -- magento2.test /path/to/magento.zip lite
```

The `magento2.test` above defines the hostname to use, and the `/path/to/magento.zip` defines the local path to Magento zip archive.   
The `lite` param at the end means that we do not need to execute composer install during the setup because zip version of magento already have all needed files in the vendor folder

Note that since we need a write to `/etc/hosts` for DNS resolution, you will be prompted for your system password during setup.

After the one-liner above completes running, you should be able to access your site at `https://magento2.test`.

### Manual Setup

Same result as the one-liner above. Just replace `magento2.test` references with the hostname that you wish to use.

#### New Projects

```bash
# Download the Docker Compose template:
curl -s https://raw.githubusercontent.com/mage2click/docker-magento-mutagen/master/lib/template | bash -s -- magento-2

# Download the version of Magento you want to use with:
bin/download 2.3.1

# or if you'd rather install with Composer, run:
#
# OPEN SOURCE:
#
# rm -rf src
# composer create-project --repository=https://repo.magento.com/ --ignore-platform-reqs magento/project-community-edition=2.3.1 src
#
# COMMERCE:
#
# rm -rf src
# composer create-project --repository=https://repo.magento.com/ --ignore-platform-reqs magento/project-enterprise-edition=2.3.1 src

# Create a DNS host entry for the site:
echo "127.0.0.1 magento2.test" | sudo tee -a /etc/hosts

# Run the setup installer for Magento:
bin/setup magento2.test

open https://magento2.test
```

#### Existing Projects

```bash
# Download the Docker Compose template:
curl -s https://raw.githubusercontent.com/mage2click/docker-magento-mutagen/master/lib/template | bash -s -- magento-2

# Remove existing src directory:
rm -rf src

# Replace with existing source code of your existing Magento instance:
cp ~/Sites/existing src
# or: git clone git@github.com:myrepo.git src

# Create a DNS host entry for the site:
echo "127.0.0.1 magento2.test" | sudo tee -a /etc/hosts

# Copy some files to the containers and install dependencies, then restart the containers:
docker-compose up -d
bin/copytocontainer --all

# Install composer dependencies, then copy artifacts back to the host:
bin/composer install
bin/copyfromcontainer vendor

# Import existing database:
bin/clinotty mysql -hdb -umagento -pmagento magento < existing/magento.sql

# Update database connection details:
# vi src/app/etc/env.php

# Set base URLs to local environment URL:
bin/magento config:set web/secure/base_url https://magento2.test/
bin/magento config:set web/unsecure/base_url https://magento2.test/

bin/restart

open https://magento2.test
```

> For more details on how everything works, see the extended [setup readme](https://github.com/mage2click/docker-magento-mutagen/blob/master/SETUP.md).

## Custom CLI Commands

- `bin/bash`: Drop into the bash prompt of your Docker container. The `phpfpm` container should be mainly used to access the filesystem within Docker.
- `bin/dev-urn-catalog-generate`: Generate URN's for PHPStorm and remap paths to local host. Restart PHPStorm after running this command.
- `bin/cli`: Run any CLI command without going into the bash prompt. Ex. `bin/cli ls`
- `bin/clinotty`: Run any CLI command with no TTY. Ex. `bin/clinotty chmod u+x bin/magento`
- `bin/composer`: Run the composer binary. Ex. `bin/composer install`
- `bin/copyfromcontainer`: Copy folders or files from container to host. Ex. `bin/copyfromcontainer vendor`
- `bin/copytocontainer`: Copy folders or files from host to container. Ex. `bin/copytocontainer --all`
- `bin/download`: Download & extract specific Magento version to the `src` directory. Ex. `bin/download 2.3.1`
- `bin/fixowns`: This will fix filesystem ownerships within the container.
- `bin/fixperms`: This will fix filesystem permissions within the container.
- `bin/grunt`: Run the grunt binary. Note that this runs the version from the node_modules directory for project version parity. Ex. `bin/grunt exec`
- `bin/magento`: Run the Magento CLI. Ex: `bin/magento cache:flush`
- `bin/node`: Run the node binary. Ex. `bin/node --version`
- `bin/npm`: Run the npm binary. Ex. `bin/npm install`
- `bin/redis`: Run a command from the redis container. Ex `bin/redis redis-cli monitor`
- `bin/remove`: Remove all containers.
- `bin/removevolumes`: Remove all volumes.
- `bin/restart`: Stop and then start all containers.
- `bin/root`: Run any CLI command as root without going into the bash prompt. Ex `bin/root apt-get install nano`
- `bin/rootnotty`: Run any CLI command as root with no TTY. Ex `bin/rootnotty chown -R app:app /var/www/html`
- `bin/setup`: Run the Magento setup process to install Magento from the source code, with optional domain name. Defaults to `magento2.test`. Ex. `bin/setup magento2.test`
- `bin/start`: Start all containers, good practice to use this instead of `docker-compose up -d`, as it may contain additional helpers.
- `bin/status`: Check the container status.
- `bin/stop`: Stop all containers.
- `bin/varnish`: Run commands in the Varnish container. Ex `bin/varnish varnishlog -q 'ReqURL ~ "^/$"'` to monitor requests to homepage, or `bin/vanirsh varnishlog -g request -q 'ReqMethod eq "PURGE"'` to monitor PURGE requests
- `bin/xdebug`: Disable or enable Xdebug. Accepts params `disable` (default) or `enable`. Ex. `bin/xdebug enable`
- `bin/magento-configure-elasticsearch5`: Enabling Elasticsearch 5 as Search Engine...
- `bin/mutagen-start`: Start mutagen daemon & sync.
- `bin/mutagen-stop`: Stop mutagen daemon & sync.
- `bin/update`: Update the content of the bin folder and docker-compose.yml file with the latest changes from the master branch.
- `bin/selfupdate`: Alias for bin/update.
- `bin/self-update`: Alias for bin/update.
## Misc Info

### Database

The hostname of each service is the name of the service within the `docker-compose.yml` file. So for example, MySQL's hostname is `db` (not `localhost`) when accessing it from within a Docker container. Elasticsearch's hostname is `elasticsearch`.

Here's an example of how to connect to the MySQL cli tool of the Docker instance:

```
bin/cli mysql -h db -umagento -pmagento magento
```

You can use the `bin/clinotty` helper script to import a database. This example uses the root MySQL user, and looks for the `dbdump.sql` file in your local host directory:

```
bin/clinotty mysql -h db -u root -pmagento magento < dbdump.sql
```

### Composer Authentication

First setup Magento Marketplace authentication (details in the [DevDocs](http://devdocs.magento.com/guides/v2.0/install-gde/prereq/connect-auth.html)).

Copy `src/auth.json.sample` to `src/auth.json`. Then, update the username and password values with your Magento public and private keys, respectively. Finally, copy the file to the container by running `bin/copytocontainer auth.json`.

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

For more information about Redis usage with Magento, <a href="https://devdocs.magento.com/guides/v2.3/config-guide/redis/redis-session.html" target="_blank">see the DevDocs</a>.


### Xdebug & PHPStorm
>not tested yet

1.  First, install the [Chrome Xdebug helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc). After installed, right click on the Chrome icon for it and go to Options. Under IDE Key, select PHPStorm from the list and click Save.

2.  Next, enable Xdebug in the PHP-FPM container by running: `bin/xdebug enable`, the restart the docker containers (CTRL+C then `bin/start`).

3.  Then, open `PHPStorm > Preferences > Languages & Frameworks > PHP` and configure:

    * `CLI Interpreter`
        * Create a new interpreter and specify `From Docker`, and name it `mage2click/magento-php:7-2-fpm-mailhog`.
        * Choose `Docker`, then select the `mage2click/magento-php:7-2-fpm-mailhog` image name, and set the `PHP Executable` to `php`.

    * `Path mappings`
        * Don't do anything here as the next `Docker container` step will automatically setup a path mapping from `/var/www/html` to `./src`.

    * `Docker container`
        * Remove any pre-existing volume bindings.
        * Ensure a volume binding has been setup for Container path of `/var/www/html` mapped to the Host path of `./src`.

4. Open `PHPStorm > Preferences > Languages & Frameworks > PHP > Debug` and set Debug Port to `9001`.

5. Open `PHPStorm > Preferences > Languages & Frameworks > PHP > DBGp Proxy` and set Port to `9001`.

6. Open `PHPStorm > Preferences > Languages & Frameworks > PHP > Servers` and create a new server:

    * Set Name and Host to your domain name (ex. `magento2.test`)
    * Keep port set to `80`
    * Check the Path Mappings box and map `src` to the absolute path of `/var/www/html`

7. Go to `Run > Edit Configurations` and create a new `PHP Remote Debug` configuration by clicking the plus sign and selecting it. Set the Name to your domain (ex. `magento2.test`). Check the `Filter debug connection by IDE key` checkbox, select the server you just setup, and under IDE Key enter `PHPSTORM`. This IDE Key should match the IDE Key set by the Chrome Xdebug Helper. Then click OK to finish setting up the remote debugger in PHPStorm.

8. Open up `src/pub/index.php`, and set a breakpoint near the end of the file. Go to `Run > Debug 'magento2.test'`, and open up a web browser. Ensure the Chrome Xdebug helper is enabled by clicking on it > Debug. Navigate to your Magento store URL, and Xdebug within PHPStorm should now trigger the debugger and pause at the toggled breakpoint.

## Credits

### Mark Shust

<a href="https://u.magento.com/certification/directory/dev/883/" target="_blank">Certified Magento Developer & Architect</a> and <a href="http://www.zend.com/en/yellow-pages/ZEND014633" target="_blank">Zend Certified Engineer</a>, and available for consulting & development of your next project 🤓. You can read technical articles on my blog at <a href="https://markshust.com" target="_blank">markshust.com</a> or contact me directly at <a href="mailto:mark@shust.com">mark@shust.com</a>.  
<a href="https://courses.markshust.com/p/setup-magento-2-development-environment-docker" target="_blank">Mark Shust's Free Course about Setup a Magento 2 Development Environment with Docker</a>

### Nexcess

A special thanks goes out to <a href="https://www.nexcess.net/" target="_blank">Nexcess</a> for hosting <a href="http://pubfiles.nexcess.net/magento/ce-packages/" target="_blank">public archives of every version of Magento</a> 💙. I've used their Magento hosting services in the past also (both <a href="https://www.nexcess.net/magento/hosting/" target="_blank">shared</a> and <a href="https://www.nexcess.net/magento/enterprise-hosting/" target="_blank">enteprise</a> offerings) and they're great, ...highly recommended!

### Willem Wigman
Implemented Varnish support with https proxy <a href="https://github.com/wigman" target="_blank">Willem Wigman</a>

### Max Uroda
<a href="https://u.magento.com/certification/directory/dev/1122780/" target="_blank">Certified Magento Developer (M1 Developer Plus)</a>, WebDeveloper interested in Magento/Magento2, Docker, JS, Varnish, PWA  
<a href="https://twitter.com/u_maxx" target="_blank">@u_maxx</a>  
<a href="https://maxuroda.pro" target="_blank">maxuroda.pro</a> 

### Dmitry Shkoliar
<a href="https://www.zend.com/en/yellow-pages/ZEND026786" target="_blank">Zend Certified PHP Engineer</a>, Magento2, Docker, PWA, Varnish, JS, HTML5, Mobile, iOS, Android  
<a href="https://twitter.com/shkoliar" target="_blank">@shkoliar</a>  
<a href="https://shkoliar.com" target="_blank">shkoliar.com</a>  


## License

[MIT](https://github.com/mage2click/docker-magento-mutagen/blob/master/LICENSE.md)

## TBD 
- Easy switch between using or not using Varnish - currently you can use fully automated Varnish setup from our [feature/develop-varnish](https://github.com/mage2click/docker-magento-mutagen/tree/feature/develop-varnish) branch
- n98-magerun2 tool installed out of the box  

feel free to create new GitHub issue with feature request :) 
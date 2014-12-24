# How to get it running

DockerFlow will create the necessary Docker containers to easily start your TYPO3 Flow/Neos distribution.
The package provides a wrapper script in `bin/fig` to simplify the handling of docker and basic configurations
optimized for TYPO3 Neos.

## Install docker

    https://docs.docker.com/installation/

## Install fig

    http://www.fig.sh/install.html

## With a Mac or Windows install boot2docker

    http://boot2docker.io/

## Install Flow or Neos into the distribution folder

## Run it in the background

    `bin/fig up -d`
    
The command will echo the url with which you can access your project.
The default database credentials for Flow are:

    TYPO3:
      Flow:
        persistence:
          backendOptions:
            dbname: neos
            user: root
            password: ''
            host: db
            driver: pdo_mysql

## Check the status

    `bin/fig ps`

This will show the running containers. The `data` container can be inactive to work.

# Tipps & Tricks

## Using different FLOW_CONTEXT

    `FLOW_CONTEXT=Production bin/fig up -d`

## Running a shell in one of the service containers

    `bin/fig run SERVICE /bin/bash`
    
SERVICE can currently be `app`, `web`, `data` or `db`.

## Keep Flow cache in the container to improve performance (especially with boot2docker)

Add this setting to your Flow `Settings.yaml`

    TYPO3:
      Flow:
        utility:
          environment:
            temporaryDirectoryBase: /tmp/dockerflow/Temporary/

## Check open ports in a container

    `bin/fig run SERVICE netstat --listen`

# Further reading

* blog post on php-fpm - http://mattiasgeniar.be/2014/04/09/a-better-way-to-run-php-fpm/
* nginx+php-fpm+mysql tutorial - http://www.lonelycoder.be/nginx-php-fpm-mysql-phpmyadmin-on-ubuntu-12-04/
* Docker documentation - http://docs.docker.com/reference/builder/
* fig configuration for another docker Neos project - https://github.com/million12/docker-typo3-neos/blob/master/fig.yml
* fig documentation - http://www.fig.sh/yml.html
* nginx.conf for FLow - https://gist.github.com/iwyg/4c8c0c0dec21dcfc8969
* boot2docker version which supports nfs - https://vagrantcloud.com/yungsang/boxes/boot2docker
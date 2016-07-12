---
layout: post
title: "Ansible DB Deployment Outline"
date: 2016-07-11 03:46:49 +0000
comments: true
categories: [ansible, mysql]
---
### Outline
* Installing and Configuring a MariaDB Server (master)
* The installation will be done with the ansible user
* The installation needs to be done with sudo privileges
* The connection used is ssh
* gathering of facts needs to be on

### What do we need to know?
* the package name f the Db server
* the group/host of the master server
* the directory for installing the db(if not default)
* the version of the db
* the distribution it is installed on

### What needs to be done/installed
* install the MariaDB server and utilities
* root password install
    - waitfor the db service to be started
      - takes place manually after the mysql-secure-installation run
* install the mysql/mariadb configuration file ( if needed)
* copy the mysql/mariadb database backup to the home directory
* import the database(s)
* add a cron job for nightly backups

### Testing the db
run a MYSQL command and register the output as JSON format to determine success


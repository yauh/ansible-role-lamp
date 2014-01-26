LAMP
=====

This role installs and configures a complete LAMP stack on Debian based systems.

Requirements
------------

This role requires Ansible 1.4 or higher and platform requirements are listed in the metadata file.

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows.

MySQL users and databases are created based on variables, just add all users, dbs, and privileges in the variables. However you cannot define hosts for the time being.

	lamp:
	  admin_email: mail@example.org    # the admin email used by apache
	  apache:
	    port: 80                       # port for apache sites to be served on
	    root: /var/www/                # root directory for web sites
	    modules:                       # list of apache modules to be installed
	        - alias
	        - auth_basic
	        - autoindex
	        - deflate
	        - dir
	        - env
	        - expires
	        - php5
	        - rewrite
	        - setenvif
	        - status
	        - vhost_alias
	  php:                             # various options for PHP running inside apache (php.ini)
	    php_version: 5
	    max_execution_time: 30
	    max_input_time: 60
	    memory_limit: 128M
	    upload_max_filesize: 8M
	    allow_url_fopen: On
	    allow_url_include: Off
	    session_cookie_httponly: 1
	    display_errors: Off
	    error_reporting: E_ALL & ~E_NOTICE & ~E_STRICT & ~E_DEPRECATED
	  mysql:
	    root_password: password         # root password for mysql
		users:                          # users and databases to be created
	        - name: ci
	          password: password
	          privs: "cidb.*:ALL"

Examples
========

Set up complete lamp stack only on lamp hosts

	- hosts: lamp
	  sudo: True
	  roles:
	     - { role: role-lamp, tags: lamp}


Dependencies
------------

None

License
-------

BSD

Author Information
------------------

Stephan Hochhaus <stephan@yauh.de>

[yauh.de](http://yauh.de)



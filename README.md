# PHP Development Docker Image

This image is aimed to help developers which need to develop and test their projects in different PHP versions
(specially free or open source software developers). It comes with the latest supported PHP versions plus the latest
5.3 release.

The following PHP versions are available:

- 5.6.4
- 5.5.20
- 5.4.36
- 5.3.29

This container also ships with Nginx, which integrates to the right PHP-FPM version.


## Usage

Start the container:

    $ docker run -p 80:80 -v ~/your-app:/var/www/your-app -d "eriksencosta/php-dev:latest"

This will expose your application through port 80, which you can then access in your web browser with the address `http://localhost` (or an IP address if you're using Boot2Docker).

Starting your container in this way will run your application with the latest released PHP version and will output
the Nginx access logs.

To get the real value of the image and switch between the different PHP versions, start the container in interactive
mode:

    $ docker run -t -i -p 80:80 -v ~/your-app:/var/www "eriksencosta/php-dev:latest" /bin/bash

Use the `phpenv` command to switch between the installed PHP versions:

    # phpenv versions
      5.3
      5.3.29
      5.4
      5.4.35
      5.5
      5.5.19
      5.6
    * 5.6.3 (set by /opt/phpenv/version)

5.6, 5.5, 5.4 and 5.3 are just shortcuts. `phpenv` let you define the global (system-wide) and local PHP version. To
set it globally:

    # phpenv global 5.5

To set a local version, use:

    # phpenv local 5.4

To install additional PHP libraries globally with Composer:

    # composer global require fabpot/php-cs-fixer:dev-master

You can start the Nginx and PHP-FPM services using the helper command `webserver`:

    # webserver start
    Starting PHP-FPM server.
    Starting Nginx server.
    Done.

The Zend OPCache is enabled by default. If you want to disable it, you can run the helper command `opcache`:

    # opcache disable
    The Zend OPCache was disabled.

    You need to restart the webserver for the changes to take effect.
    Execute: webserver restart

**Note:** check the [Silex Docker Example][#github-silex-docker] application for further usage examples.


## PHP Information

After starting the container, access `http://localhost/info.php` (or an IP address if you're using Boot2Docker).


### PHP-FPM

PHP-FPM is installed for each PHP version. To start it with Nginx, use the helper command `webserver`. See the Usage
section.


### PHP Extensions

Each PHP version is built with the following extensions:

- amqp
- bcmath
- Core
- ctype
- curl
- date
- dom
- ereg
- exif
- fileinfo
- filter
- ftp
- gd
- hash
- iconv
- igbinary
- intl
- json
- libxml
- mbstring
- mcrypt
- memcached
- mongo
- mysql
- mysqli
- mysqlnd
- openssl
- pcntl
- pcre
- PDO
- pdo_mysql
- pdo_pgsql
- pdo_sqlite
- Phar
- posix
- readline
- Reflection
- riak
- session
- shmop
- SimpleXML
- soap
- sockets
- SPL
- sqlite3
- standard
- sysvsem
- sysvshm
- tidy
- tokenizer
- xdebug
- xml
- xmlreader
- xmlrpc
- xmlwriter
- xsl
- Zend OPcache
- zip
- zlib

From the previous list, the following extensions were installed using PECL:

- [amqp][#php-amqp]
- [igbinary][#php-igbinary]
- [memcached][#php-memcached]
- [mongo][#php-mongo]
- [riak][#php-riak]
- [xdebug][#php-xdebug]
- [Zend OPcache][#php-opcache] (PHP < 5.5)


### Composer

Composer is also installed. The following libraries are installed globally:

- [Behat][#behat]
- [PHP Coding Standards Fixer][#php-cs-fixer]
- [PHP_Depend][#phpdepend]
- [PHPLOC][#phploc]
- [PHPMD][#phpmd]
- [PHPUnit][#phpunit]
- [PHPCPD][#phpcpd]
- [PHP_CodeSniffer][#phpcodesniffer]
- [phpDox][#phpdox]


## Additional Information

The image is built using Ansible. The playbook used is the [Ansible PHP Development][#ansible-php-dev].


## License

Apache License 2.0


[#github-silex-docker]: https://github.com/eriksencosta/silex-docker-example
[#php-amqp]: http://pecl.php.net/package/amqp
[#php-igbinary]: http://pecl.php.net/package/igbinary
[#php-memcached]: http://pecl.php.net/package/memcached
[#php-mongo]: http://pecl.php.net/package/mongo
[#php-riak]: http://pecl.php.net/package/riak
[#php-xdebug]: http://pecl.php.net/package/xdebug
[#php-opcache]: http://pecl.php.net/package/ZendOpcache
[#behat]: http://behat.org
[#php-cs-fixer]: http://cs.sensiolabs.org
[#phpdepend]: http://pdepend.org
[#phploc]: https://github.com/sebastianbergmann/phploc
[#phpmd]: http://phpmd.org
[#phpunit]: https://phpunit.de
[#phpcpd]: https://github.com/sebastianbergmann/phpcpd
[#phpcodesniffer]: https://github.com/squizlabs/PHP_CodeSniffer
[#phpdox]: http://phpdox.de
[#ansible-php-dev]: https://github.com/eriksencosta/ansible-php-dev

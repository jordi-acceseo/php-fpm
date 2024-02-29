<div align="center">
    <a href="https://www.acceseo.com">
        <img
            alt="acceseo logo"
            src="https://www.acceseo.com/wp-content/uploads/2019/09/logoAcceseo-2.svg"
            width="150">
    </a>
</div>

<h1 align="center">PHP-FPM</h1>
<div align="center">
    <a href="https://hub.docker.com/r/acceseo/php-fpm"><img src="https://img.shields.io/docker/pulls/acceseo/php-fpm.svg" alt="Docker pulls"></a>
    <br><br>
    <a href="https://github.com/acceseo/php-fpm/tree/main/README.md">Spanish version</a> | <a href="https://hub.docker.com/r/acceseo/php-fpm">Docker Hub</a>
</div>

<hr>

Image based on the official PHP image in its FPM implementation.

## 🧰 Currently supported versions
* 7.2
* 7.3
* 7.4
* 8.0
* 8.1
* 8.2
* 8.3

*It's possible to use a specific version based on [semver](https://semver.org/). For example acceseo/php-fpm:8.1-1.0.0.*

## 🔨 What's in the image
* [composer](https://getcomposer.org/)
* [wp cli](https://wp-cli.org/)
<details>

<summary>PHP Extensions</summary>

```
[PHP Modules]
Core
ctype
curl
date
dom
exif
fileinfo
filter
ftp (PHP <=8.1)
gd
hash
iconv
intl
json
libxml
mbstring
mysqli
mysqlnd
openssl
pcre
PDO
pdo_mysql
pdo_pgsql
pdo_sqlite
pgsql
Phar
posix
random (PHP >= 8.2)
readline
Reflection
session
SimpleXML
sodium
SPL
sqlite3
standard
tokenizer
xdebug
xml
xmlreader
xmlwriter
zip
zlib

[Zend Modules]
Xdebug
```
</details>

## 📃 Configurable parameters
* Upload max size:
  `PHP_UPLOAD_MAX_FILESIZE=32M`
* Post max size:
  `PHP_POST_MAX_SIZE=32M`
* Max input vars:
  `PHP_MAX_INPUT_VARS=50000`
* Memory limit:
  `PHP_MEMORY_LIMIT=128M`
* Max execution time:
  `PHP_MAX_EXECUTION_TIME=30`
* Max input time:
  `PHP_MAX_INPUT_TIME=60`
* Time zone:
  `TZ=Europe/Madrid`
* WORKDIR:
  `PHP_APP_DIRECTORY=/app`
* Change the Xdebug mode:
  `XDEBUG_MODE=off`

## 🕹️ Use case (with a docker-compose.yml config file) 
  ```yaml
    version: '3'
    services:
      httpd.local:
        image: acceseo/httpd
        volumes:
          - .:/app
        ports:
          - 80:80
          - 443:443
      php.local:
        image: acceseo/php-fpm:8.3
        volumes:
          - .:/app
      #...
  ```

## 👷 Credits
* Made by [acceseo](https://acceseo.com)

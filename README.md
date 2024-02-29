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
    <a href="https://github.com/acceseo/php-fpm/tree/main/README.en.md">English version</a> | <a href="https://hub.docker.com/r/acceseo/php-fpm">Docker Hub</a>
</div>

<hr>

Imagen que tiene como base la oficial de PHP en su implementación FPM.

## 🧰 Versiones actualmente soportadas
* 7.2
* 7.3
* 7.4
* 8.0
* 8.1
* 8.2
* 8.3

*Es posible utilizar una versión con formato [semver](https://semver.org/). Por ejemplo acceseo/php-fpm:8.1-1.0.0.*

## 🔨 Qué contiene la imagen
* [composer](https://getcomposer.org/)
* [wp cli](https://wp-cli.org/)
<details>

<summary>Extensiones PHP</summary>

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

## 📃 Parámetros de la imagen configurables
* Tamaño máximo de subida de un archivo:
  `PHP_UPLOAD_MAX_FILESIZE=32M`
* Tamaño máximo del cuerpo POST:
  `PHP_POST_MAX_SIZE=32M`
* Cantidad de variables de entrada máximas:
  `PHP_MAX_INPUT_VARS=50000`
* Límite de memoria de ejecución:
  `PHP_MEMORY_LIMIT=128M`
* Tiempo máximo de ejecución:
  `PHP_MAX_EXECUTION_TIME=30`
* Tiempo máximo de lectura de datos de entrada:
  `PHP_MAX_INPUT_TIME=60`
* Cambiar la zona horaria:
  `TZ=Europe/Madrid`
* Modificar el WORKDIR de la imagen:
  `PHP_APP_DIRECTORY=/app`
* Selección del modo de Xdebug:
  `XDEBUG_MODE=off`

## 🕹️ Ejemplo de uso (archivo de configuración docker-compose.yml) 
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

## 👷 Créditos
* Creado por [acceseo](https://acceseo.com)

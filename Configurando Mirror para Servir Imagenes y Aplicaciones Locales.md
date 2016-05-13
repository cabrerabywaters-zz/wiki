# Por qué quiero un Mirror #

Los mirrors se utilizan para poder acceder a la información de múltiples repositorios a lo largo de internet por medio de una sola máquina local. Esto permite que todos los repositorios se descarguen directamente desde Internet con una máquina y todas las otras máquinas podrán acceder a esta a través de la red local para descargar nuevos paquetes.

# Instalación #

## Node JS y NPM ##

En primer lugar, debemos asegurarnos de instalar NODEJs en la máquina 

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Luego, deberemos instalar otras herramientas de desarrollo.

```
sudo apt-get install -y build-essential
```

Y finalmente, instalamos NPM

```
sudo npm install npm -g
``` 

## Instalando NPM Mirror ##

Ahora, deberemos instalar el paquete local-npm para levantar el servidor que hará de mirror

```
npm install -g local-npm
```

### Crear carpeta para guardar los packetes ###
Una vez instalado deberemos crear una carpeta en la cual se guardaran los paquetes a instalar. La ubicación de la carpet dependerá de dónde en la máquina queremos guardar los archivos.

```
mkdir /var/node_repositories
```

Luego debemos ingresar en ella.

```
cd /var/node_repositories
```

Y correr el comando

```
local-npm --url-base http://192.168.x.x:5080
```

Donde 192.168.x.x es la dirección IP privada que los demás servidores deberán acceder para instalar los paquetes de NPM

# Configurar la máquina Privada #

Finalmente, en la máquina privada que debe acceder a nuestro mirror, debemos correr el siguiente comando

```
npm set registry http://192.168.x.x:5080
``` 

# Instalando Satis para Composer #

Satis es una herramienta que nos permite realizar un mirror local de nuestros packages que generalmente se instalan a traves de composer. Para poder configurarlo correctamente, nuestra maquina necesitara tener instalado composer.
Para eso crearemos una carpeta en la cual queramos instalar el proyecto y correremos el siguiente comando dentro de ella

```
#!bash
curl -sS https://getcomposer.org/installer | php

```

Posteriormente, debemos instalar Satis.


```
#!bash

php composer.phar create-project composer/satis --stability=dev --keep-vcs 
```

Una vez instalado Satis podemos crear el archivo de configuracion que nos permitira descargar los packages que queraramos compartir a traves de mirror.


```
#!bash

{
    "name": "Sonda Mirror",
    "homepage": "http://localhost:4680",
 
    "repositories": [
        { "type": "vcs", "url": "https://github.com/SynetoNet/monolog" },
        { "type": "composer", "url": "https://packagist.org" }
    ],
 
    "require": {
        "monolog/monolog": "syneto-dev",
        "mockery/mockery": "*",
        "phpunit/phpunit": "*"
    },
    "require-dependencies": true
}
```

Una vez creada esta configuracion debemos decirle a Satis que genere los mirrors correspondientes mediante el comando


```
#!bash

php ./satis/bin/satis build ./mirrored_packages.conf ./packages-mirror

```

Finalmente, podemos correr un servidor en PHP para poder servir los paquetes recientemente instalados.


```
#!bash

php -S localhost:4680 -t ./packages-mirror/
```

# Configurando un Mirror para Ubuntu #

En primer lugar, debemos instalar aptmirror para poder crear el mirror de ubuntu


```
#!bash

sudo aptitude install apt-mirror
```

Para poder servir los repositorios de manera local deberemos configurar apache en la maquina


```
#!bash

sudo aptitude install apache2
```

El archivo de configuracion de aptmirror se encuentra en 

```
#!bash

/etc/apt/mirror.list
```

Luego, para comenzar a descargar los paquetes debemos utilizar el comando


```
#!bash
apt-mirror

```

Finalmente, debemos configurar apache para servir los paquetes desde el nuevo repositorio


```
#!bash

cd /var/www/
sudo ln -s /media/STORAGE/mirror/us.archive.ubuntu.com/ubuntu/ ubuntu
```

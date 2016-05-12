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
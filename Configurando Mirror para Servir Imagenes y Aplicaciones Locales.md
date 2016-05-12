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

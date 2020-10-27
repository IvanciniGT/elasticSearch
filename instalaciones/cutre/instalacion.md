# Paso 1: Preparación del entorno:
Consiste en algunas configuraciones que necesitamos hacer en el SO del host (ubuntu)
## DESACTIVAR SWAPPING
Usar el HDD como si fuera RAM: 
    Ventajas: Acceso a más "RAM"
    Inconvenientes: Lentitud extrema HDD es muyyyyy lento comparado con la RAM
    $ free
    $ sudo swapoff -a # TRAMPA! Cambio temporal
    ¢ sudo vim /etc/fstab
      Como usuario ROOT
           EDITOR  

## Aumentar número maximo de ficheros que podemos tener abiertos simultaneamente
sudo su -
ulimit -n 65535
exit

# Aumentar memoria virtual
sudo su -
sysctl -w vm.max_map_count=262144
exit

# Paso 2: Instalar un contenedor con elastic:
docker run -d --name MI_ELASTIC -p 8080:9200 -e "discovery.type=single-node" elasticsearch:7.9.3

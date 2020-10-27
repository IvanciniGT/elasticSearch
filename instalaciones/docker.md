# Comandos de docker

## Imágenes

Una **imagen** es un archivo que contiene __todo lo necesario__ para ejecutar
un programa o conjunto de programas. 

### Saber que imágenes tengo disponibles en mi ordenador

docker image list
(Equivalente: docker images)

### Borrar una imagen

docker image rm <id>
(Equivalente: docker rmi <id>)

### Borrar todas las imágenes
docker rmi $(docker image list -q)

### Descargar una imagen de Internet
Muchísimas empresas suben imágenes de su software a una página que se llama hub.docker.com
Podemos descargar imágenes desde esa página web

docker pull <nombre de la imagen>:<version>

## Contenedores
Las imágenes, debemos "instalarlas" para convertrlas a un CONTENEDOR, que es lo que realmente
podemos ejecutar en nuestro ordenador.

### Generar un contenedor desde una imagen
docker container create <nombre de la imagen>:<version>
    Nota: Si creamos un contenedor sin ponerle un nombre, docker le asigna uno aleatorio

A este comando le vamos a dar MUCHOS PARAMETROS en realidad:
docker container create <PARAMETROS> <nombre de la imagen>:<version>
    --name <nombre del contenedor>
    

### Listar todos los contenedores que tengo en mi ordenador QUE SE ESTAN EJECUTANDO
docker container list
(equivalente: docker ps)

### Listar todos los contenedores que tengo en mi ordenador INDEPENDIENTEMENTE DE SU ESTADO DE EJECUCION
docker container list --all
(equivalente: docker ps --all)

### Para arrancar un contenedor 
docker start <nombre contenedor>
 
### Para parar un contenedor 
docker stop <nombre contenedor>

### Para reiniciar un contenedor 
docker restart <nombre contenedor>

### Borrar un contenedor
docker container rm <nombre del contenedor>
(Equivalente: docker rm <nombre del contenedor>)

### Descargar una imagen, crear un contenedor y arrancarlo TODO EN UNO 
docker run -d --name <nombre del contenedor> <nombre de la imagen>:<version>
    El parametro -d, no muestra el log
    
### Para sacar el log de un programa corriendo en un contenedor
docker logs <nombre del contenedor>

### Para ejecutar un comando dentro de un contenedor
docker exec <PARAMETROS> <nombre del contenedor> <comando que quiero ejecutar>
Entre los parametros el más importantes es:
 -it <--- terminal interactiva
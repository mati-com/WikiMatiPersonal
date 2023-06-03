---
title: Docker 🐳
publishDate: 02 Jun 2023
description: Introducción a docker, instalación y uso básicos.
---
<img src="/public/assets/blog/docker.gif" alt= "gif del logo de docker" width="500px" height="500px" style="display: block; margin: 0 auto;">

[Docker](https://www.docker.com/) es una herramienta que permite empaquetar y ejecutar aplicaciones de forma aislada en contenedores. Es como una caja virtual que contiene todo lo necesario para que una aplicación funcione correctamente, incluyendo el código, las bibliotecas y las dependencias.

## <a name="top"></a> Tabla de Contenido

- [Introducción a Docker](#introducción-a-docker)
  - [Ventajas de usar docker](#ventajas-de-usar-docker)
  - [Conceptos clave de docker](#conceptos-clave-de-docker)
- [ Requisitos de Docker](#-requisitos-de-docker)
- [ Comandos de imágenes](#-comandos-de-imágenes)
- [ Comandos de contenedores](#-comandos-de-contenedores)
- [ Conectándose a los contenedores](#-conectándose-a-los-contenedores)
- [ Docker Compose](#-docker-compose)
  - [Introducción a Docker Compose](#introducción-a-docker-compose)
- [ Volúmenes en Docker](#-volúmenes-en-docker)
  - [Conceptos](#conceptos)
    - [Conceptos de volúmenes en Docker:](#conceptos-de-volúmenes-en-docker)
    - [Creación y  gestión de volúmenes:](#creación-y--gestión-de-volúmenes)
    - [Uso de de volúmenes para persistencia de datos:](#uso-de-de-volúmenes-para-persistencia-de-datos)
- [ Ambientes y hot reload:](#-ambientes-y-hot-reload)
    - [Configuración de variables de entorno en contenedores:](#configuración-de-variables-de-entorno-en-contenedores)

---

# <a name="iad"></a>Introducción a Docker

## Ventajas de usar docker

- Portabilidad: las aplicaciones se pueden ejecutar de forma consistente en diferentes entornos.
- Aislamiento: las aplicaciones se ejecutan de manera independiente y segura.
- Eficiencia en recursos: los contenedores son más ligeros y rápidos de iniciar y detener.
- Escalabilidad: facilita manejar un mayor volumen de tráfico de forma eficiente.
- Facilidad de uso: ofrece una interfaz fácil de usar y simplifica el desarrollo y despliegue de aplicaciones.

## Conceptos clave de docker

- Imagen: Una imagen de Docker es un paquete que contiene todo lo necesario para ejecutar una aplicación, incluyendo el código, las bibliotecas y las dependencias. Se utiliza como plantilla para crear contenedores.

- Contenedor: Un contenedor de Docker es una instancia en ejecución de una imagen. Es un entorno aislado y liviano que ejecuta la aplicación de manera consistente en diferentes entornos.

- Dockerfile: Un Dockerfile es un archivo de texto que contiene las instrucciones para construir una imagen de Docker. Define cómo se configurará y ejecutará el contenedor.

- Registro: Un registro de Docker es un repositorio donde se almacenan y comparten las imágenes de Docker. Docker Hub es el registro público más utilizado, pero también se pueden utilizar registros privados.

- Orquestación: La orquestación en Docker se refiere a la administración de múltiples contenedores y su escalabilidad. Docker Swarm y Kubernetes son herramientas populares para orquestar y administrar contenedores a gran escala.

- Volumen: Un volumen de Docker es una forma de persistir y compartir datos entre contenedores y el sistema host. Permite almacenar datos de manera persistente incluso cuando un contenedor se detiene o se destruye.

- Red: Docker proporciona funcionalidad de red para conectar contenedores y permitir la comunicación entre ellos y con el mundo exterior. Se pueden crear redes personalizadas para aislar y asegurar los contenedores.

Estos conceptos son fundamentales para comprender y utilizar Docker de manera efectiva en el desarrollo y despliegue de aplicaciones

---

# <a name="rdd"></a> Requisitos de Docker

Los requisitos del sistema para Docker pueden variar ligeramente según el sistema operativo en el que se instale.

- Sistema operativo: Docker es compatible con una amplia gama de sistemas operativos, incluyendo Windows, macOS y varias distribuciones de Linux, como Ubuntu, CentOS y Debian. Es importante verificar la compatibilidad específica según el sistema operativo que estés utilizando.
- Procesador: Se recomienda un procesador de 64 bits para ejecutar Docker de manera óptima.
- Memoria RAM: Docker requiere una cantidad mínima de memoria RAM para funcionar correctamente. Se recomienda al menos 2 GB de RAM, aunque es posible que algunas aplicaciones o contenedores requieran más recursos.
- Espacio en disco: Debes asegurarte de tener suficiente espacio en disco para las imágenes de Docker, los contenedores y los volúmenes de datos. Se recomienda tener al menos 20 GB de espacio libre para un uso básico de Docker.
- Virtualización: Docker utiliza la virtualización a nivel de sistema operativo para crear y ejecutar contenedores. En sistemas Windows y macOS, Docker Desktop utiliza la virtualización de Hyper-V (Windows) o la virtualización de Apple (macOS). Asegúrate de que tu sistema admita y tenga habilitada la virtualización en el BIOS o la configuración del sistema.

---

# <a name="cdi"></a> Comandos de imágenes

1. Construcción de imágenes Docker

   - **docker build -t nombre_imagen ruta_dockerfile** _:Construye una imagen de Docker a partir de un Dockerfile ubicado en la ruta especificada._

2. Descarga de imágenes desde Docker Hub

   - **docker pull nombre_imagen:tag** _:Descarga una imagen específica desde Docker Hub. Puedes especificar una etiqueta (tag) para obtener una versión específica de la imagen. Si no se especifica una etiqueta, se descargará la última versión por defecto._

3. Listado y gestión de imágenes

   - **docker images** _:Lista todas las imágenes de Docker disponibles en tu sistema._
   - **docker rmi nombre_imagen** _:Elimina una imagen específica de Docker. Asegúrate de no tener ningún contenedor en ejecución basado en esa imagen antes de eliminarla._

4. Eliminación de imágenes

   - **docker rmi nombre_imagen** _:Elimina una imagen específica de Docker. Asegúrate de no tener ningún contenedor en ejecución basado en esa imagen antes de eliminarla._
   - **docker image prune** _:Elimina todas las imágenes sin utilizar, liberando espacio en disco. Ten en cuenta que esto eliminará todas las imágenes que no estén siendo utilizadas por ningún contenedor._

---

# <a name="cdc"></a> Comandos de contenedores

1. Creación y ejecución de contenedores

   - **docker run nombre_imagen** _:Crea y ejecuta un contenedor basado en una imagen específica._
   - **docker run -d nombre_imagen** _:Crea y ejecuta un contenedor en segundo plano (modo "detach")._
   - **docker run -p puerto_host:puerto_contenedor nombre_imagen** _:Asocia un puerto del host al puerto del contenedor al crear y ejecutar un contenedor._

2. Listado y gestión de contenedores en ejecución

   - **docker ps** _:Lista todos los contenedores en ejecución._
   - **docker ps -a** _:Lista todos los contenedores, tanto en ejecución como detenidos._
   - **docker inspect ID_contenedor** _:Muestra información detallada de un contenedor específico._
   - **docker logs ID_contenedor** _:Muestra los registros (logs) de un contenedor específico._

3. Detención y eliminación de contenedores

   - **docker stop ID_contenedor** _:Detiene un contenedor en ejecución de forma suave (envía una señal de apagado)._
   - **docker kill ID_contenedor** _:Detiene un contenedor en ejecución de forma inmediata (envía una señal de finalización)._
   - **docker rm ID_contenedor** _:Elimina un contenedor específico. Asegúrate de detenerlo antes de eliminarlo._

4. Reinicio y pausa de contenedores
   - **docker restart ID_contenedor** _:Reinicia un contenedor en ejecución._
   - **docker pause ID_contenedor** _:Pausa la ejecución de un contenedor._
   - **docker unpause ID_contenedor** _:Reanuda la ejecución de un contenedor pausado._

---

# <a name="calc"></a> Conectándose a los contenedores

1. Conectarse a un contenedor

   - **docker exec -it ID_contenedor comando** _:Conéctate a un contenedor en ejecución y ejecuta un comando en su interior. Por ejemplo, **`docker exec -it mi_contenedor`** bash abre un terminal interactivo dentro del contenedor llamado "mi_contenedor"._

2. Acceso a unterminal interactivo dentro de un contenedor

   - **docker exec -it ID_contenedor bash** _:Accede a un terminal interactivo dentro de un contenedor en ejecución utilizando el shell "bash". Puedes reemplazar "bash" por otro shell como "sh" o "zsh", dependiendo de la configuración del contenedor._

3. Copia de archivos dentro y fuera de los contenedores

   - Copiar desde el sistema host al contenedor: 
     **docker cp archivo origen ID_contenedor:destino** _:Copia un archivo desde el sistema host al contenedor. Por ejemplo, **`docker cp archivo txt mi_contenedor:/ruta/destino`** copia el archivo "archivo.txt" al contenedor "mi_contenedor" en la ruta "/ruta/destino"._
   - Copiar desde el contenedor al sistema host:
     **docker cp ID_contenedor:archivo origen destino** _:Copia un archivo desde el contenedor al sistema host. Por ejemplo, **`docker cp mi_contenedor:/ruta/archivo.txt /ruta/destino`** copia el archivo "archivo.txt" del contenedor "mi_contenedor" a la ruta "/ruta/destino" en el sistema host._

4. Redirección de puertos para acceder a servicios dentro de los contenedores:
   - **docker run -p puerto_host:puerto_contenedor nombre_imagen** _:Redirige un puerto del sistema host al puerto del contenedor al crear y ejecutar un contenedor, como se mencionó anteriormente._

---

# <a name="dc"></a> Docker Compose

## Introducción a Docker Compose
[Docker Compose](https://docs.docker.com/compose/) es una herramienta que simplifica la gestión de aplicaciones multi-contenedor. Permite definir y ejecutar servicios relacionados en un archivo YAML, coordinando su configuración y creación. Con Docker Compose, puedes manejar fácilmente aplicaciones complejas basadas en contenedores Docker.

---

# <a name=""></a> Volúmenes en Docker

## Conceptos
Los volúmenes en Docker son un mecanismo que permite persistir y compartir datos entre contenedores y el sistema host. Proporcionan un medio para almacenar información de manera duradera y acceder a ella incluso después de que un contenedor se haya detenido o eliminado.

### Conceptos de volúmenes en Docker:
  - Los volúmenes en Docker son directorios o carpetas especiales que existen fuera del sistema de archivos del contenedor y se gestionan por Docker.
  - Los volúmenes pueden ser utilizados para compartir datos entre múltiples contenedores, respaldar información importante o permitir que los contenedores accedan a archivos del sistema host.
  - Los volúmenes son independientes del ciclo de vida de los contenedores, lo que significa que persisten incluso si el contenedor que los utiliza se detiene o se elimina.

### Creación y  gestión de volúmenes:
   - Puedes crear un volumen utilizando el siguiente comando de Docker: **`docker volume create nombre_volumen`**
   - Para listar los volúmenes disponibles en tu sistema, puedes utilizar el siguiente comando: **`docker volume ls`**
   - También puedes eliminar un volumen con el siguiente comando: **`docker volume rm nombre_volumen`**
   - Para utilizar un volumen en un contenedor, debes especificar el volumen en el momento de ejecutar el contenedor, utilizando la opción `-v` o `--volume`: **`docker run -v nombre_volumen:ruta_contenedor nombre_imagen`**

### Uso de de volúmenes para persistencia de datos:
   - Los volúmenes son útiles para la persistencia de datos, ya que permiten que los datos se mantengan incluso después de que los contenedores se detengan o se eliminen.
   - Al montar un volumen en un contenedor, cualquier cambio realizado en los datos dentro del volumen será persistido.
   - Puedes utilizar volúmenes para almacenar bases de datos, archivos de configuración, registros y otros datos que necesiten persistencia.
 
Al utilizar volúmenes en Docker, puedes asegurarte de que los datos importantes se mantengan seguros y accesibles a través de contenedores y reinicios de contenedor. Además, los volúmenes facilitan la compartición de información entre contenedores y el sistema host.

---

# <a name=""></a> Ambientes y hot reload:

- En el desarrollo de aplicaciones, los ambientes se refieren a diferentes configuraciones y variables utilizadas en diferentes etapas del ciclo de vida de una aplicación, como desarrollo, pruebas y producción.
- El hot reload es una funcionalidad que permite a los desarrolladores realizar cambios en el código de su aplicación en tiempo real, sin tener que reiniciarla por completo. Esto acelera el proceso de desarrollo y facilita la detección de errores.

### Configuración de variables de entorno en contenedores:
- Docker permite configurar variables de entorno en los contenedores mediante el uso de la opción `-e` o `--env` al ejecutar el contenedor: **`docker run -e VARIABLE=valor nombre_imagen`** `Esto establecerá la variable de entorno VARIABLE con el valor especificado dentro del contenedor.`

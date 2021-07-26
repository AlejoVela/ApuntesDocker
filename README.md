# ApuntesDocker
Apuntes Curso de Docker Fedesoft Profesor Johan Giraldo
## ¿Qué es docker y como funciona?

La tecnología Docker usa el kernel de Linux y las funciones de este, como Cgroups y namespaces, para segregar los procesos, de modo que puedan ejecutarse de manera independiente. El propósito de los contenedores es esta independencia: la capacidad de ejecutar varios procesos y aplicaciones por separado para hacer un mejor uso de su infraestructura y, al mismo tiempo, conservar la seguridad que tendría con sistemas separados.

Las herramientas del contenedor, como Docker, ofrecen un modelo de implementación basado en imágenes. Esto permite compartir una aplicación, o un conjunto de servicios, con todas sus dependencias en varios entornos. Docker también automatiza la implementación de la aplicación (o conjuntos combinados de procesos que constituyen una aplicación) en este entorno de contenedores.

Estas herramientas desarrolladas a partir de los contenedores de Linux, lo que hace a Docker fácil de usar y único, otorgan a los usuarios un acceso sin precedentes a las aplicaciones, la capacidad de implementar rápidamente y control sobre las versiones y su distribución.

## ¿La tecnología Docker es la misma que la de los contenedores de Linux tradicionales?
No. Al principio, la tecnología Docker se desarrolló a partir de la tecnología LXC, lo que la mayoría de las personas asocia con contenedores de Linux "tradicionales", aunque desde entonces se ha alejado de esa dependencia. LXC era útil como virtualización ligera, pero no ofrecía una buena experiencia al desarrollador ni al usuario. La tecnología Docker no solo aporta la capacidad de ejecutar contenedores; también facilita el proceso de creación y diseño de contenedores, de envío de imágenes y de creación de versiones de imágenes (entre otras cosas).
![Linux vs Docker](https://www.redhat.com/cms/managed-files/traditional-linux-containers-vs-docker_0.png)

Los contenedores de Linux tradicionales usan un sistema init que puede gestionar varios procesos. Esto significa que las aplicaciones completas se pueden ejecutar como una sola. La tecnología Docker pretende que las aplicaciones se dividan en sus procesos individuales y ofrece las herramientas para hacerlo. Este enfoque granular tiene sus ventajas.

## Ventajas de los contenedores Docker
### Modularidad
El enfoque Docker para la creación de contenedores se centra en la capacidad de tomar una parte de una aplicación, para actualizarla o repararla, sin necesidad de tomar la aplicación completa. Además de este enfoque basado en los microservicios, puede compartir procesos entre varias aplicaciones de la misma forma que funciona la arquitectura orientada al servicio (SOA).

### Control de versiones de imágenes y capas
Cada archivo de imagen de Docker se compone de una serie de capas. Estas capas se combinan en una sola imagen. Una capa se crea cuando la imagen cambia. Cada vez que un usuario especifica un comando, como ejecutar o copiar, se crea una nueva capa.

Docker reutiliza estas capas para construir nuevos contenedores, lo cual hace mucho más rápido el proceso de construcción. Los cambios intermedios se comparten entre imágenes, mejorando aún más la velocidad, el tamaño y la eficiencia -Keep it small: a closer look at Docker image sizing. El control de versiones es inherente a la creación de capas. Cada vez que se produce un cambio nuevo, básicamente, usted tiene un registro de cambios incorporado: control completo de sus imágenes de contenedor.

### Restauración
Probablemente la mejor parte de la creación de capas es la capacidad de restaurar. Toda imagen tiene capas. ¿No le gusta la iteración actual de una imagen? Restáurela a la versión anterior. Esto es compatible con un enfoque de desarrollo ágil y permite hacer realidad la integración e implementación continuas (CI/CD) desde una perspectiva de las herramientas.

### Implementación rápida
Solía demorar días desarrollar un nuevo hardware, ejecutarlo, proveerlo y facilitarlo. Y el nivel de esfuerzo y sobrecarga era extenuante. Los contenedores basados en Docker pueden reducir el tiempo de implementación a segundos. Al crear un contenedor para cada proceso, puede compartir rápidamente los procesos similares con nuevas aplicaciones. Y, debido a que un SO no necesita iniciarse para agregar o mover un contenedor, los tiempos de implementación son sustancialmente inferiores. Además, con la velocidad de implementación, puede crear y destruir la información creada por sus contenedores sin preocupación, de forma fácil y rentable.

Por lo tanto, la tecnología Docker es un enfoque más granular y controlable, basado en microservicios, que prioriza la eficiencia.

## ¿Hay limitaciones para el uso de Docker?
En sí mismo, Docker es una excelente herramienta para la gestión de contenedores individuales. Al comenzar a utilizar cada vez más contenedores y aplicaciones en contenedores, divididas en cientos de piezas, la gestión y la organización se pueden tornar muy difíciles. Finalmente, debe retroceder y agrupar los contenedores para ofrecer servicios, como redes, seguridad, telemetría, etc., en todos sus contenedores. Es aquí donde aparece Kubernetes.
 
Con Docker no se obtiene la misma funcionalidad tipo UNIX que se obtiene con los contenedores Linux tradicionales. Esto incluye poder usar procesos como cron o syslog dentro del contenedor, junto con su aplicación. También hay limitaciones, por ejemplo, en cuanto a la eliminación de procesos nieto después de terminar con los procesos hijo; algo que se gestiona de forma inherente en los contenedores de Linux tradicionales. Estas cuestiones se pueden mitigar mediante la modificación del archivo de configuración y el ajuste de esas habilidades desde el comienzo (algo que no es inmediatamente obvio a simple vista).
Asimismo, existen otros subsistemas y dispositivos de Linux que no tienen espacios de nombres. Estos incluyen SELinux, Cgroups y dispositivos /dev/sd*. Esto implica que si un atacante obtiene control de estos subsistemas, el host se ve comprometido. Para permanecer liviano, compartir el kernel del host con contenedores abre la posibilidad de una vulnerabilidad de la seguridad. Esto difiere de las máquinas virtuales, las cuales están mucho más segregadas del sistema host.

## ¿Los contenedores Docker son realmente seguros?
El daemon de Docker también puede ser una preocupación en materia de seguridad. Para usar y ejecutar los contenedores Docker, es muy probable que utilice el daemon de Docker, un tiempo de ejecución persistente para los contenedores. El daemon de Docker requiere privilegios de raíz, por lo que se debe prestar especial atención a quiénes obtienen acceso al proceso y en dónde reside este. Por ejemplo, un daemon local tiene una superficie de ataque más pequeña que uno que se encuentra en un sitio más público, como un servidor web.

> Tomado del sitio web oficial de RedHat

# Arquitectura Básica de Docker
![Arquitectura Docker](https://i.postimg.cc/sXXf7srL/Arquitectura-Docker.jpg)
Docker host: Host o servidor desde el cual se ejecuta Docker
## Que es una imagen y como se Compone
Cada comando del archivo Dockerfile funciona como una capa dentro de la imagen, usualmente el primer comando ejecutado es un “FROM” que suele indicar el sistema operativo que tendrá configurada la imagen; El segundo comando, indica la aplicación que a instalar (por ejemplo, para sistemas que usen el gestor de paquete “yum” se usuaria este comando para instalar la aplicación); El comando CMD ejecuta la orden que inicial el programa instalado previamente en RUN.
![Arquitectura Imagenes](https://i.postimg.cc/q790hn1N/Arquitectura-Imagenes.jpg)
### Ejemplo de un Dockerfile
![Ejemplo Dockerfile](https://i.postimg.cc/3rj7Nkmw/Ejemplo-Docker-File.jpg)
Como decíamos previamente, cada comando es una capa de la imágen de Docker.

## ¿Que es un contenedor?
Una Contenedor puede verse como una capa adicional que ejecuta las instrucciones dadas en las imágenes. A diferencia de las imágenes que funcionan solo en lectura (Read Only), los contenedores funcionando tanto en lectura como en escritura (Read and Write) por lo que es posible modificar las capas de la imagen desde un contenedor, sin embargo, esto no es recomendable dado que las modificaciones realizadas sobre un contenedor no serán persistentes, es decir, no modifican la imagen sino únicamente el contenedor y una vez este sea eliminado, se perderán los cambios realizados a la imagen. 
![Arquitectura Contenedores](https://i.postimg.cc/Wb64B9XX/Arquitectura-Contenedores.jpg)
## ¿Qué contiene un Contenedor?
Un contenedor puede contener imágenes, volúmenes y redes.
![Contenido contenedor](https://i.postimg.cc/sfm8b755/Contenido-Contenedor.jpg)

## Comandos Importantes
**Subir Contenedores**  
docker-compose up  
**Subir Contenedores en segundo plano**  
docker-compose up -d  
**Subir una imagen con un nombre distinto al nombre por defecto usado en Dockerfile o docker-composer**  
docker-compose -f docker-compose-jenkins.yml up -d  
**Bajar imágenes desde la mas pequeña hasta la mas grande**  
docker-compuse down  
**Eliminar imagenes (Por id o nombre)**  
docker rm idImagen  
**Listar Imagenes**  
*docker ps*  
*docker image ls*  
**Listar contenedores Docker Compose**  
docker-compose ps  
**Revisar log de un contenedor**  
docker logs -f codimd_codimd_1  
**Iniciar un contenedor**  
docker container start nombreContenedor  
**Reiniciar contenedor**  
docker container restart nombreContenedor  
**Detener un contenedor**  
docker container stop nombreContenedor  
**Para no tener que ingresar sudo en cada comando de docker**  
sudo usermod -aG docker nombreUsuario  
**Obtener información de una imagen**  
docker inspect nombreImagen  
**Escalar de manera Horizontal y crear varios contenedores de una aplicación**  

Comando docker-compose up --scale web=5 -d


### Enlaces interesantes  
**Crear imagen desde contenedor corriendo**  
https://docs.docker.com/engine/reference/commandline/commit/   
**Página web profesor**  
https://jsgiraldoh.io  
[Archivos Docker Compose](https://jsgiraldoh.io/Blog/Archivo-docker-compose)  
**Instalar Docker**  
https://docs.docker.com/engine/install/ubuntu/  
**Instalar Docker Compose**  
https://docs.docker.com/compose/install/  


## Instalación de jenkins  
Usamos el comando **git clone https://github.com/jsgiraldoh/Jenkins**  
Hacemos cd Jenkins (carpeta que se crea al clonar jenkins)  
Esto es necesario para archivos que tienen un nombre especifico distinto a **Docker-compose.yml**, por ejemplo, en el caso de Jenkins:  
**docker-compose -f docker-compose-jenkins.yml up -d**  
Debemos otorgar permisos  
**sudo chown ubuntu:ubuntu jenkins_home/**  
**sudo chmod 2777 jenkins_home/**  
Montamos nuevamente con docker-compose  
Vamos a la dirección ip del Docker host:8090 por ejemplo:  
http://192.168.20.43:8090  
Y ejecutamos el comando para que nos devuelva la contraseña  
**docker logs -f Jenkins**  
![](https://i.postimg.cc/vZ98M0Y4/jenkins-key.jpg)  
Después instalamos los plugins Recomendados de Jenkins  
![](https://i.postimg.cc/Fz7m6ZCs/jenkins-instaal.jpg)  
Por ultimo, se ingresan los datos para crear el usuario y finalmente se carga el menú principal de Jenkins  
[![jj.jpg](https://i.postimg.cc/PxFn1DfG/jj.jpg)](https://postimg.cc/bDb5hs2L)  

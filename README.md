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

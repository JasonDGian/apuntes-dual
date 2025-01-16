# 📌 Introduccion a Jenkins.

## 📓 ¿Qué es Jenkins?
Jenkins es una herramienta de código abierto diseñada para facilitar los procesos de integración continua (CI) y entrega continua (CD) en el desarrollo de software. Se utiliza para automatizar la construcción, prueba y despliegue de aplicaciones, permitiendo a los equipos trabajar de manera más eficiente y detectar errores rápidamente. Se puede utilizar en cualquier sistema operativo, de modo local o en cloud, y puede ser contenedorizado.

>[!TIP]
>**Jenkins Job**: Un Jenkin Job es una tarea ejecutable que es supervisada y ejecutada por Jenkins.

## 📍 Arquitectura de Maestro y Esclavo.
Jenkins está basado en arquitectura de Maestro y Esclavo, en la que el Maestro se encarga de programar los Jenkins Jobs y enviarlos al Esclavo para que este los ejecute e informen del resultado.

### 🗒️ El maestro:
En Jenkins, el maestro (también conocido como master) es el servidor principal que coordina y gestiona todo el proceso de integración continua. Es el componente central de Jenkins, desde el cual se gestionan las tareas, configuraciones y comunicación con los esclavos (nodos agentes). En términos de arquitectura, el maestro es el componente central de Jenkins, y se refiere a la máquina o proceso donde se ejecuta el software principal de Jenkins, que incluye la interfaz web, la lógica de orquestación y la administración de trabajos.

### 🗒️ El nodo esclavo:
En los términos de hardware y software, un esclavo (también llamado nodo agente o agent node) en Jenkins es una máquina o entorno que se conecta al maestro para ejecutar trabajos específicos que le son asignados. **Un esclavo de Jenkins puede ser cualquier máquina física, virtual o contenedor que tenga la capacidad de ejecutar trabajos de Jenkins.** El software que ejecuta un esclavo de Jenkins incluye principalmente el agente de Jenkins (Jenkins agent), que es un proceso o servicio que se ejecuta en la máquina esclava. Este agente es responsable de permitir que el esclavo se conecte con el maestro de Jenkins y reciba las tareas asignadas.

### 🗒️ El agente esclavo:
En un nodo esclavo de Jenkins, puedes tener múltiples agentes esclavos, cada uno de los cuales puede ejecutar trabajos de manera independiente. Este enfoque es útil cuando deseas aprovechar los recursos de un solo nodo esclavo para ejecutar varios trabajos en paralelo, o cuando necesitas distintos entornos de ejecución en el mismo nodo físico o virtual.

![imagen](https://github.com/user-attachments/assets/ed966825-acfc-4ba0-8bf6-d0f53b7883c5)


## 📍 Crear tareas en Jenkins.
Con el servicio preparado y corriendo abrimos el portal de jenkins y seguimos los siguientes pasos:
1. Hacemos clic en `Nueva Tarea`
2. Asignamos un nombre a la tarea y seleccionamos tipo de tarea.
3. Establecemos parametros y configuraciones para la tarea.
4. Comprobamos el éxito de la operacion.
   
Para más información consulta [este documento](jenkins-jobs.md).


## 📍 Directorios de trabajo de Jenkins.
Entre los directorios de trabajo de Jenkins encontraremos dos directorios:
- `/var/jenkins_home/workspace`
- `/var/jenkins_home/jobs`.
Uno almacena los ficheros de construccion y el otro el historial de construcciones.
   
### 🔸 Directorio `/var/jenkins_home/workspace`
El directorio `/var/jenkins_home/workspace` es el área de trabajo donde Jenkins almacena los archivos del proyecto durante la ejecución de los trabajos (jobs). Aquí se crean subdirectorios específicos para cada trabajo, donde Jenkins descarga y manipula el código fuente. 

- **Objetivo**: Facilitar un entorno aislado para cada trabajo en el cual Jenkins pueda realizar construcciones, pruebas y otras operaciones sin interferencias de otros trabajos.
- **Estructura**: Contiene subdirectorios para cada trabajo en Jenkins. Por ejemplo, si tienes un trabajo llamado `JobX`, su workspace se ubicará en `/var/jenkins_home/workspace/JobX`.

### 🔸 Directorio `/var/jenkins_home/jobs`
El directorio `/var/jenkins_home/jobs` contiene la configuración y el historial de ejecuciones de los trabajos en Jenkins. Aquí es donde Jenkins guarda toda la información necesaria para administrar y ejecutar cada trabajo.

- **Objetivo**: Almacenar la configuración de los trabajos y el historial de ejecuciones. Esto incluye registros de ejecución, resultados de pruebas y otros datos relevantes.
- **Estructura**: Contiene un subdirectorio para cada trabajo. Dentro de cada uno de estos subdirectorios, encontrarás más carpetas que almacenan diferentes tipos de información, como configuraciones y registros de ejecuciones. Por ejemplo, para un trabajo llamado `JobX`, su información se almacenará en `/var/jenkins_home/jobs/JobX`.

#### 🧮 Ejemplo Visual
Imaginemos que tienes un trabajo llamado `JobX`:
- `workspace/JobX/` es el directorio donde Jenkins descargará el código y realizará la construcción actual.
- `JENKINS_HOME/jobs/JobX/builds` es el directorio donde Jenkins guarda el historial de ejecuciones del trabajo, con subdirectorios para cada ejecución.
    
![image](https://github.com/user-attachments/assets/780504ae-aa5d-4168-94e2-79cefae4cb43)

## Resumen
El "workspace" en Jenkins es un área de trabajo aislada específica para cada trabajo, donde se descargan y manipulan los archivos durante la ejecución. El historial de ejecuciones se guarda en un directorio separado, asegurando que cada trabajo tenga acceso a un espacio limpio y actualizado para sus operaciones.

   

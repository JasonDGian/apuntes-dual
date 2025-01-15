# 📌 Antes de comenzar: ¿Qué es la Integracion continua (CI)?
La integración continua (CI) es una práctica de desarrollo de software que consiste en integrar y verificar automáticamente el código nuevo en un repositorio central varias veces al día. 
Esta práctica permite detectar y corregir errores rápidamente, mejorando la calidad del software y facilitando la colaboración entre desarrolladores.

## 📍 ¿Cómo funciona la integración continua?
1. Los desarrolladores trabajan en conjunto en una aplicación.
2. Modifican el código separadamente y aplican cambios a distintas partes de la aplicacion.
3. Esos cambios los envían a un repositorio de código fuente central, compartido.
4. Desde el repositorio, el código llega al Servidor CI (lo clona el servidor).
5. Dentro del servidor se hace la construccion o 'build' del código.
6. Una vez obtenida una construcción, se realizan una bateria de pruebas.
7. Con los resultados obtenidos, se informa al equipo de desarrollo de la calidad del código subido.
   
![image](https://github.com/user-attachments/assets/5f0dac98-b200-46fd-8195-d0b765f9e6d0)
    
### 🗒️ Acerca del repositorio central.
En una configuración típica de integración continua (CI), el repositorio de código no reside en el servidor de CI. Generalmente, el repositorio de código está alojado en 
una plataforma de control de versiones como GitHub, GitLab, Bitbucket, o similares. El servidor de CI está configurado para monitorear ese repositorio y, cuando se 
detectan cambios (como commits o pull requests), el servidor de CI clona o extrae el código del repositorio y ejecuta una serie de pruebas y compilaciones automatizadas.

## 📍 ¿Qué beneficios conlleva el uso de integración continua?
La integración continua ofrece múltiples beneficios, entre los que destacan:
- Reducción del tiempo para identificar errores: Permite detectar problemas en las etapas iniciales del desarrollo, lo que facilita una solución rápida y eficiente.
- Ahorro de tiempo en la corrección de errores: Las actualizaciones son más pequeñas y manejables, lo que simplifica el proceso de depuración.
- Menos problemas de integración: Al integrar cambios continuamente, se minimizan los conflictos en el código, lo que contribuye a acelerar la entrega de productos de mayor calidad.

## 📍 Etapas de implementación de integración continua.
La implementación de CI no es un paso único, es un proceso adoptado por la organización de trabajo y para lograrlo deberemos cumplir con las siguientes prácticas.

#### 🔸 Automatizar el proceso de build o compilación. 
Este proceso debe de incluir la construcción de la aplicación y la ejecución de pruebas unitarias que comprueben el estado.   
#### 🔸 Optimizar la 'build' para que se auto-testee
Deben existir pruebas diseñadas y creadas para que su ejecución automatica permita comprobar el estado del proyecto para ver si todo está bien o si hay errores y el resultado sea entregado automaticamente al equipo de desarrollo.
#### 🔸 Manenter un unico repositorio de código fuente.
El equipo de desarrolladores que trabaja en el proyecto, deben de reunir su progreso en un único repositorio central.
#### 🔸 Mantener la visibilidad de eventos.
En el trabajo de equipo, es crucial que todos puedan ver en todo momento 'que está pasando', incluyendo la build, los unit-test, dependencias, o que falla en caso de error.
#### 🔸 Despliegue automatico.
Despliegue sin intervención manual, utilizando herramientas y scripts que automatizan las tareas necesarias. Permite que los equipos puedan entregar actualizaciones de software de manera más rápida, confiable y consistente.

>[!CAUTION]
> En la integración continua, es importante hacer check-in de manera frecuente, **siempre y cuando el código haya sido testeado, no presente errores y la build funcione correctamente**.


# 📌 Antes de comenzar: ¿Qué es el Despliegue Continuo?
El despliegue continuo es una práctica en el desarrollo de software que consiste en automatizar la liberación de cada compilación exitosa al entorno de producción, una vez que ha pasado todas las pruebas necesarias. Esta práctica asegura entregas rápidas, consistentes y confiables, optimizando el flujo de desarrollo.
    
>[!TIP]
>El conjunto de Integracion Continua con Despliegue continuo se conoce como `CI/CD`
    
# 📌 Instalación de Jenkins con Docker (Windows).
>[!IMPORTANT]
> Antes de comenzar con la instalación, debemos de tener instalado y adecuadamente configurado Docker.
       
Con docker instalado en el equipo, seguimos los siguientes pasos:
   1. Descargamos la imagen de [jenkins](https://hub.docker.com/r/jenkins/jenkins) de dockerhub .
   2. Creamos el directorio donde deseamos que Jenkins almacene sus datos.
   3. Ejecutamos el comando de creación de contenedor con la configuración deseada.
   4. Recuperamos la contraseña y accedemos al portal Jenkins desde el navegador.
          
---
           
**1. Descargamos la imagen de jenkins.**
>```bash
>docker pull jenkins/jenkins
>```
       
**2. Creamos un directorio para que haga de 'home' a nuestra instalación de Jenkins.**    
>Este directorio es importante porque al apagar el contenedor el contenido se perderá, para evitar perderlo configuraremos un volumen de docker en nuestro
>host que será el encargado de mantener esos datos y ficheros.
    
**3. Ejecutamos el siguiente comando para crear el contenedor.**    
>Recordando configurar los parametros de los puertos y el directorio home.
>```bash
>docker run --name mi-jenkins -p [puerto host]:8080 -p [puerto agente conexion host]:50000 -v [directorio home en host]:/var/jenkins_home jenkins/jenkins:latest
>```
    
**4. Consulta de la contraseña.**   
>Para consultar la contraseña configurada debemos de ejecutar la consola bash dentro del contenedor. Para ello introducimos el siguiente comando:
>```bash
>docker exec -ti jenkins bash
>```
>Donde `jenkins` es el nombre que hemos dado al contenedor y `bash` es el comando que deseamos ejecutar.
>Esto nos abrirá la terminal bash en modo _attached_ al contenedor. Una vez hecho eso, ejecutaremos el siguiente comando.
>```bash
>cat /var/jenkins_home/secrets/initialAdminPassword
>```
>Como resultado obtendremos por pantalla la contraseña perteneciente a la instancia de Jenkins actual.
>    
>![image](https://github.com/user-attachments/assets/cb066c53-7b60-4e25-ba95-e88b28a92342)
    
**5. Con la contraseña preparada, abrimos la URL de acceso desde un navegador y nos autenticamos con ella.**      
> La url de acceso al servicio Jenkins dependerá del metodo elegido. En docker deberá ser `localhost:<puerto configurado>`. En caso de estar ejecutando en una máquina distinta, deberemos emplear la IP de dicha maquina para realizar el acceso.
>    
>![image](https://github.com/user-attachments/assets/87056e14-61b0-4735-b662-f8ebc4f4a227)
    
---
    
# 📌 Instalación de Jenkins con Docker (Linux).
Con docker instalado en el equipo, seguimos los siguientes pasos:
   1. Descargamos la imagen de [jenkins](https://hub.docker.com/r/jenkins/jenkins) de dockerhub .
   2. Creamos el directorio donde deseamos que Jenkins almacene sus datos.
   3. Damos los permisos al usuario Jenkins sobre ese directorio.
   4. Ejecutamos el comando de creación de contenedor con la configuración deseada.
   5. Recuperamos la contraseña y accedemos al portal Jenkins desde el navegador.
    
--- 
    
**1. Descargamos la imagen de jenkins.**   
>```bash
>docker pull jenkins/jenkins
>```

![imagen](https://github.com/user-attachments/assets/9ad4c5aa-36fe-4094-a7be-a74e7730669e)
    
**2. Creamos un directorio para que haga de 'home' a nuestra instalación de Jenkins.**    
> Este directorio es importante porque al apagar el contenedor el contenido se perderá, para evitar perderlo configuraremos un volumen de docker en nuestro
>host que será el encargado de mantener esos datos y ficheros.
>```bash
>mkdir -p jenkins/jenkins_home
>```
>
>![imagen](https://github.com/user-attachments/assets/a3489a05-0579-4e6a-8a96-ce8f7f00c2be)

>[!NOTE]
>En instalaciones tipicas, jenkins utiliza el directorio `/var/jenkins_home/` para almacenar sus datos y ficheros.

**3. Otorgamos permisos necesarios en la carpeta al usuario Jenkins ( normalmente utiliza UID 1000 ).**   
Con este comando otorgaremos la propiedad del directorio `jenkins` al usuario 1000 y grupo 1000, necesario para que el contenedor pueda usar el directorio adecuadamente.
Para más información acerca de este apartado consultar [este documento](usuario-jenkins.md). 
>```bash
>sudo chown -R 1000:1000 jenkins
>```


     
>[!IMPORTANT]
>En una instalación de Docker, Jenkins generalmente usa el UID 1000 si la cuenta de usuario de Jenkins dentro del contenedor está configurada con ese UID. Esto puede depender de la imagen de Docker específica que estés utilizando para Jenkins. Muchas imágenes de Docker, incluyendo la oficial de Jenkins, están configuradas para ejecutar Jenkins bajo un usuario que tiene el UID 1000 por defecto.

**4. Ejecutamos el siguiente comando para crear el contenedor.**    
>Recordando configurar los parametros de los puertos y el directorio home.
>```bash
>docker run --name mi-jenkins -p [puerto host]:8080 -p [puerto agente conexion host]:50000 -v [directorio home en host]:/var/jenkins_home jenkins/jenkins:latest
>```
>   
>![imagen](https://github.com/user-attachments/assets/f110468e-a53a-4b0b-abc6-4e38a6a8a565)
    
    
**5. Consulta de la contraseña.**    
>Para consultar la contraseña configurada debemos de ejecutar la consola bash dentro del contenedor. Para ello introducimos
>```bash
>docker exec -ti mi-jenkins bash
>```
>Donde `mi-jenkins` es el nombre que hemos dado al contenedor y `bash` es el comando que deseamos ejecutar.
>    
>Esto nos abrirá la terminal bash en modo _attached_ al contenedor. Una vez hecho eso, ejecutaremos el siguiente comando.
>```bash
>cat /var/jenkins_home/secrets/initialAdminPassword
>```
>Como resultado obtendremos por pantalla la contraseña perteneciente a la instancia de Jenkins actual.
>    
>![imagen](https://github.com/user-attachments/assets/8fcf868b-62a0-4d90-b53a-4d2e4600a8ad)
        
**6. Con la contraseña preparada, configuramos la instancia inicial.**      
>    
>![image](https://github.com/user-attachments/assets/87056e14-61b0-4735-b662-f8ebc4f4a227)
>
> Procedemos a instalar los plugins básicos seguidos de los plugins especificos para nuestra aplicacion que puedan ser necesarios. 
> ![imagen](https://github.com/user-attachments/assets/d19e9460-a75c-45cd-b224-e977721208b7)
>
> Configuramos el usuario administrador, la url base y listo.
> ![imagen](https://github.com/user-attachments/assets/d1a91129-310f-4840-9f26-bbd32fe9e4cf)
   



# 🗒️ OPCIONAL: Fichero docker compose.
Por comodidad podemos configurar un fichero docker compose y usarlo con los comandos de docker para simplificar.

>[!CAUTION]
> Este fichero emplea la configuración de acceso privilegiado `privileged: true` que supone un riesgo de seguridad y nunca deberá ser usada en entornos de produccion.

```yml
    version: '3'
    services:
        jenkins:
            image: jenkins/jenkins 
            ports:
                - 8080:8080
                - 50000:50000
            container_name: jenkins
            privileged: true
            user: root
            volumes:
                - $PWD/jenkins_home:/var/jenkins_home 
            networks:
                - net
    networks:
        net: 
```

   
---
   
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

---   
   

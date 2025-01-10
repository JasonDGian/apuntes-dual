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

<!--# 📌 Instalación de Jenkins.
Existen distintas maneras de instalar y montar Jenkins. 
1. Instalación de Jenkins de forma local con una máquian virtual clásica.
2. Instalación en la nube utilizando Docker (AWS, Digital Ocean, Google Cloud, Azure...).
3. Instalación en Vagrant (Herramienta para gestionar máquinas virtuales).
4. Instalación contenedorizada en Docker local. -->

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
    
**2. Creamos un directorio para que haga de 'home' a nuestra instalación de Jenkins.**    
> Este directorio es importante porque al apagar el contenedor el contenido se perderá, para evitar perderlo configuraremos un volumen de docker en nuestro
>host que será el encargado de mantener esos datos y ficheros.
>```bash
>mkdir -p jenkins/jenkins_home
>```

>[!NOTE]
>En instalaciones tipicas, jenkins utiliza el directorio `/var/jenkins_home/` para almacenar sus datos y ficheros.

**3. Otorgamos permisos necesarios en la carpeta al usuario Jenkins ( normalmente utiliza UID 1000 ).**   
>```bash
>chown 1000 jenkins
>```
    
>[!IMPORTANT]
>En una instalación de Docker, Jenkins generalmente usa el UID 1000 si la cuenta de usuario de Jenkins dentro del contenedor está configurada con ese UID. Esto puede depender de la imagen de Docker específica que estés utilizando para Jenkins. Muchas imágenes de Docker, incluyendo la oficial de Jenkins, están configuradas para ejecutar Jenkins bajo un usuario que tiene el UID 1000 por defecto.

**4. Ejecutamos el siguiente comando para crear el contenedor.**    
>Recordando configurar los parametros de los puertos y el directorio home.
>```bash
>docker run --name mi-jenkins -p [puerto host]:8080 -p [puerto agente conexion host]:50000 -v [directorio home en host]:/var/jenkins_home jenkins/jenkins:latest
>```
    
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
>![image](https://github.com/user-attachments/assets/cb066c53-7b60-4e25-ba95-e88b28a92342)
    
**6. Con la contraseña preparada, abrimos la URL de acceso desde un navegador y nos autenticamos con ella.**      
>    
>![image](https://github.com/user-attachments/assets/87056e14-61b0-4735-b662-f8ebc4f4a227)


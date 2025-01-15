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

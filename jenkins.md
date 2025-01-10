![image](https://github.com/user-attachments/assets/5e6adfd9-e698-48b0-b762-55ef61cc1923)# 📌
## 📍
### 📔
#### 🔸
##### 🧮

# 📌 Antes de comenzar: ¿Qué es la Integracion continua (CI)?
La integración continua (CI) es una práctica de desarrollo de software que consiste en integrar y verificar automáticamente el código nuevo en un repositorio central varias veces al día. 
Esta práctica permite detectar y corregir errores rápidamente, mejorando la calidad del software y facilitando la colaboración entre desarrolladores.

## ¿Cómo funciona la integración continua?
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

# 📌 Instalación de Jenkins.
Existen distintas maneras de instalar y montar Jenkins. 
1. Instalación de Jenkins de forma local con una máquian virtual clásica.
2. Instalación en la nube utilizando Docker (AWS, Digital Ocean, Google Cloud, Azure...).
3. Instalación en Vagrant (Herramienta para gestionar máquinas virtuales).
4. Instalación contenedorizada en Docker local.

## 📍 Instalación de Jenkins en Docker.
Con docker instalado en el equipo, seguimos los pasos a continuación:

1. Vamos a la página de dockerhub para la imágen de Jenkins. https://hub.docker.com/r/jenkins/jenkins
2. Copiamos el comando de pull indicado `docker pull jenkins/jenkins`.    
![image](https://github.com/user-attachments/assets/a9c4305f-424b-4298-8756-f22043f51daf)    

3. Ejecutamos el comando en la terminal de nuestro docker.    
![image](https://github.com/user-attachments/assets/dd770be3-dcf9-4265-8aba-d1db9f7ca534)    

4. Creamos un directorio para que haga de 'home' a nuestra instalación de Jenkins.
```bash
mkdir -p jenkins/jenkins_home
```
5. Otorgamos permisos de escritura en la carpeta al usuario Jenkins ( normalmente utiliza UID 1000 ).
```bash
chown 1000 jenkins
```
6. Copiamos el fichero `docker-compose.yml` con la configuración preferida en el directorio home de Jenkins.    
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

7. Ejecutamos un contenedor tomando como base el fichero `docker-compose.yml`.
```bash
docker-compose up -d
```
    
![image](https://github.com/user-attachments/assets/d26c77b0-f7f5-4ff6-8424-2651a726a5e6)

8. Consulta de la contraseña.    
Para consultar la contraseña configurada debemos de ejecutar la consola bash dentro del contenedor. Para ello introducimos
```bash
docker exec -ti jenkins bash
```
Donde `jenkins` es el nombre que hemos dado al contenedor y `bash` es el comando que deseamos ejecutar.
    
Esto nos abrirá la terminal bash en modo _attached_ al contenedor. Una vez hecho eso, ejecutaremos el siguiente comando.
```bash
cat /var/jenkins_home/secrets/initialAdminPassword
```
Como resultado obtendremos por pantalla la contraseña perteneciente a la instancia de Jenkins actual.
    
![image](https://github.com/user-attachments/assets/cb066c53-7b60-4e25-ba95-e88b28a92342)
    
10. Con la contraseña preparada, abrimos la URL de acceso desde un navegador y nos autenticamos con ella.      
    
![image](https://github.com/user-attachments/assets/87056e14-61b0-4735-b662-f8ebc4f4a227)



>[!IMPORTANT]
>En una instalación de Docker, Jenkins generalmente usa el UID 1000 si la cuenta de usuario de Jenkins dentro del contenedor está configurada con ese UID. Esto puede depender de la imagen de Docker específica que estés utilizando para Jenkins. Muchas imágenes de Docker, incluyendo la oficial de Jenkins, están configuradas para ejecutar Jenkins bajo un usuario que tiene el UID 1000 por defecto.

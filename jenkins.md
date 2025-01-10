# 📌
## 📍
### 📔
#### 🔸
##### 🧮

# 📌 Integracion continua.
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


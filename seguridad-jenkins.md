# 📌 Seguridad en Jenkins
Jenkins es una herramienta vital en el ecosistema de una empresa de desarrollo. Para protegerla, es esencial seguir las prácticas conocidas como 'buenos hábitos', que incluyen lo siguiente:

>[!NOTE]
>**¿Por qué es importante la seguridad en Jenkins?**  
En el pasado, se han descubierto brechas de seguridad que pueden ser explotadas sin necesidad de iniciar sesión en Jenkins. Esto ha permitido a usuarios malintencionados acceder a una cantidad significativa de información sensible.

### 🔸 Proteger Jenkins de Internet
**Jenkins es una herramienta de uso interno en red privada.** Para proteger a Jenkins de la red externa, se pueden crear reglas en el cortafuegos y ubicarlo tras una VPN empresarial. Si está en la nube, se debe utilizar el firewall que ofrecen y bloquear todos los puertos, permitiendo el acceso solo a la IP de la oficina o la VPN, si se dispone de una.

> [!CAUTION]
> Recuerda agregar a la lista blanca (whitelist) de tu cortafuegos las direcciones de **GitHub**, **GitLab** y **Bitbucket** para que Jenkins pueda hacer *pull* de los repositorios de trabajo.

### 🔸 Establecer autenticación y autorizaciones
Esta práctica permite restringir permisos a los usuarios que no deben tener privilegios de administrador y personalizar la experiencia y autoridad de los usuarios según sea necesario. Por ejemplo, un usuario podrá leer, otro podrá ejecutar un job, otro podrá ejecutar y modificar jobs, etc.

### 🔸 Emplear directorios de usuarios más avanzados como LDAP o SAML
Utilizar directorios de usuarios avanzados como LDAP o SAML permite una gestión centralizada y segura de las credenciales de los usuarios. Estas tecnologías facilitan la autenticación y autorización de manera eficiente, mejorando la seguridad y simplificando el acceso a múltiples aplicaciones y servicios.

### 🔸 Utilizar claves de acceso complejas
Es evidente la razón detrás de esta práctica: las claves complejas son significativamente más seguras que las contraseñas cortas y simples. Las contraseñas robustas reducen el riesgo de acceso no autorizado y protegen mejor la información sensible.

### 🔸 Mantener Jenkins actualizado a la última versión disponible
Es fundamental mantener Jenkins siempre actualizado. Cada actualización incluye mejoras de seguridad cruciales, resolviendo vulnerabilidades y corrigiendo fallos que podrían ser explotados por usuarios malintencionados para acceder a información y datos sensibles.

> [!IMPORTANT]
> Al igual que con la versión de Jenkins, los plugins son piezas de software que deben mantenerse actualizadas a la última versión por los mismos motivos.

### 🔸 Usar versiones LTS (Long Term Support)
Las versiones LTS reciben soporte durante un lapso de tiempo más extendido en comparación con las versiones regulares. Es una buena idea emplear, en la medida de lo posible, versiones LTS que son más estables.  
**En Jenkins contenedorizado: Usar la `latest-tag`.**

### 🔸 Consultar el changelog
Es de vital importancia consultar el registro de cambios (_changelog_). Este registro recoge los cambios introducidos en el salto de una versión a otra y es importante estar al tanto en el caso de que haya que realizar cambios en el flujo de trabajo o instalación.


## 📍 Autenticación.
En Jenkins la autenticación está habilitada por defecto.    
   
Para configurar la autenticación, en el panel lateral izquierdo, pinchamos en **`Administrar Jenkins`**.       
    
![image](https://github.com/user-attachments/assets/427bbca4-b94c-4c03-a09f-3a2978439ecd)
    
A continuación pinchamos en **`Configuración global de la seguridad.`**.    
    
![image](https://github.com/user-attachments/assets/34b81fea-1bc5-4209-a3b2-dcdf75b3899d)    
       
En el panel de configuración emergente, seleccionamos las opciones de seguridad que deseamos configurar.    
En este ejemplo configuraremos: **`Usar base de datos de Jenkins`** y **`Usuarios autenticados tienen privilegios para todo`**.     
     
![image](https://github.com/user-attachments/assets/285b141c-f263-413e-89ab-7850903f60b4)


 Esta configuración permitirá manejar los usuarios de forma local con Jenkins independiente de cualquier sistema que la empresa tenga montado en su ecosistema pre-existente. Esto es util cuando Jenkins atiende a pocos usuarios o cuando la empresa no dispone de un ecosistema de usuarios proprio sobre el cual enlazarse.

#### 🔸 Registro de usuarios en Jenkins.
Es posible habilitar el registro de usuarios en jenkins, pero esto supone un fallo de seguridad ya que cualquier persona con acceso a la red donde está hospedado el servicio será capaz de registrarse y accedere al servicio Jenkins. Lo más común es que el administrador de Jenkins sea el encargado de dar de alta a los usuarios que necesiten acceder al servicio.

>[!NOTE]
> Es posible enlazar Jenkins con servicios hosteados de bases de datos que soporten SAML. Servicios como Google o OneLogin son ejemplos de posibles enlaces para la gestión de usuarios en Jenkins mediante SAML. También es posible enlazar Jenkins con una BBDD de Active Directory.

## 📍 Autorización.
Cuando hablamos de autorización hablamos de la funcion de especificar 'derechos de acceso' a los recursos relacionados con la seguridad de la información y en general al control de acceso. Los niveles de autorización disponibles en jenkins son los siguientes:
- Cualquiera puede acceder y realizar cualquier accion.
- Usuarios autenticados pueden realizar cualquier acción.
- Estrategia de seguridad según proyecto.
- Plug-in de estrategia basada en roles.


### 🔸 Configuración de estrategia basada en proyecto.
Para configurar esta estrategia de autorización, en el panel lateral izquierdo, pinchamos en **`Administrar Jenkins`** y a continuación en **`Configuración global de la seguridad`**. Una vez aquí seleccionamos **`Estrategia de seguridad para el proyecto`**.   
    
![image](https://github.com/user-attachments/assets/449c422b-fd08-4e49-9268-0f7839224d3b)

>[!CAUTION]
> Aparecerá una tabla de configuración, para actualizar la tabla debemos guardar los cambios y recargar la página. Haciendo esto aparecerá el usuario de administrador con privilegios de **`Administer`**. **Es de vital importancia no borrar/desacrtivar estos privilegios, de lo contrario perderemos el control de la plataforma y deberemos restaurarlos modificando manualmente los ficheros de configuración de Jenkins y eso puede resultar dificil en entornos reales de desarrollo.**

#### 🔹 Añadir usuarios y grupos.
Para añadir un usuario o un grupo de usuarios y configurar su nivel de acceso pincharemos en **`Add user or group...`**.   
   
 ![image](https://github.com/user-attachments/assets/02646218-5beb-45d6-8eeb-3e5ffabfbd6b)
    
En la ventana emergente introduciremos el nombre del usuario o del grupo a añadir.    
   
![image](https://github.com/user-attachments/assets/166de646-85da-4a44-adc7-cc792f30a152)

Pinchando en **`Guardar`** aparecerá en la lista nuestro nuevo usuario.    
    
![image](https://github.com/user-attachments/assets/2d258a78-eaa4-488d-a030-ca98f4e4c35d)

#### 🔹 Configurar acceso de usuarios y grupos.
En la tabla de usuarios y grupos podremos otorgarles permisos para realizar distintas operaciones sobre las tareas, nodos, ejecuciones, vistas, etc...    
     
![image](https://github.com/user-attachments/assets/da2a86d7-6629-4f83-80f4-6b87e5603aee)

##### Modificacion de tareas mediante Jenkinsfile.
Para los desarrolladores es también posible modificar el Jenkinsfile, o añadir uno proprio para configurar distintamente una tarea de Jenkins sin necesidad de tener acceso de modificacion otorgado en Jenkins. 

### 🔸 Configuración de estrategia basada en plugin roles y grupos.
El primer paso para implementar este tipo de configuración será instalar el plug-in.
Para ello vamos al panel de control de Jenkins y pinchamos en **`Administrar Plugins`**.    
    
![image](https://github.com/user-attachments/assets/497a1889-6f46-4590-9b53-8d6f7567496b)

 A continuación buscaremos el plugin llamado **Role-based Authorization Strategy** y lo instalaremos sin reiniciar.      
    
![image](https://github.com/user-attachments/assets/6ec8f6f4-0495-4343-82e8-62b2b1a35479)

Con el plugin instalado, en la configuración global de seguridad aparecerá una nueva opción llamada **`Role-Based Strategy`**. La seleccionamos y pinchamos en **`Guardar`.**      
   
![image](https://github.com/user-attachments/assets/aa92dfcc-d0f6-4049-a487-ddeccd57e900)

Con esta opción activada, aparecerá una nueva entrada en el panel de control llamada **`Manage and Assign Roles`**. Ahora el plugin será el encargado de manejar todo lo relacionado a la autorizacion y gestion de privilegios de los usuarios.    
    
![image](https://github.com/user-attachments/assets/2455c128-8387-4d15-87fc-8feb41fa7d91)

#### 🔹 Crear roles.
Para crear roles, en el panel de control del plugin, pinchamos en **`Manage Roles`**.    
   
![image](https://github.com/user-attachments/assets/6c6566ff-8169-4f6d-b894-dd0f4d23f8f4)



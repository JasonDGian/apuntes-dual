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

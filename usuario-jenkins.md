# 📌 Acerca del usuario jenkins.
Cuando creamos un contenedor de Jenkins en un sistema Linux, uno de los pasos esenciales es garantizar que el contenedor tenga los permisos necesarios para leer y escribir en el directorio montado como volumen. Esto asegura que Jenkins pueda guardar configuraciones, datos de construcción, plugins y otros archivos críticos.

## 🔧 Contexto: El Usuario jenkins en Docker
Dentro del contenedor, Jenkins se ejecuta con un usuario específico llamado jenkins, que tiene los siguientes identificadores:
- **UID (Identificador de Usuario)**: 1000
- **GID (Identificador de Grupo)**: 1000
    
Estos identificadores son importantes porque Docker no utiliza el nombre del usuario (jenkins), sino sus identificadores (UID y GID) para determinar si el proceso tiene acceso al sistema de archivos del host cuando se monta un volumen.

Por defecto, el UID y GID del usuario jenkins en el contenedor son 1000, y los permisos en el host deben coincidir para evitar errores de acceso.

## 🚩 Problema Común
Cuando intentas ejecutar un contenedor de Jenkins con un volumen montado (por ejemplo, -v /path/to/jenkins_home:/var/jenkins_home), puedes encontrarte con el siguiente error:
```bash
INSTALL WARNING: User: missing rw permissions on JENKINS_HOME: /var/jenkins_home
touch: cannot touch '/var/jenkins_home/copy_reference_file.log': Permission denied
Can not write to /var/jenkins_home/copy_reference_file.log. Wrong volume permissions?
```
    
![imagen](https://github.com/user-attachments/assets/7f23448a-f820-48df-9def-b32911ff945c)
    
**Esto ocurre porque el contenedor no puede escribir en el directorio montado desde el host. Este problema surge debido a que el usuario dentro del contenedor (UID: 1000) no tiene permisos sobre el directorio montado en el host.**

## 🔨 Solución: Configuración de Permisos
Para resolver este problema, debes asignar los permisos correctos al directorio en el host, **de modo que coincidan con los identificadores del usuario jenkins dentro del contenedor.**

```bash
sudo chown -R 1000:1000 /directorio/al/jenkins_home
```


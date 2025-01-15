# 📌 Crear un Job
    
1. Hacemos clic en `Nueva Tarea`
En en el panel de control principal, pinchamos en `Nueva Tarea`.
   
![imagen](https://github.com/user-attachments/assets/b22e02f6-a1f6-483b-8844-34428a433948)
    
2. Asignamos un nombre a la tarea y seleccionamos tipo de tarea.

    
![imagen](https://github.com/user-attachments/assets/abf319bc-421b-4327-b270-5d19e2b71352)
        
3. Establecemos parámetros y configuraciones para la tarea.
En este paso configuraremos:
- Comportamiento del proceso de **Build**.
- Configuración del origen del código fuente (_Source code_).
- Disparadores de ejecución (_Triggers_).
- Entorno de ejecución (_Environment_).
- Pasos de construccion (_Build steps_).
- Acciones a ejecutar tras la tarea.

Entre estos parámetros estableceremos una descripción que complemente el nombre de la tarea, teniendo en cuenta que en futuro podremos necesitar identificar exactamente que operaciones realiza la tarea y en qué orden las ejecuta.
       
![imagen](https://github.com/user-attachments/assets/49cd34a7-8795-48c1-a9ab-860305e6826b)
      
Configuramos una acción de saludo por terminal.
    
![imagen](https://github.com/user-attachments/assets/acb543e4-a585-41ed-8bcd-814a4ea7f0f8)
    
4. Comprobamos el éxito de la operación.
Para comprobar el éxito de la operación pinchamos en `Panel de Control` 
    
![imagen](https://github.com/user-attachments/assets/3023b99f-27be-448b-a36d-ae8b728b016e)
     
Aparecerá la tarea en la lista de tareas.
    
![imagen](https://github.com/user-attachments/assets/917b9481-bb19-4e9f-95a7-fc8a67cf23de)

Al hacer click sobre la tarea, entramos en la vista dedicada. Aquí podremos hacer click sobre `Construir Ahora`, y veremos aparecer un listado de ejecuciones de la tarea.
![imagen](https://github.com/user-attachments/assets/376a6343-97d1-4af5-900d-d1858792369f)
   
Pinchando sobre una de las ejecuciones podremos ver el resultado de su ejecución.   
![imagen](https://github.com/user-attachments/assets/c5684f73-1da1-43a6-8761-e5320582b6ec)





# 📌 Uso de variables en Jobs.
En los scripts que escribimos para las tareas de Jenkins podemos hacer uso de variables y variables de entorno de la terminal que el servicio emplea.

#### 🧮 Ejemplo de uso.   
En la sección ejecutar escribimos nuestro script, declarando una variable personalizada que a su vez invoca la variable `DATE` con el switch `%r`.

```bash
AHORA=$(date + "%r)
echo "La hora actual es: $AHORA" > /tmp/ahora
```   
   
**Ejemplo en tarea**.
   
![image](https://github.com/user-attachments/assets/f1ece043-bd30-4be5-ad6b-803c5a6bec91)
    
**Salida de la consola**.
    
![image](https://github.com/user-attachments/assets/a6b7a69f-4233-4471-96af-4fd88a50b3a2)


# 📌 Ejecución de Scripts desde el contenedor Docker.
Con Jenkins podemos hacer uso de scripts que hayamos definido y almacenado en el contenedor Docker que sostiene el servicio. Para hacer esto, el proceso normal es el siguiente:
1. Crear un script o 'fichero guión'.
2. Otorgar permisos de ejecución al fichero.
3. Copiar el fichero en el contenedor docker.
4. Invocar el script desde la tarea de Jenkins.
   
   
#### 🧮 Ejemplo de creación y ejecución.
Como primer paso creamos un script de bash, en este caso un simple bucle.
```bash
#!/bin/bash

nombre="David Jason"
curso="Jenkins"

# Inicio del loop.
for i in 1 2 3 4 5 6 7 8
do
    if [ $i -eq 8 ]
    then
        sleep 10
        echo "A descansar de clase $nombre."
    fi
    echo "Clase Nº $i"
done
echo "Las clases han terminado."
```

A continuación otorgamos los permisos de ejecución sobre el script.
```bash
chmod +x script.sh
```

Ahora deberemos copiar nuestro fichero en el contenedor Docker para que este pueda ejecutarlo.   
Para ello usaremos el siguiente comando con la siguiente sintaxis:    
`docker cp <nombre script> <nombre contenedor>:<ubicacion> `  

```bash
docker cp script.sh mi-jenkins:/opt
```

**Qué hace exactamente el comando?**   
El comando `docker cp script.sh mi-jenkins:/opt`  se utiliza para copiar un archivo del sistema host a un contenedor Docker en ejecución.

En este caso:
- `docker cp`: Es el comando de Docker para copiar archivos o directorios entre el sistema host y un contenedor.
- `script.sh`: Es el archivo que deseas copiar, que se encuentra en el sistema host.
- `mi-jenkins`: Es el nombre (o ID) del contenedor de Docker en el que deseas copiar el archivo.
- `/opt`: Es el directorio dentro del contenedor jenkins donde deseas copiar script.sh.

Así que, este comando copiará el archivo script.sh desde tu sistema host al directorio /opt dentro del contenedor jenkins.


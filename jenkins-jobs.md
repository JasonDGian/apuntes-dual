# 📌 Crear un Job o tarea.
    
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





# 📌 Uso de variables en tareas.
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
##### 1. Creamos un fichero guión o script.
>
>```bash
>#!/bin/bash
>
>nombre="David Jason"
>curso="Jenkins"
>
># Inicio del loop.
>for i in 1 2 3 4 5 6 7 8
>do
>    if [ $i -eq 8 ]
>    then
>        sleep 10
>        echo "A descansar de clase $nombre."
>    fi
>    echo "Clase Nº $i"
>done
>echo "Las clases han terminado."
>```

##### 2. Otorgamos los permisos de ejecución sobre el script.
>```bash
>chmod +x script.sh
>```

##### 3. Copiamos nuestro fichero en el contenedor Docker para que este pueda ejecutarlo.   
>Para ello usaremos un comando con la siguiente sintaxis:    
>`docker cp <nombre script> <nombre contenedor>:<ubicacion> `  
>
>```bash
>docker cp script.sh mi-jenkins:/opt
>```
   
##### 4. Creamos una tarea que invoque el script que hemos creado.   
>Simplemente se trata de invocar el script desde la sección de **Ejecutar linea de comandos** de la tarea Jenkins.
>    
>![image](https://github.com/user-attachments/assets/81779c1e-5cf1-4bb2-aab1-90aa72a3009f)
>

# 📌 Sesiones de ejecución de Jenkins.
Cuando una tarea de Jenkins ejecuta instrucciones en la terminal de Shell, eso supone una sesión de ejecucion. Cuando en esta sesión de ejecución de tarea se invoca un script almacenado, este script lanzará una nueva sesión. Esto dará resultado a dos sesiones de ejecución distintas que no comunican entre ellas, de modo que las variables que una sesión exporta no serán visibles por la otra. Cada script lanzado independiente supondrá una sesión distinta.
   
![image](https://github.com/user-attachments/assets/8bf094b6-d5e3-4736-ad9e-095aa56fb537)

<!-- ## Esto NO funcionará.
![image](https://github.com/user-attachments/assets/0ce2ca27-88f7-46d8-b9ae-97a6f86c52f9)
-->

## 📍 Recibiendo valores paramertizados en scripts.
Para resolver el problema de la no-comunicación entre sesiónes, en los scripts que vamos a almacenar en el contenedor, podemos configurar parametros de entrada. Al definir parametros de entrada podremos pasar los valores definidos en una sesión a un script para que este los pueda emplear en su propria sesión.
   
**Para hacerlo seguimos la sintaxis**:   
```bash
#!/bin/bash

# Parametro de entrada 1 - para el nombre.
nombre=$1
# Parametro de entrada 2 - para el curso.
curso=$2

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

#Final del script.
```

#### 🧮 Ejemplo de incovación con parametros.
En ese ejemplo invocamos el script pasandole dos variables que asignamos en la sesión inicial de la tarea de Jenkins.
![image](https://github.com/user-attachments/assets/d81dd79c-048d-4479-ba08-676085a24826)










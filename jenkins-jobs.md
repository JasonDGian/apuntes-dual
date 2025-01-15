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
   
---  
    
# 📌 Tareas de ejecución de Scripts desde el contenedor Docker.
Con Jenkins podemos hacer uso de scripts que hayamos definido y almacenado en el contenedor Docker que sostiene el servicio.    
Para hacer esto, el proceso normal es el siguiente:
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




    
---   
    


# 📌 Uso de variables en tareas y scripts.
Existen dos tipos de variables que podemos usar en las tareas. 
1. Variables de entorno.
2. Variables de sesión.
     
Para poder hacer uso de las variables correctamente es conveniente comprender como funciona el entorno de ejecución y las sesiones de ejecución.

## 📍 Sesiones y Entorno de ejecución de Jenkins.
Cuando una tarea de Jenkins ejecuta instrucciones en la terminal de Shell, se crea una sesión de ejecución dentro del entorno. Al invocar un script almacenado en esta sesión, se lanza una nueva sesión dentro del mismo entorno. Esto da como resultado dos sesiones de ejecución distintas que no se comunican entre ellas, de modo que las variables de una sesión no serán visibles para la otra. Cada script lanzado independientemente crea una sesión distinta.   
  
Existen un tipo de variables llamadas `Variables de entorno` que transcienden las sesiones de ejecucion y son accesiblas por todas ellas. Fungen de "valores globales" que todas las sesiones pueden consultar.

![image](https://github.com/user-attachments/assets/2051bda1-63d9-46fe-b205-aec713d3f1df)

<!-- ![image](https://github.com/user-attachments/assets/ad230934-fd59-4bfa-8afa-097dbf939a1c) -->


## 📍 Comunicar valores de una sesión a otra.
Si queremos definir variables en una sesión y que estas puedan ser utilizadas en otra (por ejemplo; definir una variable y utilizar su valor en un script) podemos hacerlo de dos maneras.
- Exportando la variable al entorno de ejecución.
- Pasando las variables como parametros al script.

### 🔸 Exportar variables al entorno.
Para exportar variables al entorno de ejecución definiremos las variables de manera habitual, pero añadiremos la palabra clave `export` como prefijo.
   
**Ejemplo:**
```bash
export nombre="David"
export curso="Jenkins"
```

**Esto NO funcionará.**    
>Variables locales de sesión no parametrizadas.
>![image](https://github.com/user-attachments/assets/0ce2ca27-88f7-46d8-b9ae-97a6f86c52f9)

**Esto SI funcionará**    
>Variables exportadas a entorno.
>![image](https://github.com/user-attachments/assets/792d64e7-7bb4-4a13-85b5-79ada42e69ea)
   
   
### 🔸 Pasar las variables como parametro.
En los scripts que vamos a almacenar en el contenedor Docker, podemos configurar parametros de entrada para que este pueda recibir valores de otras sesiones y los pueda emplear en su propria sesión.
   
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

#### 🧮 Ejemplo de invocación con parametros.
En ese ejemplo invocamos el script pasandole dos variables que asignamos en la sesión inicial de la tarea de Jenkins.
![image](https://github.com/user-attachments/assets/d81dd79c-048d-4479-ba08-676085a24826)



<!--



----  

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




-->

# 📌 Tareas parametrizadas en Jenkins.
Las tareas parametrizadas en Jenkins pueden recibir valores de entrada que luego se asignan como variables de entorno dentro del entorno de ejecución de la tarea. Esto permite que los scripts y comandos dentro de la tarea utilicen estos valores, proporcionando flexibilidad y personalización en la ejecución de las tareas.

![image](https://github.com/user-attachments/assets/19b6e626-c999-41a3-b12e-da0cf67a210b)

## 📍 Como configurar los parametros de una tarea.
Para que una tarea de Jenkins esté parametrizada, durante su configuración debemos activar la opción `Esta ejecución debe parametrizarse`.
   
![image](https://github.com/user-attachments/assets/021246a4-ea3f-49dd-909a-e463aa7680aa)

Al activar la opción y seleccionar el tipo de parámetro deseado aparecerá el formulario de configuración de parámetro.   
**IMPORTANTE:** El campo `nombre` hace referencia al nombre que recibirá la variable en el entorno de ejecución.
   
![image](https://github.com/user-attachments/assets/6f18901b-f10e-4959-9294-01bdb5fc8501)
   
Una vez rellenado el formulario tantas veces como parametros deseamos configurar, pincharemos en guardar y podremos realizar las pruebas de ejecución.
   
Pinchando en `Build with Parameters` aparecerá la ventana de configuración de parámetros para la ejecución de la tarea con los valores por defecto.   
Aquí es donde introducimos los valores que deseamos para la ejecución que vamos a lanzar.
![image](https://github.com/user-attachments/assets/a8f078e3-4505-4c83-9fbd-6ebf6ab1f4c4)

Este tipo de ejecución es mucho mas efectivo que modificar las variables en la terminal cada vez que deseamos probar valores distintos.
![image](https://github.com/user-attachments/assets/95507fbf-aa70-4c90-9b2b-f86620e0e20c)

<!-- ## 📍 Tipos de parametros.
Al parametrizar las teareas podemos seleccionar distintos tipos de parametros.
- Cadena de texto: El usuario debe introducir el texto a mano.
- Seleccion de valores: El usuario elige un valore de un listado.
- 

-->

# 📌 Integración de Jenkins con Github y Maven.
 Los pasos que vamos a seguir para realizar este proceso son los siguientes:
 1. Instalación de plugins y configuración.
 2. Pull del repositorio de Maven en Jenkins.
 3. Realizar el _build_ (compilación) de la aplicación.
 4. Realizar tests sobre el _build_.
 5. Desplegar la aplicación.
 
 ## 📍 Instalación de plugins y configuración.
 Antes de comenzar debemos instalar el plug-in de Github y de Maven para luego configurarlos.
 Para ello vamos al panel lateral izquierdo y pinchamos en `Administrar Jenkins`.
    
 ![image](https://github.com/user-attachments/assets/7d744485-ab38-4deb-b473-0014ae5de7c6)

Esto nos llevará a un nuevo panel donde pincharemos en `Administrar Plugins`.
    
![image](https://github.com/user-attachments/assets/2c56252e-9efd-41ce-b605-b27e84fcb023)
    
A continuación consultaremos en la pestaña de `Plugins instalados` si aparece el plugin de "_Github Branch Source Planning_", de no aparecer usaremos la pestaña `Todos los plugins` y lo instalaremos.
    
![image](https://github.com/user-attachments/assets/ea144442-b0ab-4928-9cb4-6188b910ebbf)

Ahora repetimos el proceso para el plugin de **Maven**.
    
![image](https://github.com/user-attachments/assets/f24ef6bc-8880-4368-80b7-9131a3063e78)

Al pinchar en instalar aparecerá la siguiente pantalla. En ella activamos la opción de reiniciar al terminar la instalación.
    
![image](https://github.com/user-attachments/assets/0e5f2548-6c21-4cad-80ea-3104d706ab22)

Ahora debemos configurar el plugin de Maven para Jenkins. Vamos al panel lateral izquierdo y pinchamos en `Administrar Jenkins` luego en `Herramientas de configuración global`.
     
![image](https://github.com/user-attachments/assets/02e85234-9fff-4f64-9199-81a98de0ee30)
    
En la página buscaremos la entrada para **Maven** y pincharemos en `Añadir Maven`, activaremos la opción `Instalar automaticamente` y dejaremos la última versión configurada.
    
![image](https://github.com/user-attachments/assets/da17a677-2c13-41dc-8aa0-20b527c3108f)

 ## 📍 Hacer pull de un repositorio de GitHub.
Creamos una nueva tarea, y seleccionamos el tipo de tarea de estilo libre.
    
![image](https://github.com/user-attachments/assets/572e7d23-f935-4f3a-9fe1-64acc923a64b)
    
![image](https://github.com/user-attachments/assets/f502586e-e98b-48a9-8850-d22587fcca51)
   
     
En la pestaña de configuración general de la tarea buscamos la sección de **Configurar el origen del código fuente**.      
Aquí seleccionamos `Git` como opción de origen y configuramos los parametros necesarios.
- URL de repositorio.
- Credenciales (para repositorios privados)
- Branch
       
![image](https://github.com/user-attachments/assets/40909841-7c96-4f38-9fdf-351d44737169)


 #### 🔸 Comprobación del éxito de la operación pull.
 Para comprobar que la tarea es capaz de clonar el repositorio vamos a lanzarla y a consultar el output de la consola.
      
![image](https://github.com/user-attachments/assets/e24a0c3c-6650-4f9b-8c80-b839c6d292fe)


 ## 📍 Realizar el _build_ de la aplicación.
 Volviendo a la tarea que estamos configurando, en la sección **Ejectuar**, pinchamos en **`Añadir nuevo paso`** y seleccionamos **`Ejecutar tareas 'maven' de nivel superior`**.    
    
 ![image](https://github.com/user-attachments/assets/fe32c395-9970-4b0c-82d8-828667b87b77)

En el formulario emergente deberemos introducir dos datos.
- El nombre de la instalación que hemos hecho con maven en el paso 1 de esta guía, en mi caso será _`mavenjenkins`_.
- El **`goal`** (objetivo) de Maven que deseamos para la ejecución.    

>[!Tip]
>Un "_goal_" u _objetivo_ en Maven es una acción específica que se ejecuta como parte del ciclo de vida de construcción de un proyecto.
  
>[!IMPORTANT]
> Al configurar los "goals" (objetivos) de Maven en Jenkins, no debemos inclur el prefijo `mvn`. Esto sucede porque Jenkins ya sabe que estamos trabajando con maven y no deberemos volver a indicar que el comando que estamos introduciendo se trata de un comando maven. 
    
![image](https://github.com/user-attachments/assets/297a1e79-0672-48a3-bf01-b58e7b1874df)
   
#### 🔸 **Acerca del comando `mvn -B clean -DskipTests package`**    
El comando utilizado en el ejemplo anterior es un comando compuesto por 4 instrucciones. 
- `-B`: Ejecuta Maven en modo no interactivo para entornos automatizados.
- `-DskipTests`: Compila el código fuente y salta la ejecución de tests.
- `clean`: Limpia los archivos de construcción anteriores.
- `package`: Empaqueta el código compilado en un archivo distribuible.
    
Esto nos permitirá obtener el artefacto final rápidamente, omitiendo la fase de pruebas. El artefacto generado será un archivo empaquetado listo para su ejecución o despliegue, aunque necesitará el comando `java -jar` para ser ejecutado si es un archivo JAR, o ser desplegado en un servidor de aplicaciones si es un archivo WAR.
      
Una vez configurado el paso de _build_ procedemos a configurar las notificaciones.   
Pinchamos en **`Acciones para ejecutar después`** y seleccionamos el tipo de notificación deseada.    
    
![image](https://github.com/user-attachments/assets/af4a1094-6f0d-4ccd-8eaa-3ae04e1fb2a4)
    
Activamos las configuraciones de notificacion para los fallos y para la 'vuelta a la normalidad' y pinchamos en **`Guardar`**.    
![image](https://github.com/user-attachments/assets/6d403e92-cc24-4ac5-a8d7-c8ef893dc8b1)

   
## 📍 Realizar pruebas unitarias.
 Volviendo a la tarea que estamos configurando, en la sección **Ejectuar**, pinchamos en **`Añadir nuevo paso`** y seleccionamos **`Ejecutar tareas 'maven' de nivel superior`**.    
    
![image](https://github.com/user-attachments/assets/e2d3024b-46f9-4a4f-8b9e-1b6dd30a5bae)

Introducimos la instalación de maven que deseamos emplear para el paso y como goal introducimos `test` para indicar que se trata de un `mvn test`.    
    
![image](https://github.com/user-attachments/assets/b30e49d4-47bc-4af1-8f27-a41ce53da38e)

Nos deberá quedar así.
![image](https://github.com/user-attachments/assets/e2a89efa-6613-4d92-aeb6-3bee7057e0ee)

Ejecutando la tarea, veremos que ahora dispone de un paso más que es el paso de TESTS.    
     
![image](https://github.com/user-attachments/assets/acc45188-b66a-4e36-abaf-d13d008351d1)

#### 🔸 Configuración de la Generación de Informes XML para Resultados de los Tests.
En Jenkins, es posible configurar una salida gráfica muy útil para visualizar los resultados de los tests de aplicaciones Maven. Para hacerlo, primero necesitamos saber dónde nuestra aplicación almacena los resultados de los tests. Para averiguarlo, debemos ejecutar la tarea en Jenkins y buscar el output correspondiente en la consola.
    
![image](https://github.com/user-attachments/assets/e42d9396-8b1c-48b1-964d-1c5f033f4986)
    
Con esta ruta como referencia, volvemos a la configuración de la tarea y en la sección **`Ejecutar después`** añadiremos una nueva acción seleccionando **`Publicar los resultados de tests JUnit`**.     
     
![image](https://github.com/user-attachments/assets/5deab1ab-98ae-4e1a-937b-abecc66f466d)

Introducimos la ruta **relativa** donde se almacenan los informes en formato **`.xml`** y le indicamos que recoja todos los ficheros con esa extensión.
![image](https://github.com/user-attachments/assets/c243c470-f211-4281-8f4f-0b843a493b48)

A partir de ahora, al ejecutar la tarea configurada, nos aparecerá la opción para visualizar los resultados.
    
![image](https://github.com/user-attachments/assets/bfe5ed1d-bca5-4420-b6ec-53fb09a029e3)
    
#### 🔸 **Acerca del comando `mvn test`**
Este comando se encarga de escanear el proyecto, encontrar los tests y ejecutarlos.

## 📍 Realizar despliegue de la aplicación.
Cada vez que realizamos la compilación, se generará un nuevo artefacto en la ruta configurada o por defecto de proyecto. En mi caso la ruta es **`/var/jenkins_home/workspace/Java App con Maven/target`** (dentro del contenedor Docker que hospita el servicio Jenkins).  

Volviendo a la tarea que estamos configurando, en la sección **Ejectuar**, pinchamos en **`Añadir nuevo paso`** y seleccionamos **`Ejecutar linea de comandos`**.    
En el formulario de texto introducimos la instrucción **`java -jar [ruta/artefacto]`** para la ejecución. Es además buena idea introducir una instrucción **`echo`** con un mensaje reconocible para facilitar la identificacion de este paso en la salida de la consola.

![image](https://github.com/user-attachments/assets/7a40e11d-bd75-4ad4-85ef-b6e586ee2292)

![image](https://github.com/user-attachments/assets/2e71bc6c-b072-4fd4-8172-8c300da307ff)

#### 🔸 Guardar la ultima ejecución exitosa.
En Jenkins podemos almacenar y guardar la última ejecución del proyecto que se ejecutó sin dar fallos. Para configurar esta funcionalidad vamos a la tarea y en **`Acciones para ejecutar después`** y hacemos clic en **`Añadir una acción`** y seleccionamos **`Guardar los archivos generados.`**.
   
![image](https://github.com/user-attachments/assets/696799e1-d16c-4161-ab3d-f85bc8b29dd1)

Pinchamos en **`Avanzado`** y especificamos la ruta  donde se compilan nuestros artefactos indicando que deseamos almacenar los ficheros **`.jar`**. Indicamos además que deseamos almacenar solo los artefactos que han sido compilados con éxito.   
    
![image](https://github.com/user-attachments/assets/466f63e5-acba-4fb0-bcd8-f7a1bbe53142)

Una vez configurada esta funcionalidad, si ejecutamos nuestra aplicacion y esta no falla, podremos comprobar como aparece una nueva opción de descarga.    
    
![image](https://github.com/user-attachments/assets/8db5496b-5a58-4544-a7a7-af954be27d39)


 # 📌 Integración de Jenkins con Github y Maven.
 1. Instalar plugins de Github y Maven y configurarlos.
 2. Hacer pull del repositorio de GitHub.
 3. Configurar las tareas a ejecutar tras el pull.

 ## 📍 Instalación de plugins y configuración.
 Antes de comenzar debemos de instalar el plug-in de Github y de Maven para luego configurarlos.
 Para ello vamos al panel lateral izquierdo y pinchamos en `Administrar Jenkins`.
    
 ![image](https://github.com/user-attachments/assets/7d744485-ab38-4deb-b473-0014ae5de7c6)

Esto nos llevará a un nuevo panel donde pincharemos en `Administrar Plugins`.
    
![image](https://github.com/user-attachments/assets/2c56252e-9efd-41ce-b605-b27e84fcb023)
    
A continuación consultaremos en la pestaña de `Plugins instalados`si aparece el plugin de "_Github Branch Source Planning_", de no aparecer usaremos la pestaña `Todos los plugins` y lo instalaremos.
    
![image](https://github.com/user-attachments/assets/ea144442-b0ab-4928-9cb4-6188b910ebbf)

Ahora repetimos el proceso para el plugin de **Maven**.
    
![image](https://github.com/user-attachments/assets/f24ef6bc-8880-4368-80b7-9131a3063e78)

Al pinchar en instalar aparecerá la siguiente pantalla. En ella activamos la opción de reiniciar al terminar la instalación.
    
![image](https://github.com/user-attachments/assets/0e5f2548-6c21-4cad-80ea-3104d706ab22)

Ahora debemos de configurar el plugin de Maven para Jenkins. Vamos al panel lateral izquierdo y pinchamos en `Administrar Jenkins` luego en `Herramientas de configuración global`.
     
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


 ### 🔸 Comprobación del éxito de la operación pull.
 Para comprobar que la tarea es capaz de clonar el repositorio vamos a lanzarla y a consultar el output de la consola.
      
![image](https://github.com/user-attachments/assets/e24a0c3c-6650-4f9b-8c80-b839c6d292fe)


 ## 📍 Ejecutar tareas tras el pull.
 

      



    

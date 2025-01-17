# 📌 Jenkins Pipeline.
Jenkins pipeline nos permite escribir los pasos o `steps` de las pipelines en forma de código.

**¿Qué es una pipeline?**    
Una pipeline en Jenkins es una secuencia de eventos o trabajos que se ejecutan en un orden específico. Se puede visualizar como una serie de etapas, donde cada etapa contiene una serie de pasos.     
    
- **Etapa:**    
Un bloque que contiene una serie de pasos. Puede tener cualquier nombre y se utiliza para visualizar el proceso de la pipeline.
   
- **Paso:**    
Una tarea que define qué hacer. Los pasos se definen dentro de un bloque de etapa.
     
Por ejemplo, una pipeline podría tener etapas como "Construir", "Probar" y "Desplegar", y cada una de estas etapas contendría pasos específicos para realizar las tareas necesarias
     
![image](https://github.com/user-attachments/assets/a717257f-de34-4cdb-80a2-0099a43723c2)

## 📍 Tipos de Pipelines en Jenkins - Pipeline Declarativa.
La pipeline declarativa en Jenkins utiliza una sintaxis más estructurada y fácil de leer, lo que facilita la creación y el mantenimiento de pipelines complejos.
    
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
```    

## 📍 Tipos de Pipelines en Jenkins - Pipeline Guinizada o Scripted Pipepline.
La pipeline scripted ofrece mayor flexibilidad y control, pero a cambio de una mayor complejidad en la lectura y mantenimiento.
    
```groovy
node {
    stage('Build') {
        echo 'Building...'
    }
    stage('Test') {
        echo 'Testing...'
    }
    stage('Deploy') {
        echo 'Deploying...'
    }
}
```
**En resumen:**
- **Declarative Pipeline:** Más sencilla y estructurada, ideal para la mayoría de los casos y equipos grandes.
- **Scripted Pipeline:** Más flexible y poderosa, adecuada para casos que requieran lógica personalizada o flujos complejos.


# 📌 Crear una pipeline.
Para crear una pipeline lo primero que haremos será comprobar si el plugin de pipelines está instalado, de no estarlo deberemos proceder a instalarlo antes de poder continuar.
    
![image](https://github.com/user-attachments/assets/53e5fe86-5405-4dfe-8537-a7dbd9222445)
     
Vamos a crear una nueva tarea, le asignaremos un nombre y seleccionaremos tipo de tarea `Pipeline`.
     
![image](https://github.com/user-attachments/assets/1563581b-984d-43c3-a8ff-6887e07d4a37)

Las opciones de este tipo de tarea son muy parecidas a una tarea de estilo libre, pero en lugar de tener un apartado de `Ejecutar` tendrá una apartado de `Pipeline`. En este apartado podremos definir un script de acciones
manualmente en el contenedor de texto o podemos invocar un script desde un administrador de código fuente.
     
![image](https://github.com/user-attachments/assets/9935e6b0-ecd4-4182-a729-ee3e964379a0)
   
> **Ejemplo de script 'manual'**
>     
> ![image](https://github.com/user-attachments/assets/79833f71-4c2f-462c-ab63-6649175c2fb3)
>
> Pinchando en construir ahora podremos obtener los resultados.
> ![image](https://github.com/user-attachments/assets/d14ea9c3-5bc0-49ac-bdf0-b2a75794b45c)


>[!NOTE]
>Cuando queremos ejecutar mas de un paso dentro de una etapa usaremos una sintaxis distinta. En el caso de tener distintos comandos shell usaremos la siguiente sintaxis.
>```shel
>sh 'echo "mi comando"'
>sh '''
>    echo "mi segundo comando"
>'''
>```
>     
>![image](https://github.com/user-attachments/assets/420c10e3-93ca-4195-84b8-37e9f2f82428)

## 📍 Etapas paralelas y secuenciales.
Cuando utilizamos las Pipelines declarativas.

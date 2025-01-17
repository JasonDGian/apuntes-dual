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

## 📍 Tipos de Pipelines en Jenkins.
En Jenkins, existen dos tipos principales de pipelines que podemos utilizar para definir y automatizar el flujo de trabajo:

### 🔸 Pipeline Declarativa.
La pipeline declarativa en Jenkins utiliza una sintaxis más estructurada y fácil de leer, lo que facilita la creación y el mantenimiento de pipelines complejos.
- Es ideal para la mayoría de los casos y equipos grandes debido a su simplicidad y claridad.
         
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

### 🔸 Pipeline Guionizada o Scripted Pipepline.
La pipeline scripted ofrece mayor flexibilidad y control, pero a cambio de una mayor complejidad en la lectura y mantenimiento.
- Es adecuada para casos que requieran lógica personalizada o flujos complejos.
        
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

## 📍 El fichero Jenkinsfile.
En Jenkins, podemos crear un archivo llamado `Jenkinsfile`. Este archivo se coloca en la raíz de tu proyecto, y Jenkins lo utiliza para configurar y ejecutar la pipeline. Al incluir el Jenkinsfile en tu repositorio de código, puedes versionar y gestionar tu flujo de trabajo junto con el código del proyecto, lo que facilita la colaboración y el mantenimiento.


El Jenkinsfile se escribe en **`Groovy`**, un lenguaje de programación dinámico que se ejecuta en la máquina virtual de Java (JVM). Groovy es flexible y permite escribir código de forma concisa y expresiva, lo que lo hace adecuado para definir las pipelines en Jenkins de manera clara y estructurada.
     
Tanto la pipeline declarativa como la scripted en Jenkins se escriben utilizando Groovy. La diferencia principal radica en la estructura y la sintaxis que cada tipo de pipeline emplea, pero ambos utilizan el mismo lenguaje subyacente.

## 📍 Etapas paralelas y secuenciales.
Cuando utilizamos las Pipelines declarativas podemos especificar comportamientos relativos al tiempo o modo de ejecución de los pasos y etapas.
Entre los comportamientos que podemos definir están la definición de etapas **secuenciales** y las estapas **paralelas**.

### 🔸 Etapas secuenciales.
Las etapas secuenciales en Jenkins son aquellas que se ejecutan en un orden específico, asegurando que una etapa debe completarse antes de que comience la siguiente. Esta estructura es útil para definir flujos de trabajo que dependen de la finalización exitosa de pasos anteriores.
     
Para definir etapas secuenciales en Jenkins, utilizamos la siguiente sintaxis:
```groovy
pipeline {
    agent any
    stages {
        stage('Estapa secuencial 1') {
            steps {
                // Paso para clonar el repositorio
                git url: 'https://github.com/tu-repositorio.git'
            }
        }
        stage('Estapa secuencial 2') {
            steps {
                // Paso para compilar el proyecto
                sh './gradlew build'
            }
        }
        stage('Estapa secuencial 4') {
            steps {
                // Paso para ejecutar pruebas unitarias
                sh './gradlew test'
            }
        }
        stage('Estapa secuencial 5') {
            steps {
                // Paso para empaquetar el proyecto
                sh './gradlew assemble'
            }
        }
        stage('Estapa secuencial 6') {
            steps {
                // Paso para desplegar el proyecto
                sh 'scp build/libs/tu-app.jar user@server:/ruta/destino'
            }
        }
    }
}
```
    
**Representación visual etapas secuenciales**.
Cada una de estas etapas se ejecutará secuencialmente, asegurando que solo se avance a la siguiente etapa si la etapa actual se completa con éxito.
    
![image](https://github.com/user-attachments/assets/d510edbf-87e6-4a89-a6d9-ee1420dea9f4)


### 🔸 Etapas paralelas.
Las etapas paralelas en Jenkins permiten que múltiples etapas se ejecuten al mismo tiempo, aprovechando la concurrencia para acelerar el proceso de build, prueba y despliegue. Esto es útil cuando tienes tareas que pueden ejecutarse independientemente y en paralelo, como diferentes conjuntos de pruebas o compilaciones para diferentes plataformas.

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Parallel Tests') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests...'
                        // Comando para ejecutar pruebas unitarias
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Running integration tests...'
                        // Comando para ejecutar pruebas de integración
                    }
                }
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
**Ejemplo de estructura**.
![image](https://github.com/user-attachments/assets/09be1cea-7860-4755-ad3d-eed31576b389)

**Ejemplo de orden de ejecución.**
![image](https://github.com/user-attachments/assets/0e2b0d80-52f3-4ba1-9a81-b2c0ee2e04bf)

#### 🔹 Aborto de ejecución paralela.
En las etapas paralelas es posible forzar el aborto de la ejecución completa cuando se produce un fallo.
Para ello debemos introducir la propiedad `failFast` y configurarla a `true`.

**Ejemplo**
```groovy
pipeline {
    agent any
    stages {
        stage('Parallel Stages') {
            failFast true
            parallel {
                stage('Parallel Stage 1') {
                    steps {
                        echo 'Executing Parallel Stage 1'
                        // Simulación de falla
                        error 'Failure in Parallel Stage 1'
                    }
                }
                stage('Parallel Stage 2') {
                    steps {
                        echo 'Executing Parallel Stage 2'
                    }
                }
                stage('Parallel Stage 3') {
                    steps {
                        echo 'Executing Parallel Stage 3'
                    }
                }
            }
        }
        stage('Post-Parallel Stage') {
            steps {
                echo 'This stage runs after the parallel stages'
            }
        }
    }
}
```

## 📍 Timeout y Retry.
Existen unos elementos llamados 'envoltorios' que podemos aplicar a una pipeline, una etapa o a un paso. En el caso de Timeout y Retry permiten gestionar el comportamiento en caso de fallo.

### 🔸 Retry.
Este envoltorio nos otorga un mecanismo para repetir una acción ( pipeline, etapa o paso ), en caso de fallo, un numero determinado de veces. 

### 🔸 Timeout.
El envoltorio o 'wrap' Timeout permite determinar un tiempo limite de ejecución. Si ese tiempo limite viene superado, Jenkins abortará la acción a la que se aplica el envoltorio.

**Ejemplo de retry y timeout**:
```groovy
pipeline {
    agent any
    stages {
        stage('Etapa1') {
            steps {
                retry(3) {
                    // INSTRUCCIÓN QUE SE REINTENTARÁ 3 VECES.
                    sh 'echo "Intentando..."'
                }
                timeout(time: 3, unit: 'MINUTES') {
                    // INSTRUCCIÓN CON LÍMITE DE TIEMPO AQUÍ.
                    sh 'echo "Tiempo limitado a 3 minutos"'
                }
            }
        }
    }
}
```

**También es posible combinar opciones.**
```groovy
pipeline {
    agent any
    stages {
        stage('Etapa1') {
            steps {
                retry(3) {
                    timeout(time: 3, unit: 'MINUTES') {
                         // INSTRUCCIÓN QUE SE REINTENTARÁ 3 VECES CON LIMITE DE TIEMPO.
                         sh 'echo "Intentando en tiempo limitado..."'
                    }
                }
            }
        }
    }
}
```


>[!TIP]
> **Para ver otras opciones de ejecución, consulta la [documentación oficial de jenkins](https://www.jenkins.io/doc/book/pipeline/syntax/#options).**
    
---


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

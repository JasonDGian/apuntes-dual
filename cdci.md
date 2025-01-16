# 📌 Antes de comenzar: ¿Qué es la Integracion continua (CI)?
La integración continua (CI) es una práctica de desarrollo de software que consiste en integrar y verificar automáticamente el código nuevo en un repositorio central varias veces al día. 
Esta práctica permite detectar y corregir errores rápidamente, mejorando la calidad del software y facilitando la colaboración entre desarrolladores.

## 📍 ¿Cómo funciona la integración continua / despiegue continuo?
1. **Trabajo colaborativo:** Los desarrolladores colaboran en una aplicación.
2. **Modificación del código:** Cada desarrollador modifica el código por separado y aplica cambios a diferentes partes de la aplicación.
3. **Envío al repositorio:** Los cambios se envían a un repositorio de código fuente central y compartido (normalmente usando sistemas como Git).
4. **Servidor CI:** El servidor CI clona el repositorio y obtiene el nuevo código.
5. **Construcción del código:** Dentro del servidor, se realiza la construcción (o 'build') del código.
6. **Pruebas unitarias:** Una vez obtenida la construcción, se realizan una serie de pruebas unitarias.
7. **Despliegue en entorno de pruebas:** Si la compilación pasa todas las pruebas, el código se despliega en un entorno de pruebas.
8. **Pruebas de integración y de despliegue:** En el entorno de pruebas, el código pasa por otra batería de pruebas (de integración y de despliegue).
9. **Despliegue en producción:** Si el despliegue de pruebas pasa todas las pruebas con éxito, se despliega en el entorno de producción.

   
![image](https://github.com/user-attachments/assets/36968fbd-905a-44d3-85ac-c3c3489c705a)



    
### 🗒️ Acerca del repositorio central.
En una configuración típica de integración continua (CI), el repositorio de código no reside en el servidor de CI. Generalmente, el repositorio de código está alojado en 
una plataforma de control de versiones como GitHub, GitLab, Bitbucket, o similares. El servidor de CI está configurado para monitorear ese repositorio y, cuando se 
detectan cambios (como commits o pull requests), el servidor de CI clona o extrae el código del repositorio y ejecuta una serie de pruebas y compilaciones automatizadas.

## 📍 ¿Qué beneficios conlleva el uso de integración continua?
La integración continua ofrece múltiples beneficios, entre los que destacan:
- Reducción del tiempo para identificar errores: Permite detectar problemas en las etapas iniciales del desarrollo, lo que facilita una solución rápida y eficiente.
- Ahorro de tiempo en la corrección de errores: Las actualizaciones son más pequeñas y manejables, lo que simplifica el proceso de depuración.
- Menos problemas de integración: Al integrar cambios continuamente, se minimizan los conflictos en el código, lo que contribuye a acelerar la entrega de productos de mayor calidad.

## 📍 Etapas de implementación de integración continua.
La implementación de CI no es un paso único, es un proceso adoptado por la organización de trabajo y para lograrlo deberemos cumplir con las siguientes prácticas.

#### 🔸 Automatizar el proceso de build o compilación. 
Este proceso debe de incluir la construcción de la aplicación y la ejecución de pruebas unitarias que comprueben el estado.   
#### 🔸 Optimizar la 'build' para que se auto-testee
Deben existir pruebas diseñadas y creadas para que su ejecución automatica permita comprobar el estado del proyecto para ver si todo está bien o si hay errores y el resultado sea entregado automaticamente al equipo de desarrollo.
#### 🔸 Manenter un unico repositorio de código fuente.
El equipo de desarrolladores que trabaja en el proyecto, deben de reunir su progreso en un único repositorio central.
#### 🔸 Mantener la visibilidad de eventos.
En el trabajo de equipo, es crucial que todos puedan ver en todo momento 'que está pasando', incluyendo la build, los unit-test, dependencias, o que falla en caso de error.
#### 🔸 Despliegue automatico.
Despliegue sin intervención manual, utilizando herramientas y scripts que automatizan las tareas necesarias. Permite que los equipos puedan entregar actualizaciones de software de manera más rápida, confiable y consistente.

>[!CAUTION]
> En la integración continua, es importante hacer check-in de manera frecuente, **siempre y cuando el código haya sido testeado, no presente errores y la build funcione correctamente**.


# 📌 Antes de comenzar: ¿Qué es el Despliegue Continuo?
El despliegue continuo es una práctica en el desarrollo de software que consiste en automatizar la liberación de cada compilación exitosa al entorno de producción, una vez que ha pasado todas las pruebas necesarias. Esta práctica asegura entregas rápidas, consistentes y confiables, optimizando el flujo de desarrollo.
   
      
![image](https://github.com/user-attachments/assets/c0cf11fc-e539-4727-8506-722ddd290eb6)
     
>[!TIP]
>El conjunto de Integracion Continua con Despliegue continuo se conoce como `CI/CD`
    

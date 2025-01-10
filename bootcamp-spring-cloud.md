# Bootcamp Spring Cloud.

- - - 

# 📌 Microservicios.
Los microservicios surgen como enfogque para desarrollar aplicaciones software como una serie de pequeños servicios interconectados. Entre sus caracteristicas destacan las siguientes:
- Son independientes.
- Pueden comunicarse entre si.
- Se ejecutan de forma autonoma
- Son pequeños y centrados en un servicio concreto.
- Pueden desplegarse sin afectar a los demás.
- Se pueden escribir en distintos lenguajes e interactuar sin problemas.
- Se comunican a través de APIs.

![image](https://github.com/user-attachments/assets/898f4afe-a0da-4dec-9912-0e07071232cb)


## ¿Por que surgen los microservicios?
Los microservicios surgieron como una respuesta a las limitaciones de las arquitecturas monolíticas tradicionales.
- Escalabilidad: Las aplicaciones monolíticas pueden volverse difíciles de escalar a medida que crecen. Los microservicios permiten escalar partes específicas de la aplicación de manera independiente.
- Mantenimiento: En una arquitectura monolítica, un cambio pequeño puede requerir recompilar y desplegar toda la aplicación. Los microservicios facilitan la implementación de cambios y actualizaciones.
- Desarrollo Ágil: Los equipos pueden trabajar en diferentes microservicios de forma paralela sin interferir unos con otros, lo que acelera el desarrollo.
- Flexibilidad Tecnológica: Permiten utilizar diferentes tecnologías y lenguajes de programación para diferentes microservicios según las necesidades específicas.
- Tolerancia a Fallos: Si un microservicio falla, no afecta a toda la aplicación, mejorando así la resiliencia.

  ![image](https://github.com/user-attachments/assets/39b5a552-eeef-4a71-8a72-03f24f4e8856)

![image](https://github.com/user-attachments/assets/b0c66188-bd0e-45e5-a8ef-d63473176f2a)


# 📌 Servicio de registro y autodescubrimiento.
**Spring Cloud Netflix Eureka**   
El concepto de servicio de registro y autodescubrimiento está presente en entornos distribuidos. Este concepto implica la creación de un servicio cuya único cometido es la de mantener el registro de todos los microservicios que son desplegados o eliminados. Para facilitar la implementación de este servicio, Spring Cloud pone a disposición el componente Spring Cloud Netflix Eureka.​

​

Eureka es un servicio rest que permite al resto de microservicios registrarse en su directorio. Esto es muy importante, ya que no es Eureka quien registra los microservicios, 
sino los microservicios los que solicitan registrarse en Eureka. Cuando un microservicio registrado en Eureka arranca, envía un mensaje a Eureka indicándole que está disponible. 
El servidor Eureka almacenará la información de todos los microservicios registrados así como su estado. Eureka también ofrece al resto de microservicios la posibilidad de "descubrir" y acceder al resto de microservicios registrados.

Como ejemplo de la utilidad que aporta Spring Cloud Netflix Eureka, supongamos una situación en la que existe un Microservicio 1 (MS1) que tiene que comunicarse con un Microservicio 2 (MS2):​
![image](https://github.com/user-attachments/assets/2f11e010-08ec-4b73-a8f6-c7f2a9cba386)

Supongamos que, por algún motivo, MS2 ha cambiado de IP y puerto, siendo ilocalizable desde ese momento para MS1. ¿Podría MS1 conocer la nueva dirección de MS2 de manera automática?
![image](https://github.com/user-attachments/assets/761bbc8b-ed89-4a63-b916-9ff542c3ac9d)

MS1 sí podría conocer automáticamente la nueva dirección de MS2 gracias a Eureka:​
1. Lo primero que MS2 haría sería registrarse en el servidor de Eureka (Eureka Server), proporcionando su nombre, IP, puerto y el estado en el que se encuentra (UP o DOWN).​
2. Antes de que MS1 realice una llamada a MS2, MS1 buscará la información de MS2 en el registro de Eureka, lo que le permitirá comunicarse con MS2 incluso si éste cambia su localización, mientras siga registrado en Eureka Server. ​
3. A continuación, Eureka responderá a MS1 con la información solicitada. ​
4. En ese momento MS1 obtendrá la dirección de MS2 y podrá comunicarse con él.​

Es relevante destacar que, al registrarse o buscar en Eureka, el microservicio pasa a ser cliente (Eureka Client).


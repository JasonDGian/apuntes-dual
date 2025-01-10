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

![image](https://github.com/user-attachments/assets/93fb218b-f0e4-4162-8231-132a7b0406ee)   

Es relevante destacar que, al registrarse o buscar en Eureka, el microservicio pasa a ser cliente (Eureka Client).

**La consola de Eureka (localhost:8761) permite acceder a información de los microservicios desplegados:​**
   
![image](https://github.com/user-attachments/assets/2210f87c-2ad5-4ae7-820a-f406840b9424)

## Pasos practicos.
En esta práctica se creará un servicio Eureka, que se usará para registrar nuestros primeros microservicios.​

El primer paso para crear un servicio Eureka será generar un proyecto Spring Boot desde la web de Spring:​
    
![image](https://github.com/user-attachments/assets/941a9ba5-416b-4f3e-9bc9-e9c895e78edb)

Tras descomprimir el archivo generado, se debe de llevar a nuestro workspace. A continuación, se importará desde Eclipse como un “Existing Maven Project”. Una vez importado, se deberán incluir las propiedades y dependencias necesarias en el fichero pom.xml:​

1. Comenzamos incluyendo las siguientes propiedades dentro de la etiqueta <properties>:​

```xml
<properties>​

    <java.version>11</java.version>​

    <spring-cloud.version>2021.0.0</spring-cloud.version>​

</properties>​
```
    
2. Seguidamente, se debe incluir la dependencia de Eureka bajo la etiqueta <dependencies>:​
    
```xml
<dependency>​

    <groupId>org.springframework.cloud</groupId>​

    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>​

</dependency>​
```

3. Se continúa con la configuración del pom.xml añadiendo un nuevo bloque <dependencyManagement>, que podemos ubicar después del bloque <dependencies> (no dentro) y antes de la etiqueta de apertura del bloque <build>:​ 
      
```xml
<dependencyManagement>​

    <dependencies>​

        <dependency>​

            <groupId>org.springframework.cloud</groupId>​

            <artifactId>spring-cloud-dependencies</artifactId>​

            <version>${spring-cloud.version}</version>​

            <type>pom</type>​

            <scope>import</scope>​

        </dependency>​

     </dependencies>​

</dependencyManagement>​
```
     
Finalmente, el fichero pom.xml debe tener este aspecto:​
   
  ![image](https://github.com/user-attachments/assets/0e4b6536-dbff-4067-800b-c2a59a08c889)
   
A continuación, compilamos el proyecto lanzando una Maven Build (clean install).​
    

4. El servicio Eureka debe incluir la notación @EnableEurekaServer en la clase principal, es decir, en la clase  EurekaServiceApplication:​
```java
@EnableEurekaServer​
@SpringBootApplication​
public class EurekaServiceApplication {​
    public static void main(String[] args) {​
        SpringApplication.run(EurekaServiceApplication.class, args);​
    }​
```

5. Seguidamente, se renombrará el fichero de configuración application.properties, que pasará a tener el nombre application.yml:​


6. En el fichero de application.yml se incluirá la siguiente configuración para Eureka:​
```yml
spring:​
  application:​
    name: eureka-server​

server:​
  port: 8761​

eureka:​
  client:​
    #telling the server not to register himself in the service registry​
    registerWithEureka: false​
    fetchRegistry: false​
    serviceUrl:​
      defaultZone: http://localhost:8761/eureka​
```

Después de guardar la configuración anterior, debemos lanzar una Maven Build (clean install) y después levantar de manera normal nuestro proyecto de Spring (Run). En la configuración hemos definido que el servicio se levantará en el puerto 8761, por lo que una vez levantado, debemos abrir un navegador web y acceder a la dirección: http://localhost:8761​

Si todo ha ido bien, se deberá visualizar en el navegador la consola de Eureka:​
    
![image](https://github.com/user-attachments/assets/753d2b7f-09bd-4192-8033-0a4772d64a23)
      
Más información y referencias sobre la creación y configuración de un servicio Eureka:​
- https://docs.spring.io/spring-cloud-netflix/docs/2.2.5.RELEASE/reference/html/#service-discovery-eureka-clients
- https://spring.io/guides/gs/service-registration-and-discovery/​

Tras haber creado un servicio Eureka, crearemos nuestro primer microservicio y veremos cómo se registran y se visualizan en Eureka los registros desplegados.​



     



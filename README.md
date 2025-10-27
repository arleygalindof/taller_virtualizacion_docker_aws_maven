# Taller AYGO - Virtualización Docker AWS Maven 📘 - Arley Galindo Forero

#

*Taller AYGO - Arquitectura y Gobernabilidad Tecnológica*

## 🧩 Descripción general

*Este taller contiene un proyecto simple de Java con el framework Spring que usa Docker file y docker compose y ha sido subido a un contenedor alojado en AWS*

---

## ⚙️ Tecnologías utilizadas
- Java 17  
- Spring Boot  
- Maven  
- Docker  
- AWS EC2  
- GitHub  

Script controlador

```
//Clase controlador
package edu.escuelaing.aygo.container;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class HelloRestController {
    private static final String template = "Hello, %s!";
    @GetMapping("/greeting")
    public String greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
        return String.format(template, name);
    }
}
```
Script servicio REST
```
//Clase para iniciar Spring
package edu.escuelaing.aygo.container;

import static java.util.Collections.singletonMap;
 
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class RestServiceApplication {
    public static void main(String[] args) {
        SpringApplication app = new SpringApplication(RestServiceApplication.class);
        app.setDefaultProperties(singletonMap("server.port", getPort()));
        app.run(args);
    }
    private static int getPort() {
        if (System.getenv("PORT") != null) {
            return Integer.parseInt(System.getenv("PORT"));
        }
        return 33026;
    }
}
```

Ejemplo yaml

```
version: '2'
services:
    web:
        build:
            context: .
            dockerfile: Dockerfile
        container_name: web
        ports:
            - "8087:33026"
    db:
        image: mongo:3.6.1
        container_name: db
        volumes:
            - mongodb:/data/db
            - mongodb_config:/data/configdb
        ports:
            - 27017:27017
        command: mongod
        
volumes:
    mongodb:
    mongodb_config:
```

Ejemplo DockerFile

```
FROM openjdk:17
WORKDIR /usrapp/bin
ENV PORT=33026
COPY /target/classes /usrapp/bin/classes
COPY /target/dependency /usrapp/bin/dependency
CMD ["java","-cp","./classes:./dependency/*","edu.escuelaing.aygo.container.RestServiceApplication"]
```

### Evidencias instalación

##docker build --tag dockerspringprimer .

<img width="921" height="303" alt="image" src="https://github.com/user-attachments/assets/7012e9f9-390d-4204-88e5-928f894fb040" />

##Creación de Im+agenes en Docker

<img width="921" height="296" alt="image" src="https://github.com/user-attachments/assets/8eb31cb6-5e18-4898-9cff-e2cae58ca018" />

<img width="921" height="351" alt="image" src="https://github.com/user-attachments/assets/e0a6e217-5f23-4a1f-9983-d9b559b4815b" />

Evidencia contenedores en Docker

<img width="1647" height="346" alt="image" src="https://github.com/user-attachments/assets/614ea370-0079-455d-a8b2-e67471cdf65b" />

##Muestra de ejecución de página usando docker compose

<img width="921" height="166" alt="image" src="https://github.com/user-attachments/assets/8db6be16-52a2-4b1d-8e12-76e7e8ef89ea" />

##Creación de repositorio en dockerHub

<img width="921" height="345" alt="image" src="https://github.com/user-attachments/assets/2d9b88b6-6bf4-445d-98ca-97159d6e1b75" />


##Creación Máquina virtual en AWS

<img width="921" height="321" alt="image" src="https://github.com/user-attachments/assets/ab313762-e4f6-44be-af14-725132b1d59e" />

##Conexión a una instancia

<img width="921" height="454" alt="image" src="https://github.com/user-attachments/assets/9192b30c-7c10-4833-a819-478dc2180e08" />

##Muestra de instancia en ejecución

<img width="921" height="235" alt="image" src="https://github.com/user-attachments/assets/d1958bd5-0b62-413b-8411-3545d543a921" />

##Envío contenerod de dockerHub a AWS

<img width="921" height="469" alt="image" src="https://github.com/user-attachments/assets/b795cbb6-1019-4565-9c0c-551b85b8f479" />

##Agregación de puerto 42000

<img width="921" height="200" alt="image" src="https://github.com/user-attachments/assets/a70011cc-af19-4429-b31c-bfb676bf67de" />

##Muestra de página funcionando con AWS utilizando el contenedor alojado en DockerHub

<img width="921" height="227" alt="image" src="https://github.com/user-attachments/assets/42438d88-af98-4314-a369-33da2c8e28c5" />

##URL de AWS del taller

http://ec2-54-204-130-61.compute-1.amazonaws.com:42000/greeting?name=Arley



## Configurando Swagger en nuestro proyecto y generando la documentación del API REST

Para lo documentación a través de Suagger se importaron las siguientes dependencias en el archivo build.gradle:
```
implementation 'io.springfox:springfox-swagger2:3.0.0'
implementation 'io.springfox:springfox-boot-starter:3.0.0'
```
La configuración de Swagger se centra sobre el bean Docket:

Creamos una clase que contiene el siguiente código:
```
@Configuration
@EnableSwagger2
public class SpringFoxConfig{

    @Bean
    public Docket api() { 
        return new Docket(DocumentationType.SWAGGER_2)  
          .select()                                  
          .apis(RequestHandlerSelectors.any())              
          .paths(PathSelectors.any())                          
          .build();                                           
    }
    
}
```
Podemos revisar la documentación del API REST que se nos genera:

![Imagen de WhatsApp 2023-02-08 a las 21 21 32](https://user-images.githubusercontent.com/25957863/217877921-8366eedd-1a64-4ad5-8975-41af938f8475.jpg)

Para realizar la configuración de la interfaz gráfica debemos configurar una clase que implemente WebMvcConfigurer así:
```
@EnableWebMvc
public class WebMvc implements WebMvcConfigurer{

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("swagger-ui.html")
        .addResourceLocations("classpath:/META-INF/resources/");

        registry.addResourceHandler("/webjars/**")
        .addResourceLocations("classpath:/META-INF/resources/webjars/");
    }
    
}
```
Por último agregamos la siguiente configuración al recurso denominado: application.properties:
```
spring.mvc.pathmatch.matching-strategy=ANT_PATH_MATCHER
```
Ahora accedemos al recurso a través de la dirección:

[Link](http://localhost:8080/swagger-ui/index.html#/)

Una vez accedemos se nos generan las especificaciones para la API REST de Spring:

![image](https://user-images.githubusercontent.com/25957863/217869360-1f22e560-f90b-4b0e-a707-5a4d3f64857c.png)

Si seleccionamos la pestaña de product-Controller podemos ver que Springfox ha generado las especificaciones para la entidad Usuario con métodos HTTP como GET , POST, PUT y DELETE.

![image](https://user-images.githubusercontent.com/25957863/217869979-f55b153b-388c-4416-bc30-6be15e6fa71a.png)

Si seleccionamos la pestaña de users-Controller podemos ver que Springfox ha generado las especificaciones para la entidad Usuario con métodos HTTP como GET , POST, PUT y DELETE.

![image](https://user-images.githubusercontent.com/25957863/217871413-017fecdd-fea8-4a9e-94ee-2a097bd900bd.png)

Cuando damos click en cada una de las peticiones HTTP, se nos despliega un json con los atributos y tipos del objeto. Así como la especificación de los parámetros requeridos.

![image](https://user-images.githubusercontent.com/25957863/217872632-118db931-32b7-40fe-9f44-3d4993c31ab9.png)

<img align="right" src="https://github.com/ada-school/module-template/blob/main/ada.png">

## Codelab 🧪 Implementing a REST API Service

Implement different REST API Services to support a store products management system, implementing each CRUD Operation
with Pagination for each service (Users and Products):

- Create
- Read
- Update
- Delete

👉 Aim to reach the [Glory of Rest](https://martinfowler.com/articles/richardsonMaturityModel.html).

👉 Use the correct methods and status codes
of [HTTP Protocol](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP).

👉 It should have at least have
the [Level 2 - HTTP Verbs of Richardson Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html).

**Programming Language**:- Java.

**Framework:** Spring Boot.

**Database:** MongoDB.

**Learning Objectives**

- [ ]  Use the Richardson Maturity Model to implement a REST API Service.
- [ ]  Implement a REST API Service using Spring Boot.
- [ ]  Implement CRUD Operations.

## Detail Orientation 🤹🏽

Good code is about details. Follow each step carefully and make sure your code is clean and readable.

**Main Topics**

* Microservices.
* REST API.
* MongoDB.
* Java.
* Spring Boot.

## Codelab 🧪

🗣️ "I hear and I forget I see and I remember I do and I understand." Confucius



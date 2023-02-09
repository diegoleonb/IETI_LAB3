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

![Imagen de WhatsApp 2023-02-08 a las 21 23 18](https://user-images.githubusercontent.com/25957863/217878511-3fc5faa2-9185-4e0f-a972-e6b1144091c9.jpg)

Como podemos obersarvar se nos muestra una casilla denominada Curl que hace referencia a la URL del modo detallado de la petición. Así cómo los cabezados de las respuestas de las peticiones http realizadas:

![Imagen de WhatsApp 2023-02-08 a las 21 24 01](https://user-images.githubusercontent.com/25957863/217878877-c022391a-a585-4ff6-bf1f-2b97dff7f053.jpg)

Elaborado por:
- [Jaime Castro](https://github.com/Nicolascastro25)
- [Diego Leon](https://github.com/diegoleonb)

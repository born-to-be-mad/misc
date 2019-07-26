# Ways to change Embedded Tomcat Server Port in Spring Boot Application

* By using VM options <BR/>`$ java -jar -Dserver.port=8100 springbootapp.jar`

* By specifying the server.port property in the resource file `application.properties`<BR/>
```
$ cat application.properties
server.port = 8100`
```
`server.port = 0` if you want to use random port i.e. every time your Spring boot application starts.
Also, when you use the random port you can get the port info by using the `@Value` annotation as shown below:
`@Value("${local.server.port}")`

* Programmatically
````
@Configuration
public class ServletConfig {
@Bean
public EmbeddedServletContainerCustomizer containerCustomizer() {
   return (container -> {
     container.setPort(8100);
    });
  }
}
````
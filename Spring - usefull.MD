# Ways to change Embedded Tomcat Server Port in Spring Boot Application

- By using VM options <BR/> `$ java -jar -Dserver.port=8100 springbootapp.jar`

- By specifying the server.port property in the resource file `application.properties`<BR/>

```
$ cat application.properties
server.port = 8100`
```

`server.port = 0` if you want to use random port i.e. every time your Spring boot application starts.
Also, when you use the random port you can get the port info by using the `@Value` annotation as shown below:
`@Value("${local.server.port}")`

- Programmatically

```
@Configuration
public class ServletConfig {
@Bean
public EmbeddedServletContainerCustomizer containerCustomizer() {
   return (container -> {
     container.setPort(8100);
    });
  }
}
```

# Enable HTTPS on a Spring Boot Application

- Generate Self-Signed Certificate

  - Go to jdk/bin and run `keytool -genkeypair -alias selfsigned_localhost_sslserver -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore my-secured-ssl-key.p12 -validity 3650` to have a certificate file `my-secured-ssl-key.p12` according to the "PKCS12:Public Key Cryptographic Standard". The self-signed certificate is protected by password so you need to enter password and some other datails while generating.

- Applying the SSL to Spring Boot Application

  - Copy generated PKCS12 certificate `my-secured-ssl-key.p12` to `src/main/resources` on Spring Boot Application

  ```
  #SSL Key Info
  security.require-ssl=true
  server.ssl.key-store-password=India@123
  server.ssl.key-store=src/main/resources/my-secured-ssl-key.p12
  server.ssl.key-store-type=PKCS12
  ```

  - As result if we try to get any REST endpoint by using 'HTTP' instead of 'HTTPS' we get 'Bad Request'

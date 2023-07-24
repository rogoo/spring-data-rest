# spring-data-rest
A simple app using Spring Data Rest and H2.

To have a list of all endpoints go to this URL. The base URL is the root **"/"**, but I've changed to use **"/apir"**.
```
http://localhost:8080/apir
```


All RESTful exposed are:
- http://localhost:8080/apir/person (GET) - lists all
- http://localhost:8080/apir/person/{id} (GET) - search by person by id
- http://localhost:8080/apir/person (POST) - includes a person. Send the data in JSON format.
- http://localhost:8080/apir/person (PUT) - updates all information of a person. Send the data in JSON format.
- http://localhost:8080/apir/person (PATCH) - updates some information of a person. Send the data in JSON format.
- http://localhost:8080/apir/person/{id} (DELETE) - removes the person by id

## Chaging Base URI
By default, it serves up REST resources at the root "/", and so, to avoid conflicts, I'm changing to use **/apir**.
```
spring.data.rest.basePath=/apir
```

## REST api
Spring Data REST will look for repositories and expose RESTful api based on their entities' class name, uncapitalized and pluralized.

For our only repository the exposed REST api is **/persons**.
```
public interface PerRepository extends CrudRepository<Person, Integer>
```
But you can change the URL by using either @RepositoryRestResource. In the following the URL was changed to **/person**.
```
@RepositoryRestResource(path = "person")
public interface PerRepository extends CrudRepository<Person, Integer>
```

By default, all repositories methods are exposed (and yes it can be changed). So, if you have only findAll() method, only the GET method will be exposed. As we are using CrudRepositories, all http methods are exposed.

## Date JSON Format
Spring has a default pattern for date, and I've changed it (in _Person_) to the pattern **"dd/MM/yyy"** with **@JsonFormat(pattern = "dd/MM/yyyy")** jackson annotation.

## H2 Console
Remember that H2 is a inmemory database. So on every restart it's gone. You can point to a file and make it persistent.

If you want to access the H2 embedded GUI, remember to enabled it.
```
spring.h2.console.enabled=true*
```
Go to the URL **/h2-console** and use the H2 information in your console to log in.

By default the URL is **/h2-console**, but you can change it.
```
spring.h2.console.path=/h2
```
## Database Preloading
In the ConfigurationEntry class I am preloading the H2 database so it's not empty.

## Use of Spring Devtools
Out of everything it does, the automatic restart of the application whenever a file is changed just makes the development life a lot easier.
#### Maven
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-devtools</artifactId>
	<scope>runtime</scope>
	<optional>true</optional>
</dependency>
```

#### Gradle
```
dependencies {
    developmentOnly("org.springframework.boot:spring-boot-devtools")
}
```

And that's it folks.
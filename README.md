Sprint initializer: https://start.spring.io/
mvn clean install
mvn spring-boot:run

GET http://localhost:8080/api/books

POST http://localhost:8080/api/books
Content-Type: application/json

{
 "title": "Spring Boot in Action",
 "author": "Craig Walls",
 "isbn": "9781617292545"
}

DELETE http://localhost:8080/api/books/1

Very good explaination of the project
Reference: https://medium.com/@pratik.941/building-rest-api-using-spring-boot-a-comprehensive-guide-3e9b6d7a8951 
Building REST services with Sprint: https://spring.io/guides/tutorials/rest
Docker example with Sprint:https://medium.com/@yunuseulucay/end-to-end-spring-boot-with-mysql-and-docker-2c42a6e036c0

Visit Swagger interface at: http://localhost:8080/swagger-ui.html

Good example documenting how to generate Swagger APIs in Spring Boot: https://bell-sw.com/blog/documenting-rest-api-with-swagger-in-spring-boot-3/#mcetoc_1heq9ft3o1v 

# 개요
Spring Boot에서 MongoDB를 셋팅하는 방법이다.

## Setting

### Gradle 설정
compile("org.springframework.boot:spring-boot-starter-data-mongodb")

### application.properties 설정([추가 정보](http://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html))
spring.data.mongodb.host=127.0.0.1 #호스트 주소

spring.data.mongodb.port=27017

spring.data.mongodb.database=logs #db명

## Code

### Model 생성

<pre>
import org.springframework.data.annotation.Id;

public class LogData {
    @Id
    private long timestamp;
    private String message;
}
</pre>

### Repository 생성

<pre>
import org.springframework.data.mongodb.repository.MongoRepository;

public interface LogsRepository extends MongoRepository<LogData, Long> {
}
</pre>
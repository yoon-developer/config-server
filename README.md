Spring Cloud Config (Server)
==========

# 1. build.gradle
> 버전  
- spring cloud: 2020.0.1  
- spring-boot-starter-actuator: 2.4.3  
- spring-cloud-config-server: 3.0.2

> dependencies 추가
- spring-boot-starter-actuator (config refresh 기능)
- spring-cloud-config-server (spring cloud config server)

```text
ext {
	set('springCloudVersion', "2020.0.1")
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-actuator' 
	implementation 'org.springframework.cloud:spring-cloud-config-server'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

dependencyManagement {
	imports {
		mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
	}
}
```

# 2. Application.yml

> server port 설정
- config server 는 기본적으로 8888 포트번호 사용

```yaml
server:
  port: 8888
```

> github 연동
- github yaml 파일 uri 지정
```yaml
spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/yoonDevGit/config-repository
```
# 3. Code

> @EnableConfigServer 추가
```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConfigServerApplication.class, args);
	}

}
```
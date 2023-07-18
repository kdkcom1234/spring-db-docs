Swagger를 사용하여 Spring Boot 애플리케이션의 API 스펙 문서를 생성하는 방법에 대해 설명드리겠습니다. 의존성 관리를 Gradle로 진행하겠습니다.

1. 의존성 추가:
   프로젝트의 `build.gradle` 파일에 Swagger 관련 의존성을 추가해야 합니다. 다음은 Swagger 관련 의존성을 Gradle을 사용하여 추가하는 예시입니다:

   ```groovy
   implementation 'io.springfox:springfox-boot-starter:3.0.0'
   ```

   이후 `build.gradle` 파일을 다시 빌드하여 의존성을 가져옵니다.

2. Swagger 설정 클래스 작성:
   Swagger를 구성하기 위한 설정 클래스를 작성해야 합니다. 다음은 Swagger 설정을 위한 클래스를 작성하는 예시입니다:

   ```java
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import springfox.documentation.builders.ApiInfoBuilder;
   import springfox.documentation.builders.PathSelectors;
   import springfox.documentation.builders.RequestHandlerSelectors;
   import springfox.documentation.service.ApiInfo;
   import springfox.documentation.spi.DocumentationType;
   import springfox.documentation.spring.web.plugins.Docket;
   import springfox.documentation.swagger2.annotations.EnableSwagger2;

   @Configuration
   @EnableSwagger2
   public class SwaggerConfig {

       @Bean
       public Docket api() {
           return new Docket(DocumentationType.SWAGGER_2)
                   .select()
                   .apis(RequestHandlerSelectors.basePackage("com.example.controller")) // 컨트롤러가 있는 패키지 경로 지정
                   .paths(PathSelectors.any())
                   .build()
                   .apiInfo(apiInfo());
       }

       private ApiInfo apiInfo() {
           return new ApiInfoBuilder()
                   .title("API Documentation") // 문서 제목
                   .description("API Documentation for My Spring Boot Application") // 문서 설명
                   .version("1.0.0") // API 버전
                   .build();
       }
   }
   ```

   위의 예시에서 `@EnableSwagger2` 애노테이션은 Swagger 지원을 활성화하고, `Docket` 빈을 구성하여 Swagger 문서를 생성합니다. `RequestHandlerSelectors`를 사용하여 API를 문서화할 컨트롤러 패키지를 지정하고, `PathSelectors`를 사용하여 모든 경로를 문서화하도록 설정합니다. `apiInfo()` 메소드를 사용하여 문서에 대한 정보를 추가합니다.

3. 애플리케이션 실행 및 문서 확인:
   Swagger 설정이 완료되면 애플리케이션을 실행하고 웹 브라우저에서 Swagger UI에 접속하여 문서를 확인할 수 있습니다. 기본적으로 Swagger UI는 `/swagger-ui.html` 경로에서 접근할 수 있습니다. 예를 들어, `http://localhost:8080/swagger-ui.html`에 접속하여 Swagger 문서를 확인할 수 있습니다.

   Swagger UI에서는 API 엔드포인트, 요청 및 응답의 모델 및 파라미터 정보, 예시 요청 및 응답 등을 자동으로 생성하여 시각적으로 표시합니다.

이렇게 하면 Swagger를 사용하여 Spring Boot 애플리케이션의 API 스펙 문서를 자동으로 생성할 수 있습니다. Swagger를 사용하면 개발자와 클라이언트 간의 의사 소통을 쉽게 할 수 있고, 문서화된 API를 통해 API의 사용 방법을 이해하고 테스트할 수 있습니다.

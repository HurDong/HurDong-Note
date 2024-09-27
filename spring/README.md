# 🌱 Spring Boot 프로젝트에서 리소스 폴더가 패키지로 표시되는 문제 해결 가이드

## 📂 프로젝트 설정 접근
**프로젝트 설정 열기**: 프로젝트 우클릭 후 'Build Path' -> 'Configure Build Path'를 선택합니다.
**Source 탭 접근**: 열린 설정 창에서 'Source' 탭을 선택합니다.

## 📁 리소스 폴더 설정
**리소스 폴더 위치 확인**: `src/main/resources` 폴더를 찾아 선택합니다. <br>
**Exclusion Pattern 설정**: 'Excluded' 섹션에서 'Edit'를 클릭 후, Exclusion Patterns에 '**'를 추가합니다.

## ✅ 설정 확인 및 적용
**변경 사항 저장**: 설정 변경 후 'OK'를 클릭하여 변경 사항을 저장합니다. <br>
**프로젝트 리프레시**: 프로젝트에 대한 변경 사항을 적용하기 위해 프로젝트를 리프레시 합니다. <br>
**폴더 확인**: 이제 `src/main/resources` 폴더가 올바르게 리소스 폴더로 인식되어 패키지로 보이지 않아야 합니다.

# 🗂️ MyBatis에서 Mapper 빈을 생성하지 못하는 경우

## 🔍 의존성 버전 확인
- **Build 파일 체크**: `build.gradle`이나 `pom.xml`에서 MyBatis와 Spring Boot의 버전을 확인합니다.

### 📌 호환 버전 표
| MyBatis-Spring-Boot-Starter | MyBatis-Spring | Spring Boot | Java Version |
|-----------------------------|----------------|-------------|--------------|
| 3.0                         | 3.0            | 3.0 - 3.1   | 17 or higher |
| 2.3                         | 2.1            | 2.5 - 2.7   | 8 or higher  |

- **의존성 조정**: 위 표에 따라 MyBatis를 Spring Boot의 버전에 맞게 의존성을 조정합니다. 버전이 일치하지 않는 경우, MyBatis의 의존성을 Spring Boot 버전에 맞춰 변경합니다. 이는 Mapper 빈 생성 오류를 해결하는 데 중요합니다.

# 🔧 STS에서 프로젝트 이름 변경 후 빌드 오류 해결

## 🛠 프로젝트 이름 변경
- **settings.gradle 수정**: STS에서 프로젝트 이름을 변경하고 나서 `settings.gradle` 파일을 열고 `rootProject.name` 값을 수정합니다.
  
## 🔄 Gradle 프로젝트 새로고침
- **Gradle Refresh**: 프로젝트 우클릭 후 'Gradle' -> 'Refresh Gradle Project'를 선택합니다. 이는 Gradle 설정을 최신 상태로 업데이트합니다.

## 🔄 프로젝트 새로고침
- **프로젝트 새로고침**: 프로젝트를 우클릭하고 'Refresh'를 선택하여 모든 변경 사항을 프로젝트에 적용합니다.

# 🔐 Spring에서 OAuth 2.0 사용하기

## 📖 OAuth 2.0이란?
OAuth 2.0은 인터넷 사용자가 비밀번호를 공개하지 않고도, 다른 웹 사이트의 자원에 대한 접근 권한을 서드 파티 애플리케이션에 부여할 수 있는 표준 프로토콜입니다. 이를 통해 사용자 대신 외부 시스템이 안전하게 행동할 수 있도록 합니다.

## 🚀 OAuth 2.0의 주요 역할
- **리소스 소유자(Resource Owner)**: 사용자가 리소스에 대한 접근을 허용하는 주체입니다.
- **리소스 서버(Resource Server)**: 사용자의 데이터를 호스팅하는 서버입니다.
- **클라이언트(Client)**: 사용자 대신 리소스 서버에 접근을 요청하는 애플리케이션입니다.
- **인증 서버(Authorization Server)**: 클라이언트가 사용자를 대신해 리소스에 접근할 수 있도록 토큰을 발급하는 서버입니다.

## 🛠 Spring에서 OAuth 2.0 구현 방법
### 설정 구성
`application.yml` 또는 `application.properties`에 클라이언트와 리소스 서버의 세부 정보를 설정합니다.

#### application.yml 예시
```yaml
spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: your-client-id
            client-secret: your-client-secret
            scope: email, profile
        provider:
          google:
            authorization-uri: https://accounts.google.com/o/oauth2/auth
            token-uri: https://oauth2.googleapis.com/token
            user-info-uri: https://openidconnect.googleapis.com/v1/userinfo
            user-name-attribute: sub
```

### SecurityConfig.java 예시
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/", "/home").permitAll()
                .anyRequest().authenticated()
            .and()
            .oauth2Login();
    }
}
```
## 📝 OAuth 2.0 사용시 주의사항
- **보안**: 리다이렉션 URI는 가능한 한 정확하게 설정하고 클라이언트 비밀은 안전하게 보관 필요!
- **범위 관리**: 요청하는 범위(scope)는 최소한으로 유지하며 필요 이상의 접근 권한을 요청 X

# 📜 ApiResponse 클래스 사용 가이드

## 🚀 개요
`ApiResponse` 클래스는 REST API 응답을 표준화하기 위해 사용되는 유틸리티 클래스입니다. 이 클래스를 사용하면 응답 코드, 메시지, 데이터를 포함하는 일관된 API 응답 형식을 쉽게 생성할 수 있습니다.

## 🛠 클래스 정의
```java
@Getter
@Setter
public class ApiResponse<T> {
    private int code;
    private String message;
    private T data;

    public ApiResponse(int code, String message, T data) {
        this.code = code;
        this.message = message;
        this.data = data;
    }

    public static <T> ApiResponse<T> success(String message, T data) {
        return new ApiResponse<>(200, message, data);
    }
    
    public static <T> ApiResponse<T> error(int code, String message) {
        return new ApiResponse<>(code, message, null);
    }
}
```

## 📌 사용 예시

### 성공 응답 생성

성공적인 API 요청 결과를 클라이언트에게 전달할 때 사용

```java
// 자동으로 200 상태 코드를 생성하여 제공!
ApiResponse<String> response = ApiResponse.success("게시글이 성공적으로 등록되었습니다.", ResponseDto);
```

### 오류 응답 생성

API 요청 처리 중 발생한 오류를 클라이언트에게 알릴 때 사용

```java
// 1404 같은 경우 개발자가 커스텀으로 에러 코드를 생성 주로 4~6자리로 구성 추천!
ApiResponse<Object> errorResponse = ApiResponse.error(1404, "게시글이 존재하지 않습니다!");
```

## 📝 주요 메서드 설명

- **success 메서드**: 성공적인 처리를 나타내는 ApiResponse 객체를 생성 / HTTP 상태 코드는 기본적으로 200으로 설정 / 이 메서드는 메시지와 데이터를 인자로 받아, 요청이 성공했을 때 클라이언트에 반환할 응답 객체를 생성
 
```java
ApiResponse<String> response = ApiResponse.success("게시글이 성공적으로 등록되었습니다.", ResponseDto);
```

- **error 메서드**: 오류가 발생했을 때 사용자 정의 오류 코드와 메시지로 ApiResponse 객체를 생성 / 데이터 필드는 `null`로 설정

```java
ApiResponse<Object> errorResponse = ApiResponse.error(1404, "게시글이 존재하지 않습니다!");
```

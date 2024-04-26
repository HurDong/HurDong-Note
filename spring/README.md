# 🌱 Spring Boot 프로젝트에서 리소스 폴더가 패키지로 표시되는 문제 해결 가이드

## 📂 프로젝트 설정 접근
**프로젝트 설정 열기**: 프로젝트 우클릭 후 'Build Path' -> 'Configure Build Path'를 선택합니다.
**Source 탭 접근**: 열린 설정 창에서 'Source' 탭을 선택합니다.

## 📁 리소스 폴더 설정
**리소스 폴더 위치 확인**: `src/main/resources` 폴더를 찾아 선택합니다.
**Exclusion Pattern 설정**: 'Excluded' 섹션에서 'Edit'를 클릭 후, Exclusion Patterns에 '**'를 추가합니다.

## ✅ 설정 확인 및 적용
**변경 사항 저장**: 설정 변경 후 'OK'를 클릭하여 변경 사항을 저장합니다.
**프로젝트 리프레시**: 프로젝트에 대한 변경 사항을 적용하기 위해 프로젝트를 리프레시 합니다.
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

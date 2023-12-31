# 🚀 AWS EC2를 이용한 Spring Boot(Maven) 서버 배포 가이드

## 준비 과정
1. **Git-Bash 실행**: 데스크탑에서 Git-Bash를 실행
2. **.pem 파일 위치로 이동**: `cd ~/desktop/(자신의 .pem위치)`를 입력

## SSH 연결
3. **AWS EC2 SSH 연결**: AWS EC2 홈페이지에서 제공하는 SSH 연결 코드를 복사하여 Git-Bash에 붙여넣기
4. **Connection Timeout 해결**: 연결이 안 될 경우, 인스턴스를 재부팅하거나 데스크탑을 재부팅

## 코드 클론 및 준비
5. **GitHub 레포지토리 클론**: `git clone (github 레포지토리 주소)`를 입력하여 레포지토리를 클론
6. **레포지토리로 이동 및 확인**: `cd (레포지토리 이름)` 후 `ls`를 입력하여 `mvnw` 파일이 있는지 확인
7. **실행 권한 부여**: `chmod +x mvnw`로 `mvnw`에 실행 권한을 부여

## 빌드 및 패키징
8. **패키지 생성**: `./mvnw clean package`를 입력하여 이전 기록을 지우고 새 패키지를 생성
9. **빌드 성공 확인**: `BUILD SUCCESS` 문구가 나올 때까지 대기
10. **Target 디렉토리 확인**: `ls`로 `target` 디렉토리가 생성되었는지 확인한 후 `cd target`으로 이동
11. **Jar 파일 확인**: `ls`로 jar 파일이 생성되었는지 확인

## 서버 배포
12. **서버 실행**: `java -jar (jar파일이름)`을 입력하여 서버를 실행
   - **URL 접속 문제 해결**: 정상적인 URL을 입력했는데 접속이 안 될 경우, `mv (jar파일) ..`을 입력하여 jar 파일을 상위 디렉토리로 이동
13. **백그라운드 실행**: Git-Bash를 닫아도 서버가 계속 실행되길 원할 경우 `nohup java -jar (jar파일이름) &`를 입력

## 배포 종료
14. **`java -jar (jar파일이름)으로 한 경우`** `ctrl + c`로 강제 종료
15. **`nohub java -jar (jar파일이름) &`으로 한 경우** `ps -ef`로 현재 실행중인 프로세스 목록 확인
    - java -jar (jar파일이름)으로 된 프로세스의 PID를 기억하여 `kill -9 (PID)`를 실행
## 에러 처리
16. **EC2 인스턴스에서 상태검사 1/2가 뜰 경우** AWS의 EC2 탭으로 가서 인스턴스를 강제 중지 후 다시 시작을 한다.

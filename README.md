# memo
CS Knowledge

AWS EC2를 이용하여 Spring Boot(Maven) Server 배포하는 법
1. Git-Bash를 킨다.
2. cd ~/desktop/(자신의 .pem위치)
3. ssh 연결 코드를 AWS EC2 홈페이지에서 복사 후 붙여넣기
4. Connection Timeout 발생 시 인스턴스 재부팅 해보고 안되면 데스크탑 재부팅
5. git clone (github 레포지토리에서 code누르면 나오는 코드 복사)
6. cd (레포지토리) 후 ls를 하여 mvnw 파일이 있는 지 확인
7. chmod +x mvnw 로 mvnw 실행 권한을 줌
8. ./mvnw clean package 로 이전 기록들을 지우고 새로운 package 생성
9. BUILD SUCCESS 문구가 나올 때까지 대기
10. ls로 target 디렉토리가 생성된 것을 확인후 cd target으로 해당 디렉토리로 이동
11. ls로 jar파일이 생성되었는지 확인 후 java -jar (jar파일이름)
12. 배포는 완료하였지만 정상적인 URL을 입력하였는데, 안되는 경우 jar 파일을 상위 디렉토리로 이동시켜야함
13. 백그라운드상태(Git-Bash를 꺼도 배포를 하고 싶을 때) nohub java -jar (jar파일이름) &

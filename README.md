# Gradle(입문용 공부)

## 설치[ CLI(Command Line Interface), CentOS7 사용 ]
> 설치 전제 조건
>> JDK 6 이상 설치 / Spring Boot 설치도 겸함
```sh
# SDKMAN 설치(A.K.A GVM)
curl -s get.sdkman.io | bash

# 환경변수 설정
source ~/.sdkman/bin/sdkman-init.sh // 원하는 위치로 변경

# 스프링 부트 설치(설치 경로 : ~/.sdkman/candidates/springboot/2.1.2.RELEASE/)
sdk install springboot
# 버전확인
springboot -version

# 스프링 부트 이니셜라이저 적용한 프로젝트 다운로드(demo.zip)
spring init -dweb,jpa,security --build gradle

# 지정한 폴더에 압축 풀기
mkdir springbooweb
unzip demo.zip -d ./springbooweb/

# 그레이들 설치(설치 경로 : ~/.sdkman/candidates/gradle/5.1.1/)
sdk install gradle
# 버전확인
gradle -v
```

## init 태스크를 이용한 프로젝트 자동 생성
```sh
gradle init --type java-library
```
> 그레이들의 규칙은 메이븐을 따르므로 자바 패키지의 계층 구조에 맞춰 파일을 배치한다.
>> 빌드 스크립트에 명시적으로 자바 코드 위치만 추가하면 규칙과 다른 위치에도 자바 코드를 배치할 수 있다.
>>> 메이븐과 차별화되는 그레이들의 유연성이 돋보이는 부분이다.

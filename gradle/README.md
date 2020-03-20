## Gradle(입문용 공부)

### 설치[ CLI(Command Line Interface), CentOS7 사용 ]
> 설치 전제 조건
```sh
JDK 6 이상 설치, $JAVA_HOME 환경변수 설정(.bash_profile) 적용
항상 현재 디렉토리에서 명령어를 실행할 
```

> SDKMAN 설치(A.K.A GVM)
```sh
curl -s get.sdkman.io | bash
```

> 환경변수 설정
```sh
source ~/.sdkman/bin/sdkman-init.sh // 원하는 위치로 변경
```

> 스프링 부트 설치(설치 경로 : ~/.sdkman/candidates/springboot/2.1.2.RELEASE/)
```sh
sdk install springboot
# 버전확인
springboot -version
```

> 스프링 부트 이니셜라이저 적용한 프로젝트 다운로드(demo.zip)
```sh
spring init -dweb,jpa,security --build gradle
```

> 지정한 폴더에 압축 풀기
```sh
mkdir springbooweb
unzip demo.zip -d ./springbooweb/
```

> 그레이들 설치(설치 경로 : ~/.sdkman/candidates/gradle/5.1.1/)
```sh
sdk install gradle
# 버전확인
gradle -v
```

### init 태스크를 이용한 프로젝트 자동 생성
```sh
gradle init --type java-library
```
> 그레이들의 규칙은 메이븐을 따르므로 자바 패키지의 계층 구조에 맞춰 파일을 배치한다.
>> 빌드 스크립트에 명시적으로 자바 코드 위치만 추가하면 규칙과 다른 위치에도 자바 코드를 배치할 수 있다.
>>> 메이븐과 차별화되는 그레이들의 유연성이 돋보이는 부분이다.

### build.gradle 내용 확인
```sh
plugins {
    // 자바 플러그인을 적용한다는 내용임
    id 'java-library'
}

repositories {
    // 의존 관계를 해결하기 위한 메이븐 중앙 저장소.
    // dependencies 블록에 지정한 의존 라이브러리를 메이븐 중앙 저장소에서 자동으로 내려받는다.
    jcenter()
}

dependencies {
    // 의존 라이브러리를 'group:name:version' 형식으로 지정했는데 이는 단축 형식이라는 생략 기법이다.
    // 생략하지 않을 경우 'compile group:'', name:'', version:''
    // 의존 라이브러리를 지정할 때는 compile 또는 testCompile 키워드를 사용한다.
    // compile : 프로덕션 코드를 컴파일하고 실행할 때 필요
    // testCompile : 테스트 코드를 컴파일하고 실행할 때 필요
    api 'org.apache.commons:commons-math3:3.6.1'
    implementation 'com.google.guava:guava:26.0-jre'
    testImplementation 'junit:junit:4.12'
}
```

### 빌드 실행과 결과 확인
> 사용 가능한 태스크 확인
```sh
gradle tasks
```

> 빌드 실행(결과물은 build 디렉토리 아래에 생성)
```sh
gradle build
```
* 빌드 내용
  * 의존 라이브러리 다운로드
  * 프로덕션 코드 컴파일
  * JAR 파일로 압축
  * 테스트 코드 컴파일과 실행
  
* 빌드가 완료된 상태에서 다시 빌드를 실행하면 UP-TO-DATE가 나오며 실행을 건너뛴다.

> 빌드 실행결과 지우기(빌드 실행 전 상태로 되돌리기)
```sh
gradle clean
```

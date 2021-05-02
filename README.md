# Spring Cloud Config Server
- - -

## 소프트웨어 구성
1. OpenJDK 11
2. Spring Boot 2.4.5
3. Spring Cloud Config Server
4. Spring Cloud Bootstrap
5. Spring Boot Starter Actuator
6. Spring Cloud Starter Bus AMQP

> http://localhost:8888/ecommerce/{default}
 
- - -
- Local Config Setting
- Remote Config Setting
- Native Config Setting

- - -
## RabbitMQ Install
> brew update  
> brew install rabbitmq  
> export PATH=$PATH:/usr/local/sbin  
> rabbitmq-server  
- - -
## Spring Cloud Bus (Actuator bus-refresh Endpoint)
> - 분산 시스템의 노드를 경량 메세지 브로커와 연결  
> - 상태 및 구성에 대한 변경 사항을 연결된 노드에게 전달(Broadcast)
- - -
## AMQP (Advanced Message Queuing Protocol)
> - 메세지 지향 미들웨어를 위한 개방형 표준 응용 계층 프로토콜  
> - 메세지 지향, 큐잉, 라우팅(P2P, Pushlisher-Subcriber), 신뢰성, 보안  
> - Erlang, RabitMQ 에서 사용  
> - 메세지 브로커  
> - 초당 20개 이상의 메세지를 소비자에게 전달  
> - 메세지 전달보장, 시스템 간 메세지 전달  
> - 브로커, 소비자 중심
- - -
## Kafka 프로젝트
> - Apache Software Foundation 이 Scalar 어어로 개발한 오픈 소스 메세지 브로커 프로젝트  
> - 분산형 스트리밍 플랫폼  
> - 대용량의 데이터를 처리 가능한 메세징 시스템  
> - 초당 10만건 이상의 이벤트 처리  
> - Publisher/Subscribe, Topic에 메세지 전달  
> - Ack를 기다리지 않고 전달가능  
> - 생산자 중심  

## 설정 정보의 암호화 처리(대칭, 비대칭)
- 암호화  
> POST http://localhost:8888/encrypt  
  {keyValue}
- 복호화
> POST http://localhost:8888/decrypt  
  {keyValue} 

### 비대칭 키
- 키 생성 
> keytool -genkeypair -alias apiEncryptionKey -keyalg RSA -dname "CN=Jrock, OU=API Developement, O=jrock.co.kr, L=Seoul, C=KR" -keypass "test1234" -keystore apiEncryptionKey.jks -storepass "test1234"
- 키 확인
> keytool -list -keystore apiEncryptionKey.jks -v
- cer 파일 생성 ( private key ) 인증파일
> keytool -export -alias apiEncryptionKey -keystore apiEncryptionKey.jks -rfc -file trustServer.cer
- jks 파일 생성 ( public key )
> keytool -import -alias trustServer -file trustServer.cer -keystore publicKey.jks
# Tech Interview - Web

> URL과 URI의 차이점?

URI란 리소스에 대한 식별자로 URL과 URN을 포괄하는 개념입니다.
URL은 리소스의 위치를 의미하고 URN은 리소스의 이름을 의미합니다.
리소스의 이름만으로 리소스를 찾는 방법은 보편화되어있지 않기 떄문에 대부분의 URI는 URL이라고 볼 수 있습니다.

URL은 Schema, Domain, Port, Path, 그리고 Query로 이루어져 있습니다.
* Schema는 통신 프로토콜을 명시하는 부분이고
* Domain은 호스트명을 포함하는 해당하는 인터넷 주소를 의미합니다.
* Port는 해당 서버의 프로세스와 연결된 통로를 의미하며, 해당 프로세스에서 사용하는 소켓을 식별하기 위해 사용됩니다.
* Path는 서버에 존재하는 리소스의 경로를 의미하고
* Query는 key-value 형태의 파라미터를 의미합니다.

> www.google.com 도메인을 브라우저에 입력했을 때 일어나는 일을 순차적으로 설명해주세요.

1. DNS 조회  
해당 도메인을 주소창에 입력하면 해당하는 IP주소를 알아내기 위해서 다음과 같은 순서로 조회를 합니다.
   * 먼저 hosts 파일을 조회합니다.
   * hosts 파일에 해당 도메인 정보가 없으면 DNS Cache를 확인합니다.
   * DNS Cache에도 없으면 DNS 서버에 해당 도메인에 대한 IP주소를 요청합니다.

2. TCP/IP 연결  
해당 IP주소를 확인하면 해당 주소에 TCP/IP 연결을 수행합니다.
TCP/IP 연결은 3-way handshake로 SYN - ACK/SYN - ACK 순서로 진행됩니다.
   * 클라이언트에서 SYN 패킷을 보내면
   * 서버는 응답을 받았다는 ACK와 연결을 요청하는 SYN 플래그가 설정된 패킷을 보냅니다.
   * 클라이언트가 ACK/SYN을 받으면 해당 패킷을 받았다는 ACK 패킷을 보내고 연결이 완료됩니다.

3. Http 요청  
연결이 완료되면 Http request를 보냅니다.
Http request는 startline, header, body 구조로 되어있습니다.
   * startline에는 Http 메서드와 요청의 목표 주소, http 버전이 명시되어있고,
   * header에는 request에 대한 메타 정보가 있습니다.
   * body에는 전송하는 데이터가 담기는 부분입니다.

4. Http 응답  
서버에서는 클라이언트의 요청을 처리하고 http response를 보냅니다.
http response는 reqeust와 마찬가지로 startline, header, body 구조로 되어있습니다.
   * startline에는 http 버전과 상태코드와 상태메시지가 있고,
   * header에는 resopnse에 대한 메타 정보가 있습니다.
   * body에는 전송하는 데이터가 담겨있습니다.

5. 화면 렌더링  
클라이언트는 response로 html이나 이미지 등을 받아서 화면에 렌더링을 하게됩니다.

6. TCP/IP 연결 종료  
클라이언트에서 모든 데이터를 전송받으면 4way-handshake로 TCP/IP 연결을 종료합니다.
4way-handshake 순서는 FIN - ACK - FIN - ACK 순서로 진행됩니다.
   * 먼저 클라이언트가 연결을 종료하는 FIN 패킷을 보냅니다.
   * 서버는 FIN 패킷을 받았다는 ACK 패킷을 보내고
   * 연결을 종료하는 FIN 패킷을 보냅니다.
   * 클라이언트는 서버의 FIN 패킷을 받았다는 ACK 패킷을 보냅니다.

네트워크 지연으로 FIN 패킷을 전송하기 전에 보낸 패킷이 FIN 패킷보다 늦게 도착하는 경우를 방지하기 위해 클라이언트는 서버의 FIN 패킷을 수신하더라도 일정시간 동안 대기합니다.

WAS(Web Application Server)와 WS(Web Server)의 차이를 설명해주세요.

요즘 브라우저들은 SSR 방식으로 통신하는데 SSR이란?

Client Side Rendering 과 Server Side Rendering 의 차이점

Non Blocking I/O와 Blocking I/O에 대해서 설명해주시고, 각각 어떤 곳에 사용되는지 예시를 들어주세요.

XSS 에 대해 설명해주세요

CSRF(Cross-site request forgery)에 대해 설명하고, 이를 막기 위한 방법에 대해 설명해주세요.

대칭키, 비대칭키 암호화 방식에 대해 설명해주세요.

IOCP를 설명하시오

Rest API란 무엇인지?

RESTful 하다는 것이 무엇인지 설명해주세요.

RPC란 무엇인지?

REST와 RPC의 차이가 무엇인가요?

REST API와 GraphQL의 차이와 GraphQL을 썼을 때의 장단점을 설명해주세요.

webSocket이 무엇인가요?

gRPC가 무엇인가요?

webRTC가 무엇인가요?

CORS가 무엇인가요?

코어스를 쓰는 구체적인 이유는?

코어스를 구현하려면 어떻게 하는가?

Spring에서 CORS 에러를 해결하기 위한 방법은?

Session Hijacking(세션 하이재킹)이란?

대용량 트래픽에서 장애가 발생하면 어떻게 대응할 것인가요?

nginx에서 어떤 방식으로 로드밸런싱을 하는지 설명해주세요.

netty와 tomcat에 대해 아는 내용이나 차이점 설명해주세요.

Tomcat이 요청을 처리하는 내부동작에 대해 설명해주실 수 있나요?

Kafka를 사용해보신 적 있나요?

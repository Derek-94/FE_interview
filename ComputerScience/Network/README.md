# Network

### 주소창에 www.xxx.com을 치면 일어나는 일

![image](https://user-images.githubusercontent.com/52649378/141988455-b656cabc-5139-4a87-bfbb-a4b9ee6531cc.png)

1. 브라우저에 도메인 네임 입력
2. 도메인 네임 기반으로 DNS 서버에서 IP주소를 검색.
3. 도메인 네임과 IP주소를 HTTP 프로토콜로 HTTP 요청 메시지를 생성.
4. 이 메세지는 TCP 프로토콜을 사용하여 해당 IP주소 서버로 이동.
5. 서버는 요청메시지를 HTTP 프로토콜을 사용하여 웹 페이지 URL로 변환, 데이터 검색.
6. 검색된 데이터를 다시 HTTP 프로토콜로 HTTP 응답메시지를 생성, TCP 프로토콜로 클라이언트에게 보냄.
7. 응답 메시지를 HTTP 프로토콜로 웹 페이지 데이터로 변환, 브라우저 출력.

### 웹 소켓이란?

**서버와 클라이언트 간에 Socket Connection을 유지해서 언제든 양방향 통신 또는 데이터 전송이 가능하도록 하는 기술**

Websocket 은 웹 상에서 HTTP환경에서 양방향 통신을 지원하는 프로토콜.

HTTP 기반으로 handshake 가 일어나지만 HTTP와는 다른 방식.

 **HTTP는 접속 유지하지 않고, 한방향으로만 통신이 가능.**

서버 - 클라이언트 웹소켓 연결을 HTTP 프로토콜을 통해 이루어짐.

서버에 소켓 연결되면 3way handshake통해 TCP 세션 생성.

handshake 하고 연결 유지함.

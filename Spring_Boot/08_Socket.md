# 08. HTTP가 무엇일까요?

### 1. 스프링부트 동작 원리
1. 내장 톰켓을 가진다  
   톰켓을 따로 설치할 필요 없이 바로 실행 가능
    1. 소켓 통신  
        Socket : 운영체제가 가지고 있는 것, 메세지를 주고 받을 때 사용
         - 소켓을 열면 ip 주소와 포트 번호를 이용해서 메세지를 주고 받을 수 있음  
           이 __첫 번째 소켓은 연결의 용도__ 로만 사용함  
         - 첫 번째 소켓에 연결되는 순간 새로운 포트 번호를 가진 __새로운 소켓__ 을 생성하고 __새로운 스레드__ 를 만듦  
           첫 번째 소켓과의 연결은 끊어지고 두 번째 소켓으로 메세지를 주고 받음  
         - 새로운 스레드가 없다면 두 번째 소켓으로 메세지를 주고 받고 있을 때 첫 번째 소켓이 새로운 연결 요청을 받을 수 없음  
        스레드가 있으면 시간을 쪼개서 (time slice) 여러 작업이 동시에 동작하고 있는 것처럼 보임  
        - 소켓 통신의 장단점  
       장점 : 한 번 연결되고 난 이후에는 서버 입장에서 연결되어 있는 대상을 계속 알 수 있음  
       단점 : 연결이 계속 되어 있으면 부하가 크기 때문에 속도가 느려질 수 있음  
    2. http 통신  
    html 확장자로 만들어진 문서를 전달하기 위해 만들어진 통신  
    연결을 유지하지 않고 끊는 Stateless 방식을 사용  
    부하가 적다는 장점이 있지만, 다시 연결될 때 기존에 연결했던 대상이라도 새로운 대상으로 인식한다는 단점이 있음  
    (이 단점을 보완하면서 만들어진 게 웹 서버)
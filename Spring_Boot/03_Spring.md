# 03. 메시지 컨버터가 무엇인가요?

### 7. 스프링은 MessageConverter를 가지고 있고 기본값은 현재 Json이다
- 중간 데이터 : 메시지를 보내고 받는 양쪽에서 모두 이해할 수 있는 공통의 언어   
(예전에는 xml이 많이 쓰였으나 현재는 Json이 많이 쓰임)
- 자바 Object → Json(중간 데이터) → 파이썬 Object
- 메시지 컨버터 : 자바 프로그램을 전송할 때(request) 중간 데이터인 Json으로 알아서 바꿔주는 것 (현재 기본적으로 Jackson이 설정되어 있음)   
  응답(response)을 받을 때도 메시지 컨버터가 Json을 자바 프로그램으로 바꿔줌

### 8. 스프링은 BufferedReader와 BufferedWriter를 쉽게 사용할 수 있다
- 통신은 bit 단위로 이루어지는데, bit 단위는 사람이 이해하기 어려우니 영어 한 문자 단위로 통신하고 싶음 → 8 bit 필요 (256가지의 문자 전송 가능)   
  bit 단위로 통신을 보냈을 때 8 bit 단위로 끊어 읽으면 한 문자씩 받는 게 가능   
  → 8 bit를 논리적인 단위로 1 byte라고 부름   
  → 1 byte가 통신의 최소 단위가 됨
- Byte Stream으로 데이터를 보내면 자바는 InputStream을 통해 1 byte 단위로 받음   
  → byte를 문자로 변형하기 위해서 별도의 과정(캐스팅)이 필요, 번거로움   
  → InputStreamReader를 사용하면 문자 하나로 반환, 배열로 여러 개의 문자를 받는 것도 가능   
  단, 배열은 크기가 정해져 있다는 단점이 있음   
  → __BufferedReader__ : 가변 길이의 문자를 받을 수 있음
    - request.getReader()로 사용 가능
- __BufferedWriter__ : byte stream을 통해서 가변 길이의 문자열 데이터를 전송할 수 있게 해주는 클래스
  - BufferedWriter는 내려쓰기 기능을 제공하지 않아서 보통 자바에서는 __PrintWriter__(print(), println())를 많이 사용
  - JSP에서는 out이라는 내장 객체가 BufferedWriter임
- BufferedReader/Writer를 사용할 수 있는 어노테이션 제공   
  @ResponseBody → BufferedWriter   
  @ResquestBody → BufferedReader
# 12. 디스패처 서블릿이 무엇인가요?

4. FrontController 패턴  
   1. web.xml에 특정 주소가 들어올 경우 FrontController로 넘기도록 설정해둔다.
   2. 최초 앞단에서 요청을 받을 때 URI 또는 자바 파일에 대한 요청이라면 톰켓이 제어권을 가지고, 특정 주소일 경우 FrontController로 넘어간다. 요청이 들어왔을 때 자동으로 request, response 객체가 만들어진다.
   3. FrontController에서 자원에 접근하면서 새로운 request가 만들어지는데, 이때 기존의 request가 덮어씌워지는 문제를 방지하기 위한 기법이 __RequestDispatcher__ 이다.
5. RequestDispatcher  
    필요한 클래스 요청이 도달했을 때 FrontController에 도착한 request와 response를 그대로 유지시켜준다.
6. __DispatcherServlet__  
   = FrontController 패턴 + RequestDispatcher  
   스프링이 DispatcherServlet을 제공하기 때문에 FrontController 패턴을 직접 짜거나 RequestDispatcher를 직접 구현할 필요가 없다.  
   DispatcherServlet이 자동생성될 때 여러 객체(보통 필터들)가 생성(IoC)된다. 기본적으로 필요한 필터들은 자동등록되고, 내가 직접 등록할 수도 있다.
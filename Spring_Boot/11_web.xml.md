# 11. 웹 배포서술자(web.xml)에 대해서 알려줘요

3. web.xml  
   '관문', '문지기'
   - ServletContext의 초기 파라미터 생성  
      문을 통해 들어오지 않은(몰래 들어온) 대상을 판별할 수 있음
   - Session의 유효 시간 설정  
      - 세션 : 인증을 통해 들어갈 수 있음  
      세션의 유효 시간이 지나면 세션 초기화를 통해 시간을 연장할 수 있음
   - Servlet/JSP에 대한 정의 + Servlet/JSP 매핑
   - Mime Type 매핑  
      - Mime Type : 들고 올 데이터의 타입  
      어디로 보낼지 알기 위해서 Mime Type을 알아야 함  
      데이터의 가공까지 이루어짐  
      - get 방식의 요청 : select, 데이터를 가지고 오는 것이 아니라 데이터를 가지고 가기 위한 요청
   - Welcome File List
   - Error Pages 처리
   - 리스너/필터 설정  
      - 필터 : 들어올 수 있는 대상과 아닌 대상을 구분하는 역할  
      - 리스너 : 지정한 특정 대상이 들어오는지 확인하는 역할
   - 보안 설정

여기에서 Servlet/JSP 매핑 시(web.xml에 직접 매핑 또는 __@WebServlet 어노테이션 사용__) 모든 클래스에 매핑을 적용시키기에는 코드가 너무 복잡해지기 때문에 FrontController 패턴을 이용함
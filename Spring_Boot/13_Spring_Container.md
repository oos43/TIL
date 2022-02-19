# 13. 애플리케이션 컨텍스트란 무엇일까요?

- ContextLoaderListener : root-context.xml (applicationContext.xml) 파일을 읽어서 모든 요청이 공통적으로 필요로 하는 객체들을 만드는 역할을 함 (DB Connection 등)
  - ContextLoaderListener가 만든 객체들은 DispatcherServlet이 만든 객체들에 접근할 수 없음 (반대는 가능)  
  ContextLoaderListener가 먼저 객체를 만들기 때문

- DispatcherServlet : 컴포넌트 스캔 + 주소 분배
  - 컴포넌트 스캔 : 특정 패키지 이하의 모든 파일을 스캔해 객체를 만듦  
  스캔은 '메모리에 로딩한다'는 의미  
  어노테이션을 통해 필요한 것과 필요하지 않은 것을 구분함  
  (@Controller, @RestController, @Configuration, @Repository, @Service, @Component 등)  
  DispatcherServlet이 만드는 객체들은 스레드별로 관리됨

1. 스프링 컨테이너  
    DispatcherServlet에 의해 생성된 수많은 객체들은 어디에서 관리될까?  
    1. ApplicationContext  
        IoC를 통해 만들어진 객체들이 ApplicationContext에 등록됨  
        모든 정보가 ApplicationContext에 담겨 있음  
        ApplicationContext는 싱글톤으로 관리되기 때문에 어디에서 접근하든 동일한 객체를 보장해줌
        - servlet-applicationContext : 웹과 관련된 어노테이션만 스캔해서 메모리에 띄움  
        DispatcherServlet에 의해 실행됨
        - root-applicationContext : DB 관련 객체를 생성함  
        ContextLoaderListener에 의해 실행됨
    2. Bean Factory  
        필요한 객체를 Bean Factory에 등록할 수 있음  
        Bean Factory에 등록한 객체는 초기에 메모리에 로드되는 게 아니라 필요할 때 getBean() 메소드를 통해 로드할 수 있음 (이것도 IoC) - lazy-loading
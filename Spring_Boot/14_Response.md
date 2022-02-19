# 14. 스프링부트가 응답(Response)하는 방법이 궁금해요!

8. 요청 주소에 따른 적절한 컨트롤러 요청 (Handler Mapping)  
   - 주소 요청이 오면 적절한 컨트롤러의 함수를 찾아서 실행함
9. 응답
    - html 파일을 응답한다면 ViewResolver가 관여함  
        prefix로 파일이 있는 경로, suffix로 파일의 확장자가 붙음
    - Data를 응답한다면 MessageConverter가 작동하고, 메세지를 컨버팅할 때 기본 전략은 json임
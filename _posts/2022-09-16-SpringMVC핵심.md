---
title: Spring MVC의 핵심
categories:
  - spring
excerpt: 프론트 컨트롤러와 Spring MVC의 핵심에 대해 알아보자
---

## 기존 MVC의 한계
이전 포스팅에서 기존의 순수 서블릿과 JSP로 MVC패턴을 적용시켜보았다.  
해결하지 못한 한계점은 컨트롤러 역할을 하는 서블릿의 중복되는 코드와 필요하지 않은 코드가 존재한다는 점이다.   

## 점진적 개선
### v1 
#### + 프론트 컨트롤러를 도입, url과 매핑된 컨트롤러를 호출.

---
### v2 (중복 제거)
#### + 공통 View 호출 로직을 처리하는 객체(MyView)를 생성 
#### + 각 컨트롤러의 반환타입을 MyView로 

---
### v3 (종속성 제거)
#### + 서블릿 종속성 제거
#### + request객체를 사용하지않고 Model객체를 별도 생성,
#### + View 논리이름을 사용  (viewResolver로 실제 물리 뷰 경로로 변경)

---
### 4. v4 (편의성 추가)
#### + Controller에 모델, data를 "파라미터"로 넘김
#### + Controller가 ModelAndView를 반환하지않고 ViewName만 반환

---
### 5. v5 (확장성 추가)
#### + 프론트 컨트롤러에 어댑터 패턴 적용 (컨트롤러 인터페이스를 유연하게 변경할 수 있도록)
즉, 여러가지 컨트롤러 인터페이스(핸들러)가 존재할때 이 컨트롤러를 사용할 수 있도록 호환해주는 역할이 어댑터(핸들러 어댑터)

로직의 흐름
1. 어떤 URL이 들어왔을때 이 URL과 맵핑되는 핸들러가 있는지 조회
2. 그 핸들러를 처리할 수 있는 핸들러 어댑터 조회
3. (있다면) 핸들러 어댑터 호출
4. 핸들러 호출
5. ModelAndView를 반환
6. ViewResolver 호출
7. View를 반환
8. render호출
9. HTML응답

실제로 Spring의 MVC DispatcherServlet이 이 FrontController역할을 수행한다.  
**스프링 부트는 DispacherServlet을 서블릿으로 자동등록하고 모든경로("/")에 대해 매핑한다!!**  
**실제로 99% 사용하는 핸들러 매핑과 핸들러 어댑터 -> RequestMapping, RequestMappingHandlerAdapter**


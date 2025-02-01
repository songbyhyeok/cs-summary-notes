
# spring filter concept and using delegating filter proxy to apply bean filter

## servlet filter and filter chain
<img src="https://github.com/user-attachments/assets/b1415e56-bbee-417b-a1d7-5c48567f9d11" style="width: 30%; height: auto;">  

### servlet filter
서블릿 필터는 Java에서 요청과 응답을 가로채어 처리하는 컴포넌트로, 주로 인증, 로깅, 데이터 압축 등에 사용  

클라이언트 요청 시 DispatcherServelt, 하나 이상의 필터가 ChainFilter에 포함되어 Servlet에 의해 순차적으로 실행  

**" 하나의 요청은 한 서블릿만 처리할 수 있지만, 그 요청을 처리하는 데 여러 개의 필터가 사용될 수 있다. "**  

**filter role**  
```
* 서블릿/필터 개입 방지 및 응답 반환
* 요청/응답 수정 및 전달
```

### filter chain
```Java
// filterChain Usage ExampleFilter Role
public void dofilter(ServletRequest request, ServletResponse response, filterChain chain) {
	// do something before the rest of the application
    chain.dofilter(request, response); // invoke the rest of the application
    // do something after the rest of the application
}
```

여러 개의 필터가 순차적으로 요청/응답을 처리할 수 있도록 제공된 구조

<br>

## delegating filter proxy
<img src="https://github.com/user-attachments/assets/0beb9fb1-83d7-4781-93f8-e9e2a89349a5" style="width: 30%; height: auto;">  

ServletContainer와 ApplicationContext의 중계 역할

### servlet container
http 요청 처리 과정에서 Servlet이 BeanFilter 처리 결과를 클라이언트에게 응답하는 역할

### application context
BeanFilter 생성 제어/관리 역할

### delegating filter proxy role
ServletContainer가 BeanFilter를 사용하도록 ApplicationContext에서 필터를 요청하고 위임하는 역할

### lazy loading of delegating filter proxy
```Java
// DelegatingFilterProxy Pseudo Code
public void dofilter(ServletRequest request, ServletResponse response, filterChain chain) {
	filter delegate = getfilterBean(someBeanName);
	delegate.dofilter(request, response);
}
```

ServletContainer Filter 등록 시점과 ApplicationContext Bean 생성 및 로드 시점 간의 충돌을 방지하는 역할  

<br>

![Image](https://github.com/user-attachments/assets/c174acc7-9925-4f25-bb7e-65d632ae49d6)  

# reference
- [Servlet Filter 개념과 그리고 DelegatingFilterProxy를 사용한 Bean 필터 적용 과정](https://songbyhyeok.github.io/spring/spring-filter-concept-and-using-delegatingfilterproxy-to-apply-bean-filter/)

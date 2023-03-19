# CORS

## 예상 문제점 및 방안

<aside>
💡 동일 출처 정책(same-origin policy)으로 인한 **교차** **출처** **리소스** **공유**(Cross-Origin Resource Sharing, CORS) 이슈로, 시스템 내 팝업화면에서 타 도메인 페이지 진입 및 API 통신 불가능

</aside>

## 동일 출처 정책(same-origin policy, SOP)

1. 의의
    - 동일 출처 정책은 동일한 출처의 리소스에만 접근하도록 제한하는 정책.
    - 여기서 출처는 프로토콜, 호스트명, 포트가 같다는 것을 의미한다.
    - Internet Explorer 포트가 달라도 프로토콜, 호스트가 같으면 같은 출처로 판단한다.

## **교차** **출처** **리소스** **공유**(Cross-Origin Resource Sharing, CORS)

1. 의의
    - 추가 HTTP 헤더를 사용하여, 다른 출처 간에 리소스를 공유할 수 있도록 권한을 부여하도록 브라우저에 알려주는 체제
    - XMLHttpRequest 혹은 <img> 요소를 사용할 때 등의 상호작용을 통제
    - <iframe>은 [X-Frame-Options](https://www.notion.so/CORS-4b7102efd26a40e1973c3572ab3ef693) 헤더를 사용해 교차 출처 프레임의 대상이 되는 것을 방지
2. CORS 요청 종류
    - **Simple Requests**
        - GET, POST, HEAD 메서드 중 하나를 만족
        - CONTENT TYPE
            1. application/x-www-form-urlencoded
            2. multipart/form-data
            3. text/plain
        - 헤더는 Accept, Accept-Language, Content-Language, Content-Type 만 허용
        - 요청 헤더 예제
            
            ```jsx
            요청 헤더 예제
            GET /resources/public-data/ HTTP/1.1
            User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
            Accept-Language: en-us,en;q=0.5
            Connection: keep-alive
            ```
            
        - 응답 헤더 예제
            
            ```jsx
            HTTP/1.1 200 OK
            Server: Apache/2
            Keep-Alive: timeout=2, max=100
            Transfer-Encoding: chunked
            ```
            
            **Access-Control-Allow-Origin** 헤더에는 요청의 Origin 헤더에서 전송된 값이 포함되어야 리소스에 대한 접근을 허용
            
    - **Preflight Request**
        - Simple Request 조건에 해당하지 않으면 브라우저는 Preflight Request 방식으로 요청
        - Preflight Request는 GET, HEAD, POST 외의 다른 방식으로도 요청을 보낼 수 있고, application/xml처럼 다른 Content-type으로 요청을 보낼 수도 있으며, 커스텀 헤더도 사용할 수 있다
    - **Request with Credential**
        - HTTP Cookie와 HTTP Authentication 정보(**토큰**)를 인식할 수 있게 해주는 요청
        - 클라이언트 측에서 **XMLHttpRequest.withCredentials = true**를 지정해서 Credential 요청, 서버는 Response Header에 반드시 **Access-Control-Allow-Credentials: true**를 포함
        - Response Header에 **Access-Control-Allow-Origin** 헤더의 값이 *가 아닌 http://foo.origin과 같은 **구체적인 도메인 지정**



## **교차 출처 스크립트 API [Window.postMessage()]**

1. 의의
window.postMessage() 메소드는 Window 오브젝트 사이에서 안전하게 cross-origin 통신을 할 수 있게 한다.
페이지와 생성된 팝업 간의 통신이나, 페이지와 페이지 안의 iframe 간의 통신 가능
window.postMessage()는 동일 출처 정책인 제약 조건을 안전하게 우회하는 기능을 제공
2. 문법

```jsx
//자식창에서 부모창으로 데이터를 전달하는 방법
window.onload = function() {
	console.log('child load');
	targetWindow.postMessage(message, targetOrigin, [transfer]);
	window.parent.postMessage({ childData : 'test data' }, 'http://abc.com');
};
//자식창이 보낸 데이터를 부모창이 받아서 활용하는 방법
window.addEventListener('message', function(e) {
  console.log('parent message');
  console.log(e.data); // { childData : 'test data' }
  console.log("e.origin : " + e.origin); //http://123.com(자식창 도메인)
  if(e.data.childData === 'test data'){
	...처리 로직 (부모창 함수 호출)
  }
});
```

## **X-Frame-Options**

1. 의의
The X-Frame-Options HTTP 응답 헤더는 해당 페이지를 <frame> 또는<iframe>,
    
    <object> 에서 렌더링할 수 있는지 여부를 나타내는데 사용
    
2. 문법

```jsx
X-Frame-Options: deny
X-Frame-Options: sameorigin
X-Frame-Options: allow-from https://example.com/

Deny: 어떠한 사이트에서도 frame 상에서 보여 질 수 없음
Sameorigin: 동일한 사이트의 frame에서만 보임
allow-from uri: 지정된 특정 uri의 frame 에서만 보임
```
</br>
  
# 결론

타도메인과 통신은 X-Frame-Options 헤더를 사용해 교차 출처 프레임의 대상이 되는 것을 방지하고, Window.PostMessage API로 동일 출처 제약 조건을 안전하게 우회하는 기능을 사용하여, SPO 정책에 위배되지 않고 안전하게 iframe 사용이 가능

- 예외사항: 기존 시스템 내에서 iframe으로 타 도메인 접속이 되며 같은 도메인 URI을 받을 경우 CORS이슈는 없을 것으로 예상

### 타 도메인 **시스템 요청사항**

1. 타 도메인 시스템 서버에 Response 헤더에 Xframe Option설정 요청
    
    (X-Frame-Options: allow-from 타도메인 uri)
    
2. Window.PostMessage API로 데이터 송수신 요청

### 기존 **시스템 설정**

1. Window.PostMessage API로 데이터 송수신

## 참고한 자료 📰

- 동일출처정책: [https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy](https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy)
- 교차 출처 리소스 공유 (CORS): [https://developer.mozilla.org/ko/docs/Web/HTTP/CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)
- X-Frame-Options: [https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/X-Frame-Options](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/X-Frame-Options)
- PostMessage: [https://developer.mozilla.org/ko/docs/Web/API/Window/postMessage](https://developer.mozilla.org/ko/docs/Web/API/Window/postMessage)

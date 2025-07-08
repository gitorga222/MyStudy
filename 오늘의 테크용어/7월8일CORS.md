# 'CORS' 7월 8일 2025년


📖 작성자: [kimsee8200](https://github.com/kimsee8200)
## CORS는 도대체 왜 생겼는가?

CORS(Cross Origin Resource Shering, 교차 출처 자원 공유)는 한 사이트에서 다른 사이트의 자원을 요구할 때 그 요구를 차단하거나 받아주는 것을 결정하는 것이다. 이는 서버간에는 적용되지 않고, 웹사이트 -> 서버에서 적용, 즉 웹사이트에서만 적용되는 것이다.

이 문제는 바로 브라우저에서 사용자가 접근한 웹사이트를 다른 사이트에서 신뢰할 수 없기 때문에 이를 차단하는 것이다. 악의적인 웹페이지에서 다른 사이트의 리소스에 접근한다는 것은 해당 사이트의 정보가 유출 될 수도 있기에 이를 차단하는 것이다.

## Origin, 출처
CORS의 중요한 부분은 바로 'origin (출처)'이다. origin은 프로토콜 (protocol), 호스트 (host) 그리고 포트 (port)로 나누어져 있다. 우리가 늘상 아는 http://localhost:8080 에서 http가 프로토콜, localhost가 호스트, 8080이 포트가 되는 것이다. 이들이 동일하다면 '동일 출처', 다르다면 '교차 출처'라  부른다.


## 교차 출처 열기
그러나 교차 출처는 어쩔 수 없이 발생한다. 왜냐하면, 프론트에서 웹페이지를 구동하는 서버와 백엔드에서 정보를 제공하는 서버는 달라 호스트가 동일하지 않다. 그렇기에 CORS는 협업을 할때 매우 많이 발생하는 문제 중 하나이다.

그럼 이것을 어떻게 해결할까? 이때 서버쪽에서는 신뢰할 수 있는 교차 출처를 예외로 허용할 수 있게 된다. 작동 원리는 다음과 같다.
kimsee.com (클라이언트) -> kimseeServer.net (서버)
1. 클라이언트의 해더에 origin을 추가한다. (kimsee.com이 추가될 것이다.)
2. kimseeServer.net에서 예외로 설정해 두었다면 요청을 처리하고 응답으로 Access-Control-Allow-Origin을 함깨 보낸다. 
3. 브라우저에서 Access-Control-Allow-Origin에 kimsee.com이 있는지 확인하고, 없다면 CORS 오류를, 있다면 요청이 정상적으로 처리된다.

## Spring에서의 CSRF
스프링에서는 이를 매우 간단하게 적용할 수 있다. Spring security 를 활용하여 CORS 예외 설정을 해도 되고,   컨트롤러에 아래 이미지에 있는 어노테이션을 활용해 사용할 수도 있다. ![Spring CORS](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQKICHV3138Qfc_yjttOobV2tcxh6HqCr2nhA&s)
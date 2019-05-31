* BOM(Browser Object Model)이란 웹브라우저의 창이나 프래임을 추상화해서 프로그래밍적으로 제어할 수 있도록 제공하는 수단이다. BOM은 전역객체인 Window의 프로퍼티와 메소드들을 통해서 제어할 수 있다. 따라서 BOM에 대한 수업은 Window 객체의 프로퍼티와 메소드의 사용법을 배우는 것이라고 해도 과언이 아닐 것이다. 본 토픽의 하위 수업에서는 Window 객체의 사용법을 알아볼 것이다.

* window 객체
  * Window 객체는 모든 객체가 소속된 객체이고, 전역객체이면서, 창이나 프레임을 의미한다. 

* 전역객체
  * Window 객체는 식별자 window를 통해서 얻을 수 있다. 또한 생략 가능하다. Window 객체의 메소드인 alert을 호출하는 방법은 아래와 같다.
  * alert('Hello world'); = window.alert('Hello world');
    * alert은 암묵적으로 window 전역객체를 사용
  * 아래는 전역변수 a에 접근하는 방법이다.  
    * var a = 1; alert(a); alert(window.a);
  * 객체를 만든다는 것은 결국 window 객체의 프로퍼티를 만드는 것과 같다.
    * var a = {id:1}; alert(a.id); alert(window.a.id);
  * 예제를 통해서 알 수 있는 것은 전역변수와 함수가 사실은 window 객체의 프로퍼티와 메소드라는 것이다. 또한 모든 객체는 사실 window의 자식이라는 것도 알 수 있다. 이러한 특성을 ECMAScript에서는 Global 객체라고 부른다. ECMAScript의 Global 객체는 호스트 환경에 따라서 이름이 다르고 하는 역할이 조금씩 다르다. 웹브라우저 자바스크립트에서 Window 객체는 ECMAScript의 전역객체이면서 동시에 웹브라우저의 창이나 프레임을 제어하는 역할을 한다.

* 사용자와 커뮤니케이션 하기
  * HTML은 form을 통해서 사용자와 커뮤니케이션할 수 있는 기능을 제공한다. 자바스크립트에는 사용자와 정보를 주고 받을 수 있는 간편한 수단을 제공한다.
  * alert()
    * 경고창이라고 부른다. 사용자에게 정보를 제공하거나 디버깅등의 용도로 많이 사용한다.
  * confirm()
    * 확인/취소를 가진 컨펌 팝업 창
    * 확인을 누르면 true, 취소를 누르면 false를 리턴한다.
  * prompt()
    * 사용자로 부터 입력을 받을 수 있는 창. 입력값을 리턴

* Location 객체
  * Location 객체는 문서의 주소와 관련된 객체로 Window 객체의 프로퍼티다. 이 객체를 이용해서 윈도우의 문서 URL을 변경할 수 있고, 문서의 위치와 관련해서 다양한 정보를 얻을 수 있다.
  * 현재 윈도우의 URL 알아내기
    * 아래는 현재 윈도우의 문서가 위치하는 URL을 알아내는 방법이다.
      * console.log(location.toString(), location.href);
  * URL Parsing
    * location 객체는 URL을 의미에 따라서 별도의 프로퍼티로 제공하고 있다. 
      * console.log(location.protocol, location.host, location.port, location.pathname, location.search, location.hash)
    * http://opentutorials.org:80/module/1?id=1#hash
      * location 프라퍼티로 얻음 -> protocol: http, host: opentutorials.org, port: 80, pathname: /module/1, search: ?id=1, hash: #hash
  * URL 변경하기
    * 아래 코드는 현재 문서를 http://egoing.net으로 이동한다.
      * location.href = 'http://egoing.net';
      * location = 'http://egoing.net';
    * 아래는 현재 문서를 리로드하는 간편한 방법을 제공한다.
      * location.reload();

* Navigator 객체
  * 브라우저의 정보를(제품명, 버전) 제공하는 객체다. 주로 호환성 문제등을 위해서 사용한다. (브라우저 종류 특성에 맞는 코드 작성 시 사용) 
  * W3C, ECMA 국제표준화기구 정의한 스펙에 따라 ie, ff, chrome, sa, op 브라우저를 만듦
  * 브라우저마다 다르게 발생되는 문제를 cross browsing 이슈라고 함

  * 아래 명령을 통해서 이 객체의 모든 프로퍼티를 열람할 수 있다.
    * console.dir(navigator);
    * appName
      * 웹브라우저의 이름이다. IE는 Microsoft Internet Explorer, 파이어폭스, 크롬등은 Nescape로 표시한다.
    * appVerstion
      * 브라우저의 버전을 의미한다. 필자의 현재 브라우저 정보는 아래와 같다.
      * "5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36"
    * userAgent
      * 브라우저가 서버측으로 전송하는 USER-AGENT HTTP 헤더의 내용이다. appVersion과 비슷하다.
      * "5.0 (Windows NT 6.3; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36"
    * platform
      * 브라우저가 동작하고 있는 운영체제에 대한 정보다.
      * "Win32"

  * 기능 테스트
    * Navigator 객체는 브라우저 호환성을 위해서 주로 사용하지만 모든 브라우저에 대응하는 것은 쉬운 일이 아니므로 아래와 같이 기능 테스트를 사용하는 것이 더 선호되는 방법이다. 
    * 예를 들어 Object.keys라는 메소드는 객체의 key 값을 배열로 리턴하는 Object의 메소드다. 이 메소드는 ECMAScript5에 추가되었기 때문에 오래된 자바스크립트와는 호환되지 않는다. 아래의 코드를 통해서 호환성을 맞출 수 있다. 
      * if (!Object.keys) {
         Object.keys = (function () {
             ...

* 창 제어
  * window.open()
    * window.open 메소드는 새 창을 생성한다. 현대의 브라우저는 대부분 탭을 지원하기 때문에 window.open은 새 창을 만든다. 아래는 메소드의 사용법이다.
  * 상호작용 (열려있는 윈도우 페이지 간)
    * demo3.html 참고

* 보안
  * 사용자의 인터렉션이 없이 창을 열려고 하면 팝업이 차단된다.
    * window.open('demo2.html'); 
  * 같은 도메인 안에서만 상호작용 가능
  
* jQuery
  * Javascript 라이브러리를 통해 쉽게 elements 조회할 수 있음  
  * jQuery는 DOM을 내부에 감추고 보다 쉽게 웹페이지를 조작할 수 있도록 돕는 도구이다. jQuery의 효용은 후속 수업을 통해서 살펴보자.
  * jQuery를 이용하면 DOM을 사용하는 것 보다 훨씬 효율적으로 필요한 객체를 조회할 수 있다. jQuery는 객체를 조회할 때 CSS 선택자를 이용한다.

* jQuery의 기본문법
  * $('li').css('color', 'red')     // document.getElementsByTagName
    * **$()는 jQuery의 함수**이다. 이 함수의 인자로 CSS 선택자(li)를 전달하면, **jQuery 객체라는 것을 리턴**한다. 이 객체는 선택자에 해당하는 엘리먼트를 제어하는 다양한 메소드를 가지고 있다. 위의 그림에서 css는 선택자에 해당하는 객체들의 style에 color:red로 변경한다
  * $('.active').css('color', 'red')    // document.getElementsByClassName
  * $('$active').css('color', 'red').css('textDecoration', 'underline') // document.getElementById

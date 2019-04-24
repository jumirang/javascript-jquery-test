* DOM (Document Object Model)
  * Document Object Model로 웹페이지를 자바스크립트로 제어하기 위한 객체 모델을 의미한다. window 객체의 document 프로퍼티를 통해서 사용할 수 있다. Window 객체가 창을 의미한다면 Document 객체는 윈도우에 로드된 문서를 의미한다고 할 수 있다. DOM의 하위 수업에서는 문서를 제어하는 방법에 대한 내용을 다룬다. 

* 제어 대상 찾기
  * 문서를 자바스크립트로 제어하려면 제어의 대상에 해당되는 객체를 찾는 것이 제일 먼저 할 일이다. 문서 내에서 객체를 찾는 방법은 document 객체의 메소드를 이용한다. 
    * document.getElementsByTagName
      * 문서 내에서 특정 태그에 해당되는 객체를 찾는 방법은 여러가지가 있다. getElementsByTagName은 인자로 전달된 태그명에 해당하는 객체들을 찾아서 그 리스트를 NodeList라는 유사 배열에 담아서 반환한다. NodeList는 배열은 아니지만 length와 배열접근연산자를 사용해서 엘리먼트를 조회할 수 있다.
        * var lis = document.getElementsByTagName('li');
      * 만약 조회의 대상을 좁히려면 아래와 같이 특정 객체를 지정하면 된다. 이러한 원칙은 다른 메소드에도 적용된다.
        * var ul = document.getElementsByTagName('ul')[0];
          var lis = ul.getElementsByTagName('li');
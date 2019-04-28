* Document 객체
  ![Document structure](./Document_structure.png)
  * Document 객체는 DOM의 스팩이고 이것이 웹브라우저에서는 HTMLDocument 객체로 사용된다. HTMLDocument 객체는 문서 전체를 대표하는 객체라고 할 수 있다. 아래 코드는 이를 보여준다.
  ```javascript
    <script>
    //document 객체는 window 객체의 소속이다.
    console.log(window.document);
    //document 객체의 자식으로는 Doctype과 html이 있다. 
    console.log(window.document.childNodes[0]);
    console.log(window.document.childNodes[1]);
    </script>
  ```
  * 주요 API
    * 노드 생성 API
      * document  객체의 주요 임무는 새로운 노드를 생성해주는 역할이다. 이에 대한 내용은 노드 변경 API에서 학습했기 때문에 여기서는 언급하지 않는다.
        * createElement()
        * createTextNode()

  * 문서 정보 API
    * title
    * URL
    * referrer : 문서가 어떠한 사이트를 경우에서 오게 되었는지 관한 정보
    * lastModified
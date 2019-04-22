* inline
  * inline 방식은 태그에 직접 자바스크립트를 기술하는 방식이다. 장점은 태그에 연관된 스크립트가 분명하게 드러난다는 점이다. 하지만 정보와 제어가 섞여 있기 때문에 정보로서의 가치가 떨어진다.
  * 해결방법 : script tag
* script
  * HTML 안의 <script></script> 태그를 만들어서 여기에 자바스크립트 코드를 삽입하는 방식이다. 장점은 html 태그와 js 코드를 분리할 수 있다는 점이다. 
* 외부파일로 분리
  * js를 별도의 파일로 분리할 수도 있다. 장점은 보다 엄격하게 정보와 제어를 분리할 수 있다. 하나의 js 파일을 여러 웹페이지에서 로드함으로서 js의 재활용성을 높일 수 있다. 캐쉬를 통해서 속도의 향상, 전송량의 경량화를 도모할 수 있다.
* jQuery 객체
  * jQuery 함수의 리턴값으로 jQuery 함수를 이용해서 선택한 엘리먼트들에 대해서 처리할 작업을 프로퍼티로 가지고 있는 객체다.

  * 암시적 반복
    * jQuery 객체의 가장 중요한 특성은 암시적인 반복을 수행한다는 것이다. DOM과 다르게 jQuery 객체의 메소드를 실행하면 선택된 엘리먼트 전체에 대해서 동시에 작업이 처리된다. 암시적 반복은 값을 설정할 때만 동작한다. 값을 가져올 때는 선택된 엘리먼트 중 첫번째에 대한 값만을 반환한다. 이에 대한 내용은 아래에서 살펴본다.

    * li.css('text-decoration', 'underline'); // setter
      li.css('text-decoration'); // getter

  * 체이닝
    * chainig이란 선택된 엘리먼트에 대해서 연속적으로 작업을 처리할 수 있는 방법이다.
    * li.css('text-decoration', 'underline').('color', ''red);

  * jQuery 객체에는 조회된 엘리먼트가 담겨 있다. jQuery 객체는 일종의 유사배열의 형태로 조회된 엘리먼트를 가지고 있기 때문에 배열처럼 사용해서 엘리먼트를 가져올 수 있다.
  

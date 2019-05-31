## 네트워크 통신
* 본 토픽의 하위 토픽에서는 자바스크립트를 이용해서 웹브라우저의 통신 기능을 사용하는 방법을 알아본다. 이 중에서 서버와 클라이언트 간의 데이터를 주고 받는 형식으로서 JSON과 페이지 리로드 없이 웹페이지의 내용을 변경할 수 있는 Ajax는 웹에플리케이션을 구축하는데 중요한 내용이기 때문에 주의해서 학습하자.

---
* Ajax
  * 웹브라우저는 대단히 정적인 시스템이었다. 내용이 바뀌면 페이지 새로고침을 해서 내용을 새롭게 변경해야 했다. 이것은 웹이 전자 문서를 염두에 두고 고안된 시스템이기 때문에 당연하게 생각 되었다. 
  
  * 그러다 Ajax 개념이 도입되면서 모든 것이 바뀌었다. Ajax는 웹브라우저와 웹서버가 내부적으로 데이터 통신을 하게 된다. 그리고 변경된 결과를 웹페이지에 프로그래밍적으로 반영함으로써 웹페이지의 로딩 없이 서비스를 사용할 수 있게 한다. 
  
  * Ajax는 Asynchronous JavaScript and XML의 약자다. 한국어로는 비동기적 자바스크립트와 XML 정도로 직역할 수 있는데 자바스크립트를 이용해서 비동기적으로 서버와 브라우저가 데이터를 주고 받는 방식을 의미한다. 이 때 사용하는 API가 XMLHttpRequest이다. 그렇다고 꼭 XML을 사용해서 통신해야 하는 것은 아니다. 사실 XML 보다는 JSON을 더 많이 사용한다.
  
  * Ajax의 핵심은 클라이언트가 서버로 특정 요청을 했을 때 서버의 응답을 기다린 후 다음 동작을 하는 기존 형태(동기 방식)와 달리 클라이언트가 서버의 응답을 받기 전에 다른 동작을 수행하고 서버의 응답이 도착하면 그 응답에 대한 처리를 하는 형태(비동기식)이다.
  Ajax를 이용하면 페이지 갱신없이 페이지의 일부를 변경하는 것등이 가능하며 응답속도가 빠른 웹페이지를 만들 수 있다.
  
  * Ajax 자체가 특정 언어나 함수 또는 라이브러리를 의미하진 않으며 상기와 같이 비동기적으로 클라이언트-서버간 요청/응답 처리를 하는 방식 자체를 의미한다.
  
  * 일반적으로 Ajax는 cross domain에서 작동하지 않는다. 예를들어 http://www.server1.com에서 로딩된 웹페이지에서 Ajax 호출을 통해 http://www.server2.com의 리소스를 호출할 수 없다.
  다만, 최근의 브라우저는 이를 해결하기 위해서 CORS(Cross-Origin Resource Sharing) 기술을 지원한다.

* XMLHttpRequest 객체
  * XMLHttpRequest 객체 사용이 Ajax를 사용하는 것임
  * Ajax에서는 XMLHttpRequest라는 자바스크립트 객체(object)를 사용한다.
  * XHR이라고도 줄여부르기도 하며 Microsoft에서 처음 만들었지만 모질라등 여러 업체에서 지원하고 있다.
    XHR 객체의 속성 및 메소드를 이용하여 비동기적 요청/응답 처리를 할 수 있다.

  * XHR을 이용하여 구현된 Ajax는 하기와 같은 4가지 단계를 가진다.
    1. XHR 객체 인스턴스 생성
      : 비동기 요청을 할 준비를 하는 과정으로 new를 이용해 XHR 객체의 인스턴스를 생성한다.
    2. Callback 함수 등록
      : 서버로부터 응답이 왔을 때 호출될 callback 함수의 실제 구현부를 생성하고 이를 XHR 객체 인스턴스에 등록한다.
    3. Open a request
      : http 메소드(GET, POST 등)를 정하고 접속 url을 정한다.
    4. Send a request 
      : 실제 요청을 보내는 동작이다.

  * 하기는 XHR 객체를 이용한 예이다.
  ```javascript
    <!DOCTYPE html>
    <html>
    <body>
    <div id="demo">
    <h2>Let AJAX change this text</h2>
    <button type="button" onclick="loadDoc()">Change Content</button>
    </div>
    </body>
    </html>

    function loadDoc() {
        var xhttp = new XMLHttpRequest(); //1번 동작
        xhttp.onreadystatechange = function() { //2번 동작
            if (this.readyState == 4 && this.status == 200) {
                document.getElementById("demo").innerHTML = this.responseText;
            }
        };
        xhttp.open("GET", "http://test.com/ajax_info.txt", true); //3번 동작
        xhttp.send(); //4번 동작
    }
  ```

  * 제이쿼리에서는 XHR 객체를 제이쿼리 형태로 추상화해서 사용하고 있다. 따라서 직접적으로 XHR을 이용하진 않지만 브라우저 내부에서 동작하는 기본은 상기 과정이라고 할 수 있겠다.
  
  * 아래 코드는 현재 시간을 출력한다.
  ```php
    // time1.php (서버역할)
    <?php
    $d1 = new DateTime;
    $d1->setTimezone(new DateTimezone("asia/seoul"));
    echo $d1->format('H:i:s');
    ?>
  ```
  ```javascript
    // demo1.html
    <p>time : <span id="time"></span></p>
    <input type="button" id="execute" value="execute" />
    <script>
        document.querySelector('input').addEventListener('click', function(event){
        var xhr = new XMLHttpRequest();

        // 접속하려는 대상을 지정한다. 첫번째 인자는 form 태그의 method에 대응하는 것으로 GET/POST 방식을 주로 사용한다. 두번째 인자는 접속하고자 하는 서버쪽 리소스의 주소로 form 태그의 action에 해당한다.
        xhr.open('GET', './time.php');

        // onreadystatechange 이벤트는 서버와의 통신이 끝났을 때 호출되는 이벤트이다. readyState는 통신의 현재 상태를 알려준다. 4는 통신이 완료되었음을 의미한다. status는 HTTP 통신의 결과를 의미하는데 200은 통신이 성공했음을 의미한다. responseText 프로퍼티는 서버에서 전송한 데이터를 담고 있다. 이것을 id가 time 엘리먼트의 하위로 삽입한다. 이를 통해서 현재 서버에서 가져온 현재시간을 페이지 리로딩 없이 가져올 수 있다.
        xhr.onreadystatechange = function(){
            if(xhr.readyState === 4 && xhr.status === 200){
                document.querySelector('#time').innerHTML = xhr.responseText;
            }
        }
        xhr.send(); 
        }); 
    </script> 
  ```

  * POST 방식
   ```php
    // time2.php (서버역할)
    <?php
    $d1 = new DateTime;
    $d1->setTimezone(new DateTimezone($_POST['timezone']));
    echo $d1->format($_POST['format']);
    ?>
  ```
  ```javascript
    // demo2.html
    <p>time : <span id="time"></span></p>
    <select id="timezone">
        <option value="Asia/Seoul">asia/seoul</option>
        <option value="America/New_York">America/New_York</option>
    </select>
    <select id="format">
        <option value="Y-m-d H:i:s">Y-m-d H:i:s</option>
        <option value="Y-m-d">Y-m-d</option>
    </select>
    <input type="button" id="execute" value="execute" />
    <script>
        document.querySelector('input').addEventListener('click', function(event){
            var xhr = new XMLHttpRequest();
            xhr.open('POST', './time2.php');
            xhr.onreadystatechange = function(){
                document.querySelector('#time').innerHTML = xhr.responseText;
            }
            // 서버로 전송할 데이터 타입의 형식(MIME)을 지정한다. 
            xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
            // 서버로 전송할 데이터를 형식에 맞게 만든다. 이름=값&이름=값... 의 형식을 지켜야 한다.
            var data = '';
            data += 'timezone='+document.getElementById('timezone').value;
            data += '&format='+document.getElementById('format').value;
            xhr.send(data); 
        });
    </script>
  ```

---
* JSON
  * JSON(JavaScript Object Notation)의 약자로 JavaScript에서 객체를 만들 때 사용하는 표현식을 의미한다. 이 표현식은 사람도 이해하기 쉽고 기계도 이해하기 쉬우면서 데이터의 용량이 작다. 이런 이유로 최근에는 JSON이 XML을 대체해서 설정의 저장이나 데이터를 전송등에 많이 사용된다. JSON에 대한 자세한 내용은 아래 JSON의 공식홈페이지를 참조한다.
  * http://www.json.org/json-ko.html

* JSON API
  * ECMAscript 5에는 JSON을 공식적으로 지원하는 API가 포함되었다. 
  * JSON.parse()
    * 인자로 전달된 문자열을 자바스크립트의 데이터로 변환한다.
  * JSON.stringify()
    * 인자로 전달된 자바스크립트의 데이터를 문자열로 변환한다.

* Ajax와 JSON
  * 만약 PHP의 배열을 그대로 자바스크립트에서 사용할 수 있다면? 반대로 자바스크립트의 배열을 그대로 PHP에서 사용할 수 있다면 얼마나 편리할까? 이 때 사용하는 것이 JSON이다.

  ```php
    // time3.php (서버역할)
    <?php
    $timezones = ["Asia/Seoul", "America/New_York"];
    header('Content-Type: application/json');
    echo json_encode($timezones);
    ?>
  ```
  ```javascript
    // demo3.html
    <p id="timezones"></p>
    <input type="button" id="execute" value="execute" />
    <script>
    document.querySelector('input').addEventListener('click', function(event){
        var xhr = new XMLHttpRequest();
        xhr.open('GET', './time2.php');
        xhr.onreadystatechange = function(){
            if(xhr.readyState === 4 && xhr.status === 200){
                var _tzs = xhr.responseText;
                var tzs = JSON.parse(_tzs);
                var _str = '';
                for(var i = 0; i< tzs.length; i++){
                    _str += '<li>'+tzs[i]+'</li>';
                }
                _str = '<ul>'+_str+'</ul>';
                document.querySelector('#timezones').innerHTML = _str;
            }
        }
        xhr.send(); 
    }); 
    </script> 
  ```

  * 서버로 데이터 전송
    ```php
    // time4.php (서버역할)
    <?php
    $data = json_decode(file_get_contents('php://input'), true);
    $d1 = new DateTime;
    $d1->setTimezone(new DateTimezone($data['timezone']));
    echo $d1->format($data['format']);
    ?>
    ```
    ```javascript
    // demo4.html
    <p>time : <span id="time"></span></p>
    <select id="timezone">
        <option value="Asia/Seoul">asia/seoul</option>
        <option value="America/New_York">America/New_York</option>
    </select>
    <select id="format">
        <option value="Y-m-d H:i:s">Y-m-d H:i:s</option>
        <option value="Y-m-d">Y-m-d</option>
    </select>
    <input type="button" id="execute" value="execute" />
    <script>
    document.querySelector('input').addEventListener('click', function(event){
        var xhr = new XMLHttpRequest();
        xhr.open('POST', './time3.php');
        xhr.onreadystatechange = function(){
            document.querySelector('#time').innerHTML = xhr.responseText;
        }
        var data = new Object();
        data.timezone = document.getElementById('timezone').value;
        data.format = document.getElementById('format').value;
        xhr.setRequestHeader("Content-Type", "application/json");
        xhr.send(JSON.stringify(data)); 
    });
    </script>
    ```

---
* jQuery Ajax
  * jQuery이용해서 Ajax를 사용하게 되면 많은 이점이 있는데 그 중의 하나가 크로스브라우징의 문제를 jQuery가 알아서 해결해준다는 것이다. 뿐만 아니라 여러가지 편리한 기능들을 제공한다. 이번 시간에는 jQuery를 이용해서 Ajax 통신을 하는 법을 알아보자.
  * jQuery는 Ajax와 관련해서 많은 API를 제공한다. 
  * http://api.jquery.com/category/ajax/
  * 그 중에서 가장 중요한 API는 $.ajax이다.
    * http://api.jquery.com/jQuery.ajax/

  * $.ajax의 문법 : jQuery.ajax( [settings ] )
    * setting는 Ajax 통신을 위한 옵션을 담고 있는 객체가 들어간다. 주요한 옵션을 열거해보면 아래와 같다.
      * data : 서버로 데이터를 전송할 때 이 옵션을 사용한다. 
      * dataType : 서버측에서 전송한 데이터를 어떤 형식의 데이터로 해석할 것인가를 지정한다. 값으로 올 수 있는 것은 xml, json, script, html이다. 형식을 지정하지 않으면 jQuery가 알아서 판단한다.
      * success : 성공했을 때 호출할 콜백을 지정한다. Function( PlainObject data, String textStatus, jqXHR jqXHR )
      * type : 데이터를 전송하는 방법을 지정한다. get, post를 사용할 수 있다.

  * GET 방식
  ```php
    <?php
    $d1 = new DateTime;
    $d1->setTimezone(new DateTimezone("asia/seoul"));
    echo $d1->format('H:i:s');
    ?>
  ```
  ```javascript
    <p>time : <span id="time"></span></p>
    <input type="button" id="execute" value="execute" />
    <script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
    <script>
    $('#execute').click(function(){
        $.ajax({
            url:'./time.php',
            success:function(data){
                $('#time').append(data);
            }
        })
    })
    </script>
  ```

  * POST 방식
  ```php
    <?php
    $d1 = new DateTime;
    $d1->setTimezone(new DateTimezone($_POST['timezone']));
    echo $d1->format($_POST['format']);
    ?>
  ```
  ```javascript
    <p>time : <span id="time"></span></p>
    <form>
    <select name="timezone">
        <option value="Asia/Seoul">asia/seoul</option>
        <option value="America/New_York">America/New_York</option>
        </select>
    <select name="format">
        <option value="Y-m-d H:i:s">Y-m-d H:i:s</option>
        <option value="Y-m-d">Y-m-d</option>
        </select>
    </form>
    <input type="button" id="execute" value="execute" />
    <script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
    <script>
    $('#execute').click(function(){
        $.ajax({
            url:'./time2.php',
            type:'post',
            data:$('form').serialize(),
            success:function(data){
                $('#time').text(data);
            }
        })
    })
    </script>
  ```

  * JSON 처리
  ```php
    <?php
    $timezones = ["Asia/Seoul", "America/New_York"];
    echo json_encode($timezones);
    ?>
  ```
  ```javascript
    <p id="timezones"></p>
    <input type="button" id="execute" value="execute" />
    <script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
    <script>
    $('#execute').click(function(){
        $.ajax({
            url:'./time3.php',
            dataType:'json',
            success:function(data){
                var str = '';
                for(var name in data){
                    str += '<li>'+data[name]+'</li>';
                }
                $('#timezones').html('<ul>'+str+'</ul>');
            }
        })
    })
    </script>
  ```

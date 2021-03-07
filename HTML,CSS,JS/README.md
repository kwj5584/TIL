## 브라우저 작동원리
<hr/>

### 브라우저 기본 구조
    1. 사용자 인터페이스 - 주소 표시줄, 이전/다음 버튼, 북마크 메뉴등. 요청한 페이지를 보여주는 창 제외한 나머지 모든 부분.
    2. 브라우저 엔진 - 사용자 인터페이스와 렌더링 엔진사이의 동작을 제어.
    3. 렌더링 엔진 - 요청한 콘텐츠를 표시.
    4. 통신 - HTTP요청과 같은 네트워크 호출에 사용됨.
    5. UI 백엔드 - 콤보 박스와 창 같은 기본적인 장치를 그림. 
    6. 자바스크립트 해석기 - 자바스크립트 코드를 해석하고 실행.
    7. 자료 저장소 - 자료를 저장하는 계층. 모든 종류의 자원을 하드 디스크에 저장할 필요가 있음.

### 렌더링 엔진 작동 방식
    렌더링 엔진은 웹 서버로부터 전달받은 HTML 문서를 맨 처음 네트워크 레이어에서 불러옴. 

    1. HTML 파싱 후 DOM 트리 만들기
    2. 렌더 트리(Render Tree) 만들기
    3. 렌더 트리(Render Tree) 레이아웃 만들기
    4. 렌더 트리 페인팅(Render Tree Painting)

    1. HTML파싱 후 DOM트리 만들기
        네트워크 레이어를 통해 전달받은 HTML문서를 파싱하여 각 요소들을 DOM Tree의 각 DOM노드들로 전환. 
        DOM이란 Document object model의 줄임말로 마크업 형태의 HTML문서를 오브젝트 모델의 형태로 바꿔놓은 것.

    2. 렌더 트리(Render Tree)만들기
        HTML문서들을 파싱하여 DOM Tree를 구성한 후, 렌더링 엔진은 CSS/Style 데이터를 파싱하고 그 스타일 데이터들로
        렌더 트리를 만듬. DOM트리가 웹 상에 나타날 내용을 구성한다면 Render Tree는 시각적 요소, 어떻게 나타날지 스타일을 지정.

    3. 렌더 트리(Render Tree) 레이아웃 만들기
        레이아웃을 만든다는 것은 각 노드들에게 스크린의 어느 공간에 위치해야 할지 각각의 값(Position, Size)을 부여하는 것.

    4. 렌더 트리 페인팅(Render Tree Painting)
        렌더 트리가 만들어져 레이아웃이 구성되었다면, UI 백엔드가 동작하여 각 노드들을 정해진 스타일 및 위치값대로 화면에 배치.
        더 나은 UX(User experience)를 위해, 렌더링 엔진은 각 콘텐츠를 가능한 빨리 스크린에 띄워야 한다.

## 호이스팅(Hoisting)
<hr/>

### 호이스팅의 개념
    함수 안에 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것.
    
### 호이스팅의 대상
    var 변수 선언과 함수선언문에서만 호이스팅이 일어난다.
    var 변수/ 함수 선언만 위로 끌어 올려지며, 할당은 끌어 올려지지 않는다.
    let/const 변수 선언과 함수 표현식에서는 호이스팅이 발생하지 않는다.
    변수 선언이 함수 선언보다 위로 끌어올려진다.

## 클로저
<hr/>

### 클로저란?
    클로저는 독립적인 (자유) 변수를 가리키는 함수. 또는, 함수 내에서 함수를 정의하고 사용하면 클로저라고 한다.
### 예제    
    function hello(name) {
    var _name = name;
    return function() {
        console.log('Hello, ' + _name);
    };
    }

    var hello1 = hello('승민');
    var hello2 = hello('현섭');
    var hello3 = hello('유근');

    hello1(); // 'Hello, 승민'
    hello2(); // 'Hello, 현섭'
    hello3(); // 'Hello, 유근'

## Margin, Padding 속성의 차이점
<hr/>

    Margin은 Object와 화면과의 여백(외부여백)을 말하며 Padding은 Object내의 내부여백

    Margin, Padding 속성 개수
        1개 : top/bottom/left/right 모두
        2개 : top/bottom, left,right
        3개 : top, left/right, bottom
        4개 : 시게 방향 순서로 적용 top, right, bottom, left
    한 방향에만 Margin이나 Padding을 설정해주고 싶은경우에는 margin-방향 padding-방향이라고 설정하면 된다.

## this
<hr/>

자바스크립트의 함수는 호출될 때, 매개변수로 전달되는 인자값 이외에 arguments 객체와 this를 암묵적으로 전달받는다.

Java의 this는 인스턴스 자신(self)를 가리키는 참조변수다.
<br/>
하지만 자바스크립트의 경우 Java와 같이 this에 바인딩되는 객체는 한 가지가 아니라 
해당 함수 호출방식에 따라 this에 바인딩되는 객체가 달라진다.

### 함수 호출 방식과 this 바인딩

자바 스크립트의 경우 함수 호출방식에 의해 this에 바인딩할 어떤 객체가 동적으로 결정된다.
    함수의 상위 스코프를 결정하는 방식인 렉시컬 스코프(Lexical scop)는 함수를 선언할 때 결정된다.

함수를 호출하는 방식은 아래와 같이 다양하다.

    1. 함수 호출
    2. 메소드 호출
    3. 생성자 함수 호출
    4. apply/call/bind 호출

1. 함수 호출
전역객체는 모든 객체의 유일한 최상위 객체를 의미하며 일반적으로 Browser-side에서는 window, Server-side에서는 global 객체를 의미한다.

        //in brower console
        this === window // true

        // in Terminal
        node
        this === global // true
전역객체는 전역 스코프를 갖는 전역변수를 프로퍼티로 소유한다. 글로벌 영역에 선언한 함수는 전역객체의 프로퍼티로 접근할 수 있는 전역 변수의 메소드이다.
        var ga = 'Global variable';

        console.log(ga);
        console.log(window.ga);

        function foo(){
            console.log('invoked!');
        }
        window.foo();

기본적으로 this는 전역객체에 바인딩된다. 전역함수는 물론이고 심지어 내부함수의 경우도 this는 외부함수가 아닌 전역객체에 바인딩된다.

    function foo(){
        console.log("foo's this :, this); // window
        function bar(){
            console.log("bar's this:", this) // window
        }
        bar();
    }
    foo();

또한 메소드의 내부함수일 경우에도 this는 전역객체에 바인딩된다.

    var value = 1;
    var obj = {
    value: 100,
    foo: function() {
        console.log("foo's this: ",  this);  // obj
        console.log("foo's this.value: ",  this.value); // 100
        function bar() {
        console.log("bar's this: ",  this); // window
        console.log("bar's this.value: ", this.value); // 1
        }
        bar();
    }
    };
    obj.foo();

콜백함수의 경우에도 this는 전역객체에 바인딩된다.

    var value = 1;
    var obj = {
    value: 100,
    foo: function() {
        setTimeout(function() {
        console.log("callback's this: ",  this);  // window
        console.log("callback's this.value: ",  this.value); // 1
        }, 100);
    }
    };
    obj.foo();

내부함수는 일반 함수, 메소드, 콜백함수 어디에서 선언되었든 관계없이 this는 전역객체를 바인딩한다.
내부함수의 this가 전역객체를 참조하는 것을 회피하려면 다음과 같이 해야한다.

    var value = 1;
    var obj={
        value:100,
        foo: function(){
            var that = this; // workaroud : this===obj
            console.log("foo's this:", this); // obj
            console.log("foo's this.value:", this.value); // 100
            function bar(){
                console.log("bar's this:",this); // window
                console.log("bar's this.value:", this.value); // 1

                console.log("bar's that:", that); //obj
                console.log("bar's that:",that.value); //100
            }
            bar();
        }
    };
    obj.foo();
2. 메소드 호출
함수가 객체의 프로퍼티 값이면 메소드로서 호출된다. 이때 메소드 내부의 this는 해당 메소드를 호출한 객체에 바인딩된다.

        var obj1 = {
            name: 'Lee',
            sayName: function() {
            console.log(this.name);
            }
        }
        var obj2 = {
            name: 'Kim'
        }
        obj2.sayName = obj1.sayName;
        obj1.sayName(); // Lee
        obj2.sayName(); // Kim

3. 생성자 함수 호출

기존 함수에 new 연산자를 붙여서 호출하면 해당 함수는 생성자 함수로 동작한다.

        // 생성자 함수
        function Person(name) {
        this.name = name;
        }

        var me = new Person('Lee');
        console.log(me); // {name: "Lee"}

        // new 연산자와 함께 생성자 함수를 호출하지 않으면 생성자 함수로 동작하지 않는다.
        var you = Person('Kim');
        console.log(you); // undefined

    3-1. 생성자 함수 동작 방식

    new 연산자와 함께 생성자를 호출하면 다음과 같은 수순으로 동작한다.
        1. 빈 객체 생성 및 this 바인딩
        생성자 함수의 코드가 실행되기 전 빈 객체가 생성된다. 
        이후 생성자 함수 내에서 사용되는 this는 이 빈 객체를 가리킨다. 
    
        2. this를 통한 프로퍼티 생성
        생성된 빈 객체에 this를 사용하여 동적으로 프로퍼티나 메소드를 생성할 수 있다. 
        this는 새로 생성된 객체를 가리키므로 this를 통해 생성한 프로퍼티와 메소드는 새로 생성된 객체에 추가된다.

        3. 생성된 객체 반환
        - 반환문이 없는 경우, this에 바인딩된 새로 생성한 객체가 반환된다.
        - 반환문이 this가 아닌 다른 객체를 명시적으로 반환하는 경우, this가 아닌 해당 객체가 반환된다.
    
    3-2. 생성자 함수에 new 연산자를 붙이지 않고 호출할 경우
    
    일반함수와 생성자 함수에 특별한 형식적 차이는 없으며 함수에 new 연산자를 붙여서 호출하면 해당 함수는 생성자 함수로 동작한다.
    그러나 생성자 함수를 new없이 호출하거나 일반함수에 new를 붙여 호출하면 오류가 발생할 수 있다.

    (일반 함수와 생성자 함수의 호출시 this 바인딩 방식이 다르기 때문.)

4. apply/call 호출

this에 바인딩될 객체는 함수 호출 패턴에 의해 결정된다. 이는 자바스크립트 엔진이 수행하는 것이다.

    func.apply(thisArg,[argsArray])
    // thisArg : 함수 내부의 this에 바인딩할 객체
    // argsArray : 함수에 전달할 argument의 배열

기억해야 할 것은 apply() 메소드를 호출하는 주체는 함수이며 apply() 메소드는 this를 특정 객체에 바인딩 할 뿐. 본질적인 기능은 함수 호출이다.

apply()메소드의 대표적인 용도는 arguments객체와 같은 유사 배열 객체에 배열 메소드를 사용하는 것이다.
argument객체는 배열이 아니기 때문에 slice()같은 배열의 메소드를 사용할 수 없지만 apply()메소드를 이용하면 가능하다.

    function converArgsToArray(){
        console.log(arguments);

        // arguments 객체를 배열로 변환
        // slice : 배열의 특정 부분에 대한 복사본 생성
        var arr = Array.prototype.slice.apply(arguments);
        console.log(arr);
        return arr;
    }
    convertArgsToArray(1,2,3);

call() 메소드의 경우, apply()와 기능은 같지만 apply()의 두번째 인자에서 배열 형태로 넘긴 것을 각각 하나의 인자로 넘긴다.

    Person.apply(foo,[1,2,3]);
    Person.call(foo,1,2,3);

## 브라우저 저장소 차이점
<hr/>

### Cookie
1. 매번 서버로 전송된다.
2. 개수와 용량 제한이 있다. 하나의 사이트에 최대 쿠키 수는 20개, 최대 쿠키 크기는 4KB
3. 만료일자를 지정하게 되어 있어 언젠가 제거된다.

### WebStorage
Web Storage는 쿠키와 마찬가지로 사이트의 도메인 단위로 접근이 제한된다.
1. 저장된 데이터가 클라이언트에 존재할 뿐 서버로 전송되지 않는다.
2. 문자열 기반 데이터 이외에 체계적으로 구조화된 객체 저장할 수 있다.
3. 용량의 제한이 없다.
4. 영구 데이터 저장이 가능하다.(LocalStorage)

ex) A 도메인에 저장된 데이터는 B 도메인에서 조회 불가

#### LocalStorage
저장한 데이터를 명시적으로 지우지 않는 이상 영구적으로 보관이 가능하다. 

Windows 전역 객체의 LocalStorage라는 컬렉션을 통해 저장과 조회가 이루어진다.

#### SessionStorage
데이터의 지속성과 액세스 범위에 특수한 제한이 존재한다.
브라우저가 종료되면 데이터도 같이 지워진다.

Windows 전역 객체의 SessionStorage라는 컬렉션을 통해 저장과 조회가 이루어진다.

## HTTP 메소드 정리

### GET
요청받은 URL의 정보를 검색하여 응답한다.
도메인에 queryString이 붙는다.

### HEAD
GET방식과 동일하지만, 응답에 BODY가 없고 응답코드와 HEAD만 응답한다.
웹서버 정보확인, 헬스체크, 버전확인, 최종 수정일자 확인 용도로 사용

### POST
요청한 자원은 생성(CREATE)한다.
새로작성된 리소스인 경우 HTTP헤더 항목 Location:URL주소를 포함하여 응답.

### PUT
요청된 자원을 수정(UPDATE)한다. 
내용 갱신을 위주로 Location:URL를 보내지 않아도 된다.
클라이언트 측은 요청된 URL를 그대로 사용하는 것으로 간주함.

### PATCH
PUT과 유사하게 요쳥된 자원을 수정(UPDATE)할 때 사용한다.
PUT은 자원 전체를 갱신하지만, PATCH는 해당자원의 일부를 교체할 때 사용.

### DELETE
요청된 자원을 삭제할 때 사용.

### CONNECT
동적으로 터널 모드를 교환, 프록시 기능 요청시 사용

### TRACE 
원격지 서버에 루프백 메시지를 호출하기위해 테스트용으로 사용

### OPTIONS
웹서버에서 지원되는 메소드의 종류를 확인할 경우 사용

## 자바스크립트에서 멀티 스레드
<hr/>

자바스크립트는 기본적으로 싱글 스레드이다.
여기서 싱글 스레드는 한 번에 하나의 작업만 할 수 있다는 뜻이다.
하지만 Web worker를 사용하면 멀티 스레드 구동이 가능하다.

웹 워커 사용코드

    function startWorker(){
        if(window.Worker){
            w = new Worker("example_worker.js");
            w.onmessage = function(event){
                alert(event.data);
            }
        }else{
            alert("Web worker를 지원하지 않는 브라우저입니다.");
        }
    }

웹 워커 종료코드

    function stopWorker(){
        w.terminate();
        w= undefined;
    }

## 자바스크립트 이벤트 루프
<hr/>

자바스크립트는 싱글 스레드 언어이기 때문에 함수를 실행하면 함수 호출이 스택에 순차적으로 쌓이고
스택의 맨 위에서 부터 차례대로 하나씩 처리가 된다.
아주 복잡한 프로그램을 구동한다고 새각하면 시간이 매우 오래걸리는 작업이 스택이 쌓이고 실행되면 그 다음작업은 무한정 대기할 수 밖에 없다.
이러한 점을 극복하기 위한 해결방안이 Asynchronous Callbacks(비동기 콜백)이다.

함수를 동기 호출하게 되면 call stack에 쌓여 순차적으로 실행된다.
이 때 setTimeout 혹은 DOM event 함수를 실행하면 자바스크립트 엔진은 call stack에서 WEB APIs로 보내고
정해진 시간 혹은 이벤트가 발생한 순간에 순차적으로 callback queue에 적재한다.

callback queue에 줄을 선 함수등른 call stack에 쌓여있던 것들이 모두 제거되면 차례대로 스택에 쌓여 실행되게 된다.

        console.log(1);
        
        setTimeout(function cb(){
            console.log(2);
        },5000);

        console.log(3);

위와 같이 실행하면 스택에 

main() -> console.log(1) -> 콘솔에 1 찍힘 -> cb함수 -> web APIs에 setTimeout(5000) -> 

console.log(3) -> 콘솔에 3 찍힘 -> task queue에 cb함수 -> console.log(2)
-> 콘솔에 2찍힘 순으로 나온다

## 이벤트 버블링
이벤트 버블링은 특정 화면요소에서 이벤트가 발생했을 때 해당 이벤트가 상위 화면 요소들로 전달되어가는 특성이다.

    상위 화면요소란 ? HTML요소는 기본적으로 트리구조이다. 여기서 트리 구조상 한 단계 위의 요소를 상위요소라 하며
    body태그를 최상위 요소라 한다.

    <body>
        <div class="one">
            <div class="two">
                <div class="three">
                </div>
            </div>
        </div>
    </body>
-----------

    var divs = document.querySelectorAll('div');
    divs.forEach(function(div) {
        div.addEventListener('click', logEvent);
    });

    function logEvent(event) {
        console.log(event.currentTarget.className);
    }
위 코드에서 <div class="three"></div>를 클릭하면 three -> two -> one 순으로 실행된다.
위와 같이 하위에서 상위요소로 이벤트 전파 방식을 이벤트 버블링이라 한다.

## 이벤트 캡쳐
이벤트 캡쳐는 이벤트 버블링과 반대로 진행되는 전파 방식이다.

    <body>
        <div class="one">
            <div class="two">
                <div class="three">
                </div>
            </div>
        </div>
    </body>
-----------

    var divs = document.querySelectorAll('div');
    divs.forEach(function(div) {
	div.addEventListener('click', logEvent, {
		capture: true // default 값은 false입니다.
	});
    });

    function logEvent(event) {
        console.log(event.currentTarget.className);
    }

addEventListnere() API에서 옵션 객체에 capture:true를 설정해주면 해당 이벤트를 감지하기 위해 이벤트 버블링과 반대 방향으로 탐색한다.
따라서 아까와 동일하게 <div class="three"></div>를 클릭하면 one -> two -> three 순으로 실행된다.

## HTML 렌더링 중 Javascript 실행
<hr/>

일반적으로 HTML을 파싱하고 외부 자원인 CSS, JS를 로드하게 된다.
JS는 script 태그를 만나면 해석 및 실행되는 동안 문서의 파싱은 중단되게 된다.
스크립트가 외부에 있을 경우 네트워크로부터 자원을 가져와야 하는데 이 또한 실시간으로 처리되고 자원을 받을 때까지 파싱은 중단된다.

이러한 문제를 야기시키지 않고 UX를 떨어뜨리지 않게 스크립트 소스를 body 태그 끝에 두는 것을 권장한다.

문서의 <head> 영역에 스크립트가 삽입되거나 외부 파일에 정의 되있을 경우 async나 defer를 사용하면 된다.
async 속성은 HTML렌더링을 멈추지 않고 동시에 js파일을 다운로드하고 다운로드가 끝난 후 자바스크립트를 실행한다.
defer 속성은 HTML렌더링을 멈추지 않고 동시에 js 파일을 다운로드하고 HTML렌더링이 끝난 후 자바스크립트를 실행한다.

## 서버사이드렌더링과 SPA 차이
<hr/>

렌더링이란 웹 페이지 접속 시 그 페이지를 화면에 그려주는 것.

SSR : Server Side Rendering
요청시마다 새로고침이 일어나며 서버에 새로운 페이지에 대한 요청을 하는 방식이다.

CSR : Client Side Rendering

SPA : Single Page Application

모바일 시대가 도래하며 일반적인 컴퓨터에 비해 성능이 낮은 모바일에 최적화시키기위해 SPA개념이 생겨났다.

SPA는 최초 한번 페이지 전체를 로딩 후 데이터만 변경하여 사용할 수 있는 웹 어플리케이션이다.
서버는 단지 JSON파일만 보내주는 역할을 하며 html을 그리는 역할은 클라이언트 측 자바스크립트가 수행한다.
그리고 이것이 클라이언트 사이드 렌더링이다.

SSR(서버사이드 렌더링)의 경우 초기 로딩속도가 빠르고 SEO(검색 엔진 최적화)에 유리하지만 View 변경시 서버에 계속 요청해야 하므로 서버 부담이 크다.
CSR(클라이언트사이드 렌더링)의 경우 초기 로딩속도는 느리지만 초기 로딩 후 서버에 다시 요청 할 필요가 없이 클라이언트 내에서 작업이 이루어지므로 매우 빠르다.

## Require와 Import의 차이점
<hr/>

file.js를 불러온다 가정 할 때 import는 특정 값만 따로 가져올 수 있고 나머지 값들은 웹팩의 tree shaking으로 빌드에서 제거된다.
즉, 불필요한 파일을 제거함으로 코드량을 줄이고 성능을 좋게 할 수 있다.

    //file.js
    export{
        a:'a',
        b:'b',
        c:'c'
    };
    //main
    import {a} from './file.js';

require는 동적으로 모듈을 불러올 수 있지만, 불필요한 코드들가지 불러온다.
babel-loader에서 웹팩의 tree shaking기능을 유지하기 위해 설정시 modules:false로 설정하면 된다.

import는 ES6 문법이라 현재 사용되는 브라우저에서 지원하지 않지만 babel과 같은 트랜스파일러가 해결해줄 수 있다.
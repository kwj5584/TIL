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
    4. apple/call/bind 호출

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
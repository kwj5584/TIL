# ES6 문법

## Arrow

    Arrow 함수는 ⇒ 문법을 사용하는 축약형 함수. 

    Arrow함수 표현식의 결과는 표현식 본문뿐만 아니라 상태블럭 본문도 지원

## const,let

    ES5까지는 모든 변수명을 var로 사용했지만 ES6부터는 const와 let을 사용

    var는 function scope이고 const,let은 block scope이다.

    let은 변수에 재할당이 가능하지만 const는 변수 재선언, 재할당 모두 불가능하다.

## 템플릿 문자열

    문자열 안에 변수를 넣을 수 있다.

    ex) let myName = '김휘진';

    console.log(`내 이름은 ${myName}입니다.` );

## 비구조화 할당

    비구조화 할당은 객체와 배열로부터 프로퍼티를 쉽게 꺼낼 수 있다.

    ex)

    let obj = {

        name:'김휘진',

        age:26,

        bag:{

        item_1: '지갑',

        item_2: '휴대폰'

            },

        };

    const {name, bag:{item_1} } = obj;

## 함수 기본 매개변수값 지정

    ES6의 함수 매개변수에 기본값을 지정해줄 수 있다.

    ex) function test(height=10, wdith=20, color='gree'){

    ...

    }
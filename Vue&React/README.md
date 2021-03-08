# Vue&React

## Vue와 React의 차이점
<hr/>

### Data 변형

Vue는 데이터를 생성한 후 자유롭게 업데이트 할 수 있지만, React는 state객체를 만들고 업데이트하기 위해 setState를 사용하여 업데이트한다.

### 파일의 구조

React 컴포넌트는 style을 유지해주는 파일을 따로 .css로 생성하고 .js파일에서 javascript를 확장한 문법인 jsx를 통해 화면과 이벤트 처리를 담당한다.
반면 Vue는 .vue파일안에 template, script, style을 모두 작성하여 사용하는 방식이다.

### 데이터 바인딩

양방향 데이터 바인딩과 단방향 데이터 바인딩의 차이는 HTML에서 변경된 내용이 데이터 영향을 미치는가이다.

예를 들어 Vue.js는 엘리먼트에 데이터를 바인딩하면 Javascript코드로 데이터를 변경할 수도 있고 엘리먼트의 값(input)을 수정해서 데이터를 변경할 수 있다.

하지만 React와 같은 단방향 데이터 바인딩은 Javascript -> HTML로 데이터 바인딩만 가능하다.

언뜻 보기에는 단방향이 불편해보일 수 있지만 그만큼 단방향 데이터가 가지는 장점은 모든 Javascript 코드가 데이터에 집중되며 일관된 데이터 관리 로직을 갖는다는 점이다.

#### React

React는 단방향 데이터 흐름을 지향한다. 

    ...
    const [Name,setName] = useState("")

    const onSetName = (e) => {
        setName(e.currentTarget.value);
    }
    return(
        <div>
            <input onChange={onSetName} placeholder="Name" />
        </div>
    )

위 코드처럼 input태그에서 onChange이벤트를 전달받으면 input값을 읽어와 Name state를 갱신한다.

이때 값을 직접 수정하지 않고 새로운 state객체를 생성해서 교체하는 방식인데, 이는 react에서 강조하는 immutable한 객체를 사용하기 때문이다.

#### Vue 

vue 인스턴스 -> Template와 같이 한 방향으로 데이터 접근하는 것을 단방향 데이터 바인딩이라 한다.

양방향 데이터 바인딩은 vue 인스턴스 ⇄ Template 두 방향 모두 데이터에 접근할 수 있도록 하는 것이다.

양방향 데이터 바인딩을 가능하게 해주는 디렉티브가 v-model이다.

    HTML
    <template>
        <div>
            <input type="text" v-model="name">{{name}}</input>
        </div>
    </template>
    Javascript
    <script>
        data(){
            name:"test"
        }
    </script>
    
위 코드처럼 input태그의 v-model 디렉티브를 통해 Vue의 data를 직접 수정할 수 있다.

### Vue LifeCycle
<hr/>
Vue.js 라이프 사이클은 크게 Creation, Mounting, Updating, Destruction으로 나뉜다.

#### Creation
Creation단계에서 실행되는 훅들이 라이프사이클중 가장 처음 실행된다. 이 단계에서 beforeCreate훅과 Created훅이 있다.

-beforeCreate : 모든 훅 중 가장 먼저 실행되는 훅이다. data와 events가 세팅되지 않은 시점이다.

-created : data와 events가 호라성화되어 접근할 수 있지만 템플릿과 가상돔은 마운트 및 렌더링되지 않은 상태이다.

#### Mounting
Mounting단계는 초기 렌더링 직전에 컴포넌트에 직접 접근할 수 있다.

초기 랜더링 직전에 돔을 변경하고자 하다면 이 단계를 활용할 수 있다. 그러나 컴포넌트 초기에 세팅되어야 할 데이터는 created단계를 사용하는 편이 낫다.

-beforeMount : 템플릿과 렌더 함수들이 컴파일 된 후 첫 렌더링이 일어나기 직전에 실행된다.

-mounted : 컴포넌트, 템플릿, 렌더링된 돔에 접근할 수 있다.

mounted훅에서 유의할 점은, 부모와 자식 관계의 컴포넌트에서 우리가 생각한 순서로 mounted가 발생하지 않는다는 점이다.

#### Updating
컴포넌트에서 사용되는 반응형 속성들이 변경되거나 어떤 이유로 리렌더링될 때 실행된다.
디버깅이나 프로파일링등을 위해 컴포넌트 리렌더링시점을 알고 싶을때 사용한다.

-beforeUpdate : 컴포넌트 데이터가 변하여 업데이트 사이클이 시작될 때 실행된다. 정확히는 돔이 리렌더링되고 패치되기 직전에 실행된다.

-updated : 컴포넌트의 데이터가 변하여 리렌더링이 일어난 후에 실행된다. 여기서 상태를 변경하면 무한루프에 빠질 수 있다.

#### Destruction
-beforeDestroy : 뷰 인스턴스가 제거되기 직전에 호출된다. 이벤트 리스너를 제거하고자 할 때 사용된다.
-destroyed : 뷰 인스턴스가 제거된 후에 호출된다. 뷰 인스턴스의 모든 디렉티브가 바인딩 해제되고 이벤트 리스너가 제거되며 모든 하위 뷰 인스턴스도 삭제된다.


### React lifeCycle
<hr/>

#### Class Component

##### Mount
컴포넌트가 처음 실행 될 때를 Mount라고 표현한다.

마운드될 때 발생하는 생명주기들은 constructor, getDerivedStateFromProps, render, componentDidMount가 있다.

-constructor : 컴포넌트 생성자 메소드이다. 컴포넌트가 만들어지면 가장 먼저 실행되는 메소드이다.

-getDerivedStateFromProps : props로 받아온 것을 state에 넣어주고 싶을 때 사용한다. 이 메소드는 컴포넌트가 처음 렌더링 되기 전에도 호출되고, 리렌더링 되기전에도 매번 실행된다.

-render : 컴포넌트를 렌더링하는 메소드이다.

-componentDidMount : 컴포넌트의 첫번째 렌더링이 마치면 호출되는 메소드이다. 이 메소드가 호출되는 시점에 우리가 만든 컴포넌트가 화면에 나타난 상태이다.

여기선 주로 DOM을 사용해야하는 외부 라이브러리를 연동하거나, 해당 컴포넌트에 필요로 하는 데이터를 요청하기 위해

axios, fetch등을 통해 ajax요청을 하거나, DOM의 속성을 읽거나 직접 변경하는 작업을 진행한다.

##### Update
컴포넌트가 업데이트 되는 시점에 발생하는 생명주기들은 getDerivedStateFromProps, shouldComponentUpdate, render, getSnapshotBeforeUpdate, componentDidUpdate가 있다.

-getDerivedStateFromProps : 컴포넌트의 props나 state가 바뀌었을 때도 이 메소드가 호출된다.

-shouldComponentUpdate : 컴포넌트가 리렌더링 할지 말지 결정하는 메소드이다.

-render : 컴포넌트를 렌더링하는 메소드이다.

-getSnapshotBeforeUpdate : 컴포넌트에 변화가 일어나기 직전의 DOM상태를 가져와서 특정 값을 반환하면 그 다음 발생하게 되는 componentDidUpdate함수에서 받아와서 사용할 수 있다.

-componentDidUpdate : 리렌더링이 마치고, 화면에 우리가 원하는 변화가 모두 반영되고 난 뒤 호출되는 메소드이다.

##### Unmount
컴포넌트가 화면에서 사라질 때를 Unmount라 한다. 언마운트에 관련된 생명주기는 componentWillUnmount이다.

-componentWillUnmount : 주로 DOM에 직접 등록했었던 이벤트를 제거하고, setTimeout을 걸어놓은 것이 있다면 clearTimeout을 통해 제거를 한다.
추가적으로 외부 라이브러리를 사용한게 있고 해당 라이브러리에 dispose기능이 있다면 여기서 호출하면 된다.


#### Functional Component
<hr/>

기존에는 함수형 컴포넌트에서 생명주기사용과 state사용이 불가능하였지만 React 16.8에 새로 추가된 hook으로 사용할 수 있게 되었다.

        import React, {useEffect, useState} from 'react';
        
        function Example(){
            const [count,setCount] = useState(0);

            useEffect(()=>{
                document.title = `You clicked ${count} times`;
            });

            return(
                <div>
                    <p>You clicked {count} times</p>
                    <button onClick={()=>setCount(count+1)}>Click</button>
                </div>
            )
        }   
useEffect를 사용하면 componentDidMOunt와 componentDidUpdate의 효과를 볼 수 있다.

useEffect에 return값을 주면 재실행 될 때 return의 function을 실행하고 이를 cleanUp이라 한다.

cleanUp effect는 componentWillUnmount역할을 한다.

skipping effect는 componentDidUpdate의 역할을 한다.
useEffect의 두번째 인자에 빈 배열을 넣으면 componentDidMount역할만 수행하고, 배열에 값을 넣어주면 해당 값이 바뀔 때만 호출된다.
두번째 인자값에 아무것도 넣어주지 않으면 state값 업데이트 될 때마다 렌더링 된다.

    useEffect(()=>{
        document.title = `You clicked ${count} times`;
    },[count]);

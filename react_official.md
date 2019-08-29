```jsx
const name = 'JS'
const element = <h1>Hello, {name}</h1>


ReactDom.render(
    element,
    document.getElementById('root')
)
```

```jsx
function nameparameter(){
    const user = {
        name= "taehoon"
        f_name = "kim"
    }
    
    const elemenet = ({user.name} + {user.f_name})
    render(
        내 이름은 {element}
    )
}
```

```jsx
function Hello(user){
    return {user.username}

};

const user = {
    username : "태훈"
};

const element = (
    {Hello(user)}
);

```



### const, let, function ~이있으면 쓸 때 {~}로 쓰기


element는 React앱의 가장 작은 단위입니다.
엘리먼트는 화면에 표시할 내용을 기술합니다.

const element = H!!

브라우저DOM 엘리먼트와 달리 React 엘리먼트는 일반 객체이며, 쉽게 생성할 수 있습니다. React DOM은 React 엘리먼트와 일치하도록 DOM을 업데이트합니다.

컴포넌트랑 elment는 다름다


React 엘리먼트를 루트 DOM 노드에 렌더링하려면 둘 다 ReactDOM.render()로 전달하면 됩니다.
```javascript
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```


## 리액트가 비동기로 유명한 이유(?)
=> React DOM은 해당 엘리먼트와 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트한다.
따라서 `변경된 부분만 업데이트 한다`


```jsx
const element = <Welcome name="Sara" />;
```
이렇게 사용자 정의 컴포넌트가 있을 때, React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX어트리뷰트를 해당 컴포넌트에 단일 객체로 전달한다.
이 객체를 `props`라고 함


---

#### 초기 this.state를 지정하는 class constructor
```jsx
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```
근데 이건 props를 받으면서 state를 설정하고 싶을 때 쓰는 거같은데..?

---

`componentDidMount()` 메서드는 컴포넌트 출력물이 DOM에 렌더링 된 후에 실행됩니다. 이 장소가 타이머를 설정하기에 좋은 장소입니다.

componentDidMount()는 컴포넌트가 마운트된 직후, 즉 트리에 삽입된 직후에 호출됩니다. DOM 노드가 있어야 하는 초기화 작업은 이 메서드에서 이루어지면 됩니다. 외부에서 데이터를 불러와야 한다면, 네트워크 요청을 보내기 적절한 위치입니다.

이 메서드는 데이터 구독을 설정하기 좋은 위치입니다. 데이터 구독이 이루어졌다면, componentWillUnmount()에서 구독 해제 작업을 반드시 수행하기 바랍니다.

componentDidMount()에서 즉시 setState()를 호출하는 경우도 있습니다. 이로 인하여 추가적인 렌더링이 발생하지만, 브라우저가 화면을 갱신하기 전에 이루어질 것입니다. 이 경우 render()가 두 번 호출되지만, 사용자는 그 중간 과정을 볼 수 없을 것입니다. 이런 사용 방식은 성능 문제로 이어지기 쉬우므로 주의가 필요합니다. 대부분의 경우, 앞의 방식을 대신하여 constructor() 메서드에서 초기 state를 할당할 수 있습니다. 하지만 모달(Modal) 또는 툴팁과 같이 렌더링에 앞서 DOM 노드의 크기나 위치를 먼저 측정해야 하는 경우 이러한 방식이 필요할 수 있습니다.


---


<li>this.state를 지정할 수 있는 유일한 공간은 바로 constructor입니다.

<li>다른 곳에서는 `setState()`를 사용합니다.

---

컴포넌트는 자신의 state를 자식 컴포넌트에 props로 전달할 수 있습니다.
```jsx
<FormattedDate date={this.state.date} />
```

---
### 리액트에서 이벤트 처리하기
React의 이벤트는 소문자 대신 캐멀 케이스(camelCase)를 사용합니다.
ex) `onClick`


```html
<!-- HTML -->

<button onclick="activateLasers()">
  Activate Lasers
</button>
```

```jsx
// React

<button onClick={activateLasers}>
  Activate Lasers
</button>
```
---
#### click event 작성 할 때
```jsx
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Click me
      </button>
    );
  }
}
```
바인딩 할 필요는 없지만 성능면에서 별로..
하지만 일단 이렇게 쓰자!

---
#### 조건부 연산자
```jsx
condition ? true: false
```


---
## FORM 

`제어 컴포넌트 (controlled components)`<br>
폼을 렌더링하는 React 컴포넌트는 폼에 발생하는 사용자 입력값을 제어합니다. 이러한 방식으로 React에 의해 값이 제어되는 입력 폼 엘리먼트를 (state가 아닌) “제어 컴포넌트 (controlled component)“라고 합니다.

```html
<!--정리 -->
html에서의 폼 엘리먼트 :
 사용자의 입력을 기반으로 state를 관리 및 업데이트 

react에서는 setState()에 의해 관리해야하기 때문에
state가 아닌 제어 컴포넌트를 써야한다

```
```jsx
//form 쓰는 법!
import React from 'react';

class App extends React.Component {

    constructor(props) {
        super(props);
        this.state ={ value : ''};

        this.handleChange = this.handleChange.bind(this); //함수쓰려고 바인딩해줌
        this.handleSubmit = this.handleSubmit.bind(this); //이하동문
    
    }
    //아마 props안받을거면 그냥 밑에꺼 쓰면됩니당 
    // state={value : ''} 

    handleChange = (e) => {
        this.setState({value : e.target.value}); //이벤트가 일어났으니 그냥 e써주면된다 ㅎ 그리고 e.target.value가 이벤트가 일어난 곳의 밸류라고 생각하면됨!
    }

    handleSubmit = (e) => {
        alert('네가 쓴 내용은 !!! :' + this.state.value);
        e.preventDefault(); //이걸 써주면 submit후에도 초기화 방지!(렌더링 시키지 않고 유지한다ㅇ)
    }


    render(){
        return(
            <form onSubmit = {this.handleSubmit}>
                Name : 
                <input type="text" value = {this.state.value} onChange ={this.handleChange} />

                <input type="submit" value = "제출" />

            </form>
        )
        
    }


}
export default App;


```
---
description: class 컴포넌트에서는 사용할 수 없다.
---

# hooks

* 기존 리엑트 버전에서는 함수형 컴포넌트에서  state를 사용할 수 없기 때문에, state를 사용하려면 클래스 컴포넌트를 사용해야 했다. 그런데 React 16.8 버전부터는 함수형 컴포넌트에서도 state를 사용할 수 있도록 만들었다.\(함수형 컴포넌트는 this가 없기 때문에 클래스 컴포넌트와 다른 형태로 작성해야 한다.\)

### useState

```jsx
// useState 괄호안의 0은 초기값을 나타내주며,
// useState 는 두개의 값을 반환해주는데,
// 하나는 state 변수
// 하나는 해당 변수를 갱신할 수 있는 함수를 반환해준다.
// 아래와 같이, [count, setCount] 라 쓸 수 있는 것은
// 자바스크립트의 구조 분해 할당 때문이다.
const [count, setCount] = useState(0);
```

#### 참고\(자바스크립트 구조 분해 할당 es6\)

{% embed url="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring\_assignment" %}

### useReducer

```jsx
const initialState = {count: 0};

function reducer(state, action) {
    switch(action.type) {
        case 'increment':
            return {count: state.count + 1};
            
        case 'decrement':
            return {count: state.count - 1};
    }
}

function Counter() {
    const [state, dispatch] = useReducer(reducer, initialState);
    
    return (
        <>
            Count: {state.count}
            <button onClick={() => {dispatch(type: 'decrement')}}></button>
            <button onClick={() => {dispatch(type: 'increment')}}</button>
        </>
    );
}

```


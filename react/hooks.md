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

```jsx
// typescript에서 useReducer를 사용하는 방법
// 1. Action 함수를 정의한다.
// 2. state 의 타입을 정의한다.
// 3. reducer를 정의한다.(Action에 따른 state값을 어떻게 변화시켜줄지 정의한다.)
// 4. useReducer를 사용하여 해당 state와 초기값을 연결해준다.
// 5. 사용해본다.

import React, {useReducer} from 'react';

type Color = 'red' | 'orange' | 'yellow';

type State = {
    count: number;
    text: string;
    color: Color;
    isGood: boolean;
};

type Action = 
                { type: 'SET_COUNT', count: number}
            |   { type: 'SET_TEXT', text: string} ;

// reducer는 state와 action을 매개변수로 받아, 
// 두개를 연결해주는 함수를 만들어야 한다.
// reducer 함수는 return 값이 state와 동일한 State를 리턴값으로 줘야 한다.
function reducer(state: State, action: Action): State {
    switch (action.type) {
        case 'SET_COUNT';
                return {
                    ...sate,
                    count: action.count
                };
                
        case 'SET_TEXT':
                return {
                    ...state,
                    text: action.text
                };        
    }
}

function ReducerSample() {
    const [state, dispatch] = useReducer(reducer, {
        count: 0,
        text: 'hello',
        color: 'red',
        isGood: true
    });
    
    const setCount = () => dispatch({type: 'SET_COUNT': count: 5});
    const setText = () =>  dispatch({type: 'SET_TEXT', text: 'bye'});
    return (
        <div>
            <p>
                <code>count: </code> {state.count}
            </p>
            <p>
                <code>text: </code> {state.text}
            </p>
            <div>
                <button onClick={setCount}></button>
                <button onClick={setText}></button>
            </div>
        </div>
    );
}
```

### useRef

* 리엑트 컴포넌트에서 외부 라이브러리의 인스턴스 또는 DOM을 특정 값 안에 담을 때 사용한다. 추가적으로, 이를 통해 컴포넌트 내부에서 관리하고 있는 값을 관리할 때 유용하다. **단, 이 값은 렌더링과 관계가 없어야 한다.**

```jsx
const id = useRef<number>(0);

// useRef 는 ~.current 를 통해 값을 유추할 수 있다.
const increaseId = () => {
    id.current += 1;
};
```

### useEffect

* 화면이 렌더링이 된 후 실행된다.
* componentDidMount, componentDidUpdate와 다르게 레이아웃 배치와 그리기를 완료한 후에 발생한다.


---
description: class 컴포넌트에서는 사용할 수 없다.
---

# hooks

* 기존 리엑트 버전에서는 함수형 컴포넌트에서  state를 사용할 수 없기 때문에, state를 사용하려면 클래스 컴포넌트를 사용해야 했다. 그런데 React 16.8 버전부터는 함수형 컴포넌트에서도 state를 사용할 수 있도록 만들었다.(함수형 컴포넌트는 this가 없기 때문에 클래스 컴포넌트와 다른 형태로 작성해야 한다.)

### useState

```jsx
// useState 괄호안의 0은 초기값을 나타내주며,
// useState 는 두개의 값을 반환해주는데,
// 하나는 state 변수
// 하나는 해당 변수를 갱신할 수 있는 함수를 반환해준다.
// 아래와 같이, [count, setCount] 라 쓸 수 있는 것은
// 자바스크립트의 구조 분해 할당 때문이다.
const [count, setCount] = useState(0);

// 배열일 경우
const [inArray, setInArray] = useState([]);

setInArray([
    ...inArray,
    {
        id: inArray.length,
        value: Math.random()
    }
]);
```

#### 참고(자바스크립트 구조 분해 할당 es6)

{% embed url="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment" %}

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
* 특정, props가 변경될 때에만 필요하다면, 특정 props 조건을 걸 수 있다.

```jsx
useEffect(
    () => {
        const subscription = props.source.subscribe();
        return () => {
            subscription.unsubscribe();
        };
    },
    [props.source]
);
```

* render시에 한번만 실행되게 하려면?

```jsx
const dispatch = useDispatch();
const selectList = () => {
    dispatch(searchAll());
};

// useEffect에 [] 을 넣어주면,rendering시에 한번만 실행이 된다.
useEffect(() => {
    selectList();
}), [];
```

### useSelector

* 리덕스 스토어의 상태(state)에 접근할 수 있다.

```jsx
// 아래와 같이 스토어의 상태를 가지고 올 수 있다.
// state.login.userId 는 기존에 connect를 이용하여 리덕스에 접근한
// mapStateToProps와 비슷하다고 생각하면 된다.
const {userId} = useSelector(state => {
    state.login.userId
});
```

### useDispatch

* 컴포넌트 내에서 redux 의  dispatch에 접근할 수 있게 만들어 준다.

```jsx
import createUser from 'store/modules/login';
import { useDispatch } from 'react-redux';

// 정의해준 액션함수를 import 해와서 이렇게 직관적으로 접근할 수 있게 된다.
const dispatch = useDispatch();
const createUser = (userId, userPwd) => {
    dispatch(createUser(userId, userPwd))
};
```

### useHistory

* a페이지에서 b페이지로 이동하고 싶을 때 useHistory를 쓰면 된다.&#x20;

```jsx
const history = useHistory();

history.push({
    pathname: '/test/',
    state: {
        userId: userId
    }
});
```

### useCallback

* 함수를 캐싱(또는 메모이제이션)할 때 사용하는 훅입니다.
* state가 변경되는 경우 컴포넌트가 다시 실행되는데 불필요한 렌더링이 일어나는 경우가 많다. 그럴 때 useCallback 훅을 사용해서 리렌더링이 되지 않도록 막으면 불필요한 렌더링이 일어나지 않는다.
* 하단과 같이 작성시, 해당 컴포넌트가 재실행되도 useState나 useCallback 모두 과거의 값을 가져오므로 return 부분에서 달라지는게 없어서 리렌더링이 되지 않는다.

```jsx
const [visible, setVisible] = useState(false);

const onClickButton = useCallback(() => {
    setVisible(true);
});
```

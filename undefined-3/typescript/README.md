# Typescript

{% embed url="https://hyunseob.github.io/2016/10/17/typescript-class/" %}

### 기존 js로 되어있는 react 프로젝트에 typescript 붙이기

```
$ npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```

{% embed url="https://velog.io/@velopert/typescript-basics" %}

### redux에 typescript 적용

1. action 의 type을 정해준다.(이 type은 리덕스 액션에 들어가게 될 type값.)
2. action 생성 함수를 만들어준다.
3. 액션 객체들에 대한 type을 준비한다. (typescript 타입값.)
4. 상태의 타입과 상태의 초깃값을 선언한다.
5. reducer를 만들어 준다.(reducer는 액션에 따른 state 값을 어떻게 변화시켜줄지 정의한다.)

#### 액션 type 선언

```typescript
// type을 선언할 때 뒤에 as const를 붙여주면 액션 객체를 만들 때에, type이
// typescript의 string타입이 되지 않고 실제 정의해준 액션 값을 가리키게 된다.
const INCREASE = 'counter/INCREASE' as const;
```

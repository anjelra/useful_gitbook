---
description: 상태관리 라이브러리
---

# recoil

{% embed url="https://blog.woolta.com/categories/1/posts/209" %}

#### recoil을 사용하기 위해서는 react의 컴포넌트\(App\)을 RecoilRoot로 감싸줘야 한다.

### Atom

* 상태 단위\(redux는 state와 비슷\)
* 동일한 atom을 사용하는 경우에는 해당 구성 요소가 변경되면 모두 재 렌더링이 됨. 즉, redux를 쓰지 않아도 좀더 편리하게 상태를 관리할 수 있게 됨.

```javascript
const fontSizeState = atom({
    key: 'fontSizeState',     // key값(보통 선언한 변수명과 동일하게 셋팅)
    default: 14    // 초기값
});

// .js 파일을 하나 만들어서 export 해서 사용하면 좋을듯.
```

* useRecoilState: 기존 useState와 같이 변경되는 값과 해당 값을 변경하는 함수를 반환.
* useRecoilValue: 구독하는 값만 반환하는 함수. 값의 update 함수가 필요없는 경우 사용.
* useSetRecoilState: 구독하는 값을 변경하는 함수만 반환.
* useResetRecoilState: 값을 기본값으로 reset 시키는 함수.

### Selector

* atom의 상태에 의존하는 동적인 데이터를 생성.
* get 함수를 통해 atom정보를 하나 이상 가져올 수 있음.
* set 함수를 통해 한 개 이상의 atom 정보를 업데이트할 수 있음.

```javascript
export const inputState = atom({
    key: 'inputState',
    default: ''
});

export const countInputState = selector({
    key: 'countInputState',
    get: ( { get } ) => {
        return `현재 카운트는 ${get(countState)} 이고, 입력값은 ${get(inputState)} 입니다.`;
    },
    set: ( { set }, newValue ) => {    // 두번째 파라미터는 추가로 받을 인자를 나타냄.
        set(countState, Number(newValue));    // count atom 수정
        set(inputState, newValue + 1);        // input atom 수
    }
}); 
```

* selector를 이용해 비동기 통신을 할 수 있음. \(비동기 처리를 위한 Suspene 지원\) 
  * 따라서, 비동기 상태에 대한 처리를 하기 위해서는 React의 Suspense를 통해야 함.

```javascript
import {Suspense} from 'react';

<Suspense fallback={<div>loading...</div>}>    // suspense를 통한 비동기 처리.
    <RecoilStarCount/>
</Suspense>

// 비동기 처리 seletor
export const recoilStarCountState = selector({
    key: 'asyncState',
    get: async () => {
        const response = await fetch('https://api.github.com/repos/Recoil');
        const recoilProjectInfo = await response.json();
        
        return recoilProjectInfo['stargazers_count'];
    }
});


// RecoilStarCount.js 
function RecoilStarCount () {
    const recoilStarCount = useRecoilValue(recoilStarSelector);
    
    return (
        <>
            <p>recoild gitbub star 갯수</p>
            <p>{recoilStarCount}</p>
        </>
    );
}

export default RecoilStarCount;
```

* selector는 비동기 로직을 한번에  처리할 수 있지만, 주의해야 할 점은 read-only 한 RecoilValueReadOnly 객체로서 return 값만을 가질 수 있고 값을 set할 수 없는 특징을 가지고 있음.


---
description: 문제풀이 3일차(20.01.02 목요일)
---

# 3일차

![](<../.gitbook/assets/image (39).png>)

![](<../.gitbook/assets/image (32).png>)

```javascript
function solution(array, commands) {
    var answer = [];
    
   for (let i = 0; i < commands.length; i++) {
        const newArray = array.slice(commands[i][0] - 1, commands[i][1]); 
        newArray.sort((a, b) => {
            return a-b;
        });
        answer.push(newArray[commands[i][2] - 1]);
    }
    
    return answer;
}
```

새롭게 알게된 사실.. sort 메소는 기본적으로는 문자열로 정렬이 된다. 숫자로 정렬을 하고 싶다면 sort에 숫자로 정렬을 하겠다는 것을 알려줘야 한다. 한참을 헤맸네!!

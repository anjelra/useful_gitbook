---
description: codemirror를 이용해 만든 markdown 문서를 변환해 주는 라이브러리
---

# marked

### react와 marked 연동

* yarn add marked --save

### 이미 codemirror를 이용해서 markdown 형식으로 작성한 문서를 보이게 하는 법

```jsx
import marked from 'marked';

const [outputText, setOutputText] = useState('# 안녕하세요');

function getMarkdownText() {
    var rawMarkup = marked(outputText);
    return {__html: rawMarkup};
}

<div dangerouslySetInnerHTML={getMarkdownText()}></div>
```

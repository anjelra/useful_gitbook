# code mirror

### react와 code mirror 연동

* yarn add @uiw/react-codemirror --save

### code mirror 사용하기\(Markdown 형식을 이용\)

```jsx
import CodeMirror from '@uiw/react-codemirror';
import 'codemirror/keymap/sublime';
import 'codemirror/theme/monokai.css';
import React, {useState} from 'react';

const [outputText, setOutputText] = useState('#안녕하십니까');

// Codemirror edit mode
<CodeMirror
    value={outputText}
    onChange={text.bind(this)}
    options=({
        theme: 'neo',
        keyMap: 'sublime',
        mode: 'Markdown',
        lineNumbers: false    // codemirror사용시 라인 넘버 안나오게 설
    })
></CodeMirror>
```




# tasks

VSCode에서 실행 또는 빌드, 테스트를 하기 위해서는 package.json 에 scripts에 셋팅을 해줘서 직접 terminal에 입력해야 하는데, 이 과정을 편하게 해주는게 VSCode의 tasks임. npm뿐만 아니라 gulp 등도 실행시킬 수 있음.

#### tasks 파일 만드는 법.

1. F1을 누르면 command palette 창이 나옴.
2. tasks라고 입력한 후, Tasks: Configure Tasks를 고름.
3. tasks.json 을 한번도 안만들었다면,  Create tasks.json file from template 클릭.
4. Others 클릭.\(tasks.json 이 만들어짐\)

#### tasks 파일 예제

```javascript
{
    "version": "2.0.0",
    // package.json에 셋팅된 npm을 실행시킬 수 있음.
    // 아래와 같이 하게 되면 script 부분이 실행되는 것임. 즉, npm run build:tasks
    "tasks": [
        {
            "type": "npm",
            "script": "build:tasks",
            "group": "build",
            "label": "tasks 빌드",
            "detail": "필요한 설명 입력"
        }
    ]
}
```

#### tasks 실행방법

1. F1을 누름.
2. Run Task 하게 되면 tasks.json 파일에 선언해 둔 tasks를 사용할 수 있음.




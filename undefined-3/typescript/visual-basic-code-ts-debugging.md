# visual basic code로 ts debugging

### visual basic code로 ts debugging

1. launch.json 파일에 아래와 같이 셋팅.

```javascript
// 하단의 program에 debugging할 파일을 입력한다.
{
    "type": "node",
    "request": "launch",
    "name": "docs서버 시작",
    program: "${workspaceRoot}/app.ts", 
    "cwd": "${workspaceRoot}",
    "outFiles": [],
    "sourceMaps": true
}
```

   2. tsconfig.json 파일에 sourceMap: true 부분 주석을 해제.

   3. visual code 의 아래 버튼을 클릭.

![](../../.gitbook/assets/image%20%2858%29.png)

  4. 원하는 지점에 break-point 를 찍으면 이제 debugging도 가능.


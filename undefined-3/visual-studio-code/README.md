# visual studio code

### debugger를 위한 launch.json 셋팅

```javascript
{
    "type": "node",
    "request": "launch",
    "name": "common서버 시작",
    "skipFles": ["<node_internals>/**"],
    "program": "${workspaceFolder}/common/server/app.js"
}
```


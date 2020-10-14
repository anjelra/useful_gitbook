# tsconfig.prod.json

### 문제점

node를 typescript로 작업을 해서 build하는 과정에 tsconfig.json 파일에 셋팅을 했으나, CRA\(create-react-app\)을 사용해서 react를 build하는 순간 tsconfig.json 파일이 CRA에서 설정한 값으로 tsconfig.json 파일이 돌아가는 현상이 있음.

### 해결방안

tsconfig.prod.json 파일을 생성해서 해당 파일에 node build에 필요한 소스를 해당 파일에 입력하면 react가 빌드가 되더라도 연관성이 없어져서 node를 따로 돌릴 수 있음.

```javascript
$ tsc --build tsconfig.prod.json
```


# file

### node.js, multer를 이용한 file upload

1. client에서 html 태그 input type을 file로 셋팅해주고, html에서 보낼 때 formData를 이용한다.

```markup
<input type="file" name="file"/>

<script>
    const formData = new FormData();
    
    // 파일과 같이 보낼 데이터를 formData에 같이 셋팅해 준다.
    formData.append("file", fileNm);    // 선택한 파일 셋팅 
    formData.append("id", "anjelra");
</script>

```

&#x20;  2\. client에서 server api를 호출하기 위해서는 , headers의 Content-Type을 multipart/form-data로 셋팅해 줘야 한다.

```javascript
export const docSingleFileUpload = (formData: FormData): AppThunk => dispatch => {
    axios.post('localhost:8000/api/uploadSIngle', formData, {
        withCredentials: true,
        headers: {
            'Content-Type': 'multipart/form-data'
        }
    }).then(res => {
        // 서버 호출 다음에 처리할 액션을 넣어준다.
    });
};
```

&#x20; 3\. 서버 router에 셋팅(multer를 이용)

```javascript
import multer from 'multer';

const storage: any = multer.diskStorage({
    // client에서 보낸 파일을 uploadFiles의 폴더에 저장하겠다라는 뜻.
    // uploadFiles 폴더가 없을 수도 있기 때문에 서버시작할 때, 해당 폴더가 있는지 
    // 체크를 해서 없으면 생성하는 코드를 넣어주면 된다.(하단의 셋팅 참조)
    destination(req: Request, file: any, cb: any) {
        cb(null, 'uploadFiles/');
    },
    // 서버에 저장할 이름(중복을 제거하기 위해서 multer에서 고유의 이름을 생성하는데
    // 그 이름을 내가 원하는 형태로 저장할 수 있음.
    filename(req: Request, file: any, cb: any) {
        cb(null, file.fieldname + '-' + Date.now());
    }
});

const uploadWithOriginFileName = multer( {storage: storage });

// uploadWithOriginFileName.single 은 단일 파일을 업로드하겠다는 뜻이고,
// 'file'은 client의 input 의 name과 동일한 값으로 셋팅해 주면 된다.

// 우리가 일반적으로 하는 post와 다르게 하나의 파라미터가 더 있는데,
// uploadWithOriginFileName.single('file') 의 뜻은
// 해당 action을 수행하기 전에 파일을 먼저 읽는 다는 뜻이다.

// 위에서 설정한 값은 req.file로 접근할 수 있는데, req.body와 같이 사용하기 위해서는
// 위의 클라이언트에서 formData에 셋팅을 해 줄 때 file append 이후에 원하는 값을 
// 셋팅해주면 된다.
router.post('uploadSIngle', uploadWithOriginFileName.single('file'), 
    asyncRouterHandler(req: Request, res: Response) => {
    
        try {
             const file: any = req.file ? await DocFileModel.append({
                docID: req.body.docID,
                originFileName: req.file.originname,
                serverFileName: req.file.filename,
                filePath: req.file.path,
                createBy: req.body.id
            }) : undefined;
            
            if (req.file && file._id) {
                res.status(201)
                    .send({result: true, message: '파일 upload가 완료되었습니다.'});
            } else {
                // 실패했을 떄 client에 보내줄 응답값 셋팅
            }   
        } catch (e) {
            // 에러가 발생했을 때에 client에 보내줄 응답값 셋팅
        }
    });
```

#### upload할 폴더가 없으면 체크 후, 생성하기(서버 연결하는 부분에 작성)

```javascript
import app from 'Server';
import fs from 'fs';

const port = Number(process.env.PORT || 3000);
app.listen(port, () => {
    const dir = './uploadFiles';
    
    if (!fs.existsSync(dir)) {
        fs.mkdirSync(dir);
    }
    
    logger.info('Express server started');
});
```

{% embed url="https://www.npmjs.com/package/multer" %}

### 이미지 보여주(서버에 있는 이미지 불러오기)

```javascript
// server.ts
router.get('/imageView/:imageName', (req: Request, res: Response) => {
    try {
        const image = path.join(path.dirname(path.dirname(__dirname)), 'uploadFiles/images/', req.params.imageName);    
        
        fs.readFile(image, (err, data) => {
            res.writeHead(200, { "Content-Type": "image/" + req.params.imageName.split('.')[1]});
            res.write(data);
            res.end();
        });
    } catch (error) {
        res.status(500)
        .send({message: error.message});
    }
});
```

```jsx
// react.js
<div className="container">
    {imageList ? imageList.map(list, idx) => (
        <img key={idx}
             src={`/imageView/${list.serverFileName}`}
             alt=""
        />
    ): null}
</div>
```

### 파일 다운로드

* image와 같이 get방식으로 호출하면 되는줄 알았는데, 파일 경로를 찾지 못하였다. 이유는 아직 확인을 못했다 ㅠ

```javascript
// server.ts
router.post('/download', (req: Request, res: Response) => {
    try {
        const file = path.join(path.dirname(path.dirname(__dirname)), 'uploadFiles/files/', req.body.fileName);    
        
        if (fs.existsSync(file)) {
            const filename = path.basename(file);    // 파일명 추출
            const fileStream = fs.createReadStream(file);    // 파일을 읽을 수 있는 ReadStream을 생성.
            
            res.writeHead(200, {
                'Content-Type': 'application/octet-stream',
                'Content-Disposition': 'attachment; filename=' + filename
            });
            
            fileStream.pipe(res);
        } else {
            res.status(404)
            .send({message: '해당 파일이 없습니다.'});
            return;
        }
    } catch (error) {
        res.status(500)
        .send({message: error.message});
    }
});
```

```javascript
// react(middleware)
export const docDownloadFile = (serverFileName: string, originFileName: string): AppThunk => dispatch => {
    axios.post('/docs/api/docs/download', {
        fileName: serverFileName
    }, {
        withCredentials: true,
        responseType: 'bolb'    // 반드시, bolb type으로 받아야 한다.
    }).then(res => {
        if (res.data.message) {    // 실패 했다면
            // 실패 로
        } else {
            let bolb = new Bolb([res.data]);
            let downloadUrl = window.URL.createObjectURL(bolb);
            let filename = '';
            let disposition = res.headers["content-disposition"];
            
            if (disposition && disposition.includes("attachment")) {
                let fileNameRegax = /filename[^;=\n]*=((['"]).*?\2|[^;\n]*)/;
                let matches = fileNameRegax.exec(disposition);    // 서버에서 header에 보낸 content-disposition을 찾는다.
                
                if (matches ! = null && matches[1]) {
                    // fileName = matches[1].replace(/['"]/g, "");    -> 서버 파일명과 동일한 경우에는 이런식으로 하면 된다.
                    fileName = originFileName;
                }
                
                let a = document.createElement('a');
                if (typeof a.download === "undefined") {
                    window.location.href = downloadUrl;
                } else {
                    a.href = downloadUrl;
                    a.download = fileName;    // download속성에 원하는 제목을 넣으면 해당 제목으로 문서가 떨어진다.
                    document.body.appendChild(a);
                    a.click();
                    
                    document.body.removeChild(a);    // 생성후 지워준다.
                }
            }
        }
    });
};
```

```jsx
// react component
<div className="file-container">
    {fileList ? fileList.map(idx, list) => (
        <a href={}
           onClick={(e) => downloadFile(e, list.serverFileName, list.originFileName)}
        >
            {list.originFileName}
        </a>
    ) : null}
</div>
```


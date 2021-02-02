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

   2. client에서 server api를 호출하기 위해서는 , headers의 Content-Type을 multipart/form-data로 셋팅해 줘야 한다.

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

  3. 서버 router에 셋팅\(multer를 이용\)

```javascript
import multer from 'multer';

const storage: any = multer.diskStorage({
    // client에서 보낸 파일을 uploadFiles의 폴더에 저장하겠다라는 뜻.
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



{% embed url="https://www.npmjs.com/package/multer" %}




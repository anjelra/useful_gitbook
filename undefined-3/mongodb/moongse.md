# moongse

### mongodb 에 스키마를 적용하고 싶다면? 정답은 moongse

{% embed url="https://www.zerocho.com/category/MongoDB/post/59a1870210b942001853e250" %}

{% embed url="https://www.zerocho.com/category/MongoDB/post/5963b908cebb5e001834680e" %}

### mongoose를 사용하려면

1. mongoose install.
2. mongoose connect.
3. mongoose schema 정의. \(ex: var schema = mongoose.Schema; var blogSchema = new Schema\({author: ObjectId, title:  String, body: String, date: Date}\);
4. 정의한 schema 를 사용할 수 있도록, model를 만들어 준다.\(ex: var blog = mongoose.model\('blog', blogSchema\);
5. 모델을 사용하려면, 모델의 인스턴스를 만들어 주어야 한다. 생성한 인스턴스를 이용하여 우리가 원하는 실제 데이터베이스 작업을 수행할 수 있다. \(ex: var instance = new blog\(\); instance.title = 'hello';\)

### Schema

* 스키마에 모델을 생성하려면, \(var blog = mongoose.model\('blog', blogSchema, 'blog'\);
* 생성한 스키마를 확인해보려면 require\('mongoose'\).model\('생성한 모델명'\)을 입력하면 내가 생성한 스키마에 따른 모델이 잘 생성되었는지 확인할 수 있다.

### Model data 

* find\(조건에 맞는 모든 항목을 리턴\) : await User.find\({id: userid, password: password}\)
  * 결과값을 보면 \_doc에 데이터가 전부 들어 있어 접근할 수 있지만, 각각의 결과\(배열\)에 보면, get, set이 있어서 그냥 list\[0\].name 처럼 뽑아 쓸 수 있다.

### Mongoose save

* mongoose save 메소드를 사용하게 되면, _v 라는 필드가 나타날 것이다. 이것은 \_id처럼 mongoose에서 버전 관련 속성을 자동으로 입력하는 것인데, 해당 필드 이름을 변경할 수 있다. ex\) new Schema\({..}, {versionKey: "\_versionKey'}\);_

### Mongoose 사용자 정의 schema

* 사용자 정의 schema를 만들 경우에는, schema에 선언한 필드를 사용하지 않으려면 반드시 명시를 해 주어야 한다.\(ex: userSchema.statics.create = function\(userId, name, password\) {const newUser = new this\({id: userId, name, password}\);  return newUser.save\(\)}

### Mongoose populate\(sql의 join과 비슷한 기능을 구현\)

#### sql join과 다른점

* join은 db 자체에서 데이터를 합쳐주는 것이나, populate는 일단 전부다 조회를 한 다음에 자바스크립트 단에서 합쳐주는 것이기 때문에 성능이 좋지 않다.\(populate를 여러번 중첩해서 사용하게 되면 성능에 대한 issue가 생길 수 있다.\)

#### 사용법

* docSchema의 \_id와 docPersonalSchema 의 docID를 연결해주기 위해서는 docID에 type을 아래와 같이 정의해주고, ref: '바라볼 collection이름' 을 입력해 준다. 이렇게 되면 mongoose에서 두 개의 스키마에 연관성을 부여해 준다.

```javascript
// 스키마 생
const docSchema = new mongoose.Schema({
    path: {type: String, required: true},
    title: {type: String, required: true}
});

const docPersonalSchema = new mongoose.Schema({
    docID: {type: mongoose.Schema.Types.ObjectId, ref: 'doc', required: true},
    owner: {type: String, required: true}
});

mongoose.model('doc', docSchema, 'doc');
mongoose.model('personalDoc', docPersonalSchema, 'personalDoc');
```

#### 데이터 조회

* 사용자 문서의 특정 사용자와 문서 id에 따라서 doc와 personalDoc 스키마의 데이터를 join 형식으로 합쳐서 가지고 오고 싶다면 아래와 같이 쿼리를 생성하면 된다.

```javascript
const readDoc = await PersonalDoc.find({owner: 'anjelra', docID: '123adfsfgqwer'})
                                .populate('doc').exec();
```

### 특정 필만 조회

```javascript
const group = await PersonalDoc.find({owner: 'anjelra', docID: '123'})
                .select('path _id').sort({path: 1}).exec();
```




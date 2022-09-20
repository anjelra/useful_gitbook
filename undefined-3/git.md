---
description: terminal 창으로 연습해보기
---

# git

### git 저장소 만들기 &#x20;

1. git hub에 create new repository 를 클릭해서 원하는 이름으로 만듦&#x20;
2. git init
3. git status(상태 확인)&#x20;
4. git add README.md
5. remote 할 주소 체크
6. git commit -m'init'
7. git remote add origin(alias) https://github.com/anjelra/lunchtoday.git(주소)
8. git push -u origin(alias) master

{% embed url="https://zeddios.tistory.com/4" %}



#### 터미널을 이용한 cherry-pick (특정 커밋만 해당 브랜치에 넣고 싶을 때 사용)&#x20;

* git checkout master -> master로 현 git 상태를 변경함.
* git pull origin master -> origin master에 있는 push 된 모든것을 pull.
* git status -> 현재 git상태는 어디에 있는지 확인함.
* git cherry-pick 710c9ae1 -> 현재 git이 마스터에 있다면 master에 '710c9ae1' 을 커밋함.(현재 push는 안된상태. 커밋까지 이루어져 있는 상태임.)
* &#x20;git push (이걸 하게되면 cherry-pick 한 것을 이전 커밋 메세지와 동일하게 master에 푸쉬함.)



#### 터미널을 이용한 stash를 저장하는 법&#x20;

* git status(깃 상태 확인하면 현재 작업중인 파일 목록이 나옴)

![](<../.gitbook/assets/image (12).png>)

* git add . (전체 파일을 add 함) -> add를 무조건 해야 stash를 할 수 있음.
* git status ( 깃 상태 다시 확인) -> 파일이 add 된 걸 알 수 있음.

![](<../.gitbook/assets/image (10).png>)

* git stash save '원하는 stash 이름' -> 이제 stash 가 되었음. (ex: ㅋㅋㅋ)



#### 터미널을 이용한 stash를 꺼내오는 법

* git stash list -> stash 한 list를 볼 수 있음.(저장할 때 이름을 잘 저장해놓으면 좋겟죠??)

![요기 이렇게 내가 저장한 게 있네??](<../.gitbook/assets/image (1).png>)

* q 를 누르면 빠져나올 수 있음. stash list에서!!
* git stash apply stash@{0} -> 꺼내오고 싶은 stash 를 꺼내온다!! ex: stash@{0}



#### 터미널을 이용한 commit 방법

* git status -> 상태 확인
* git add . -> 파일을 commit 할 수 있도록 add 한다.(참고로 . 은 현재 있는 모든 것을 add 한다는 뜻)
* git commit -m'commit 메세지 작성' -> -m은 message의 약자이며,  commit 메세지 작성에는 원하는 커밋 메세지를 넣어줌.
* git pull origin master -> 여기에서 나오려면 :q 를 입력하면 됨.

#### 터미널을 이용한 revert 방법

* git revert <되돌릴 커밋> -> 이것은 reset 과 다른 시점이기 때문에 revert 는 내가 작업한 부분을 내 로컬에 떨어뜨리는 것. 주의해야 할 점임.
* 만약 에러가 난다면, ::q 로 나오면 됨.&#x20;

#### 터미널을 이용한 reset 방법

* git reset <되돌릴 커밋> -> reset 할 시점 이후에 있는 모든 커밋 자체를 없애기 위해 reset 를 사용.&#x20;

#### 터미널을 이용한 git remote branch 가져오기&#x20;

* git remote update -> git remote를 갱신해야함
* git branch -r -> -r 옵션으로 원격 저장소의 branch list를 볼 수 있음.
* git branch -a -> -a 옵션으로 로컬과 원격 저장소 모두의 branch list를 볼 수 있음.
* git checkout -t -> 원격저장소의 branch 가져오기(ex: git checkout -t origin/2020\_03\_24

#### &#x20;터미널을 이용한 git merge

* master로 머지하고 싶다면 git checkout master -> master 로 브랜치 이동
* git pull origin master -> master를 pull 받음.
* git status -> git 상태 확인
* git merge \<merge하고싶은 브랜치> -> ex) git merge 2020\_03\_24
* git commit -m'master merge' -> 이렇게 하면 merge가 됨. 현재는 내 local에만 있는 상태임.
* git push origin master -> remote 브랜치에 master 머지&#x20;

#### 유용한 터미널 명령어

* mkdir test -> test 폴더를 만듬
* touch test.html -> test.html 파일을 만듦
* rm test.html -> test.html 을 삭제&#x20;
* cd ../ -> 이전 디렉토리로 이동
* cd -> 다음 폴더로 이
* ls --al -> 현재 디렉토리 목록 보여줌&#x20;

#### git repository 삭제

{% embed url="https://coding-factory.tistory.com/246" %}

### push 가 안된다!!

{% embed url="https://blog.shovelman.dev/924" %}

#### 터미널로 remote branch checkout 받기

* git remote update ->  먼저 원격의 브랜치에 접근하기 위해 git remote를 갱신해줄 필요가 있음.
* git branch -r -> branch list 보기
* git checkout 2020\_04\_01 -> 이런 식으로 원하는 브랜치명을 checkout 받으면 됨.

### git add 명령 하기 전 파일 되돌리기(GUI의 discard local change와 같은 기능)

#### repository 내 모든 수정 되돌리기

* cd {repository\_root\_dir}
* git checkout .

#### 특정 폴더 아래의 모든 수정 되돌리기

* git checkout {dir}

#### 특정 파일의 수정 되돌리기

* git checkout {file\_name}

{% embed url="http://hochulshin.com/git-revert-changes/" %}

### git add 명령으로 stage에 올린 경우

* git reset

### git remote branch 생성하기

1. git checkout -b '원하는 브랜치명' -> 브랜치 local 에 생성
2. git push origin '생성한 브랜치명' -> origin 에 push(저장소 branch에 생성 완료)
3. git branch --set-upstream-to origin/'생성한 브랜치명' -> local 및 저장소 branch 연동

### git remote branch 삭제하기

1. git checkout master ->  삭제할 브랜치에서 벗어나 master브랜치로 이동해야 삭제 가능
2. git branch --delete '삭제할 브랜치명' -> local에서 삭제
3. git push origin :' 삭제할 브랜치명' -> remote branch 삭제(저장소 branch도 삭제 완료)

### git clone

* git clone 'repository address' -> clone을 뜨게 되면 git 형태도 가지고 올 수 있어서 바로 커밋이 가능하다. 주소를 알면 이렇게 하는게 조음.

### git ignore node\_module not working

* 이미 cache를 먹고 있어서 안되는 거라서 터미널에 아래와 같이 치면 된다.
* git rm -r --cached node\_modules
* git commit -m "removing node\_modules"

### git repository 변경(ex: url 변경)

1. Remotes의 origin 우클릭&#x20;
2. 변경할 remote url 입력
3. acoount쪽에 Add New Custom Server Acoount 클릭
4. 아이디와 비밀번호 입력

* git remote set-url origin 변경할 주소
  * 근데 이렇게 하면 권한이 없다고 오류가 나옴. 그래서 위의 방법으로 해결.

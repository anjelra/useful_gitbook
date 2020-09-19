# github pages 무료 호스팅 사용하기

{% embed url="https://brunch.co.kr/@go-rani/14" %}

{% embed url="https://velog.io/@gwak2837/GitHub-Pages-gh-pages%EB%A1%9C-%EB%AC%B4%EB%A3%8C-%EC%9B%B9-%ED%98%B8%EC%8A%A4%ED%8C%85%ED%95%98%EA%B8%B0" %}

### github에 html 올리기

1. github에 새로운 repository 를 만든다.
2. 원하는 위치를 깃에 연결해 주기 위해서 폴더를 하나 만든다.
3. terminal을 켜서 git init.
4. git add README.md
5. git commit -m'first commit'
6. git remote add origin '새로운 repository 주소'
7. git push -u origin master
8. yarn add gh-pages --dev -&gt; gh-pages 패키지 설치
9. package.json 에 "homepage": "https://\(내 깃허브 아이디\).github.io/\(만든 Repository 이름\)"
10. github에 만든 repository 에 들어가서 setting 클릭.
11. 하단에 보면 Github Pages -&gt; Source 부분을 작업한 branch\(현재는 master\)로 클릭해주고, root를 클릭한 후, save를 누른다.
12. 아까 homepage에 연결해 준 주소를 브라우저에 입력하면 아까 만든 index.html 파일이 나온다.\(ex: https://anjelra.github.io/portfolio/index.html\)


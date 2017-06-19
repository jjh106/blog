---
title: hexo로 블로그 시작하기
tags:
  - hexo
  - github
date: 2017-04-29 00:50:24
---

hexo + github pages로 블로그 만들기를 시작한다! (순서대로 따라하면 됨)

### # 준비하기

hexo로 블로그를 만들기 전에 준비해야 할 것은 github의 repository를 **2개** 만들어야 합니다. 

***why...?*** 

github.io는 실제로 포스트한 글이 보이는 블로그의 repo이고, 다른 하나는 블로그의 정보를 저장하는 용도입니다.

블로그의 정보를 저장해두는 repo를 생성하는 이유는 다른 pc에서도 포스팅할 수 있게 하기 위해서입니다.

자세한 것은 아래에서 설명하겠습니다.

![repository](/uploads/repo.jpg)

* Repository name은 **계정명.github.io**로 하나를 생성합니다. ( 예: jjh106.github.io )

  _(이 때 주의할 점은 README를 생성하지 않는다.)_   

  두 번째 Repository는 아무 이름으로 지어준다. (블로그의 정보 저장용)  

* 시작 전 아래 두 가지를 설치합니다.

  * [node.js](https://nodejs.org/en/)
  * [Git](https://git-scm.com/) 


---

### # hexo 설치하기

```
npm i hexo-cli -g
hexo init blog
cd blog
npm i
```

* 블로그를 관리할 blog 폴더를 생성해서 초기화 시켜준다.



###  # 로컬서버에서 확인하기

```
hexo server
```

> 명령어 입력 후 localhost:4000으로 접속해서 확인.

![로컬](/uploads/screen.png)

**이렇게 뜬다면 설치 성공!**

---

### # github과 연동하기

```
deploy:
  type: git
  repo: https://github.com/jjh106/jjh106.github.io
  branch: master
```

```
url: https://jjh106.github.io/
root: /
```

> 로컬의 블로그 디렉토리를 처음에 만들었던 **github.io** repository에 배포해줘야 한다.  그러기 위해선 _config.yml에서 약간의 설정을 해줘야 한다.



```
hexo generate
```

> url과 deploy부분을 설정해주었다면 정적파일을 생성한다.



```
npm install hexo-deployer-git --save
```

> 그리고 deploy를 하기 위해선 플러그인을 설치해줘야 한다.



```
hexo deploy
```

> 모든 준비가 다 되었다면 deploy를 하자!

---

### # 포스트 작성하기

```
hexo new post '포스트명'
```

> 명령어를 입력하면 /source/_posts/ 내에 .md파일이 생성된다.
>
> 해당 md파일을 에디터에서 작성 후



```
hexo generate --deploy
```

> generate와 deploy를 동시에 하자.



입력하면 **끝!**

---

### # 다른 pc에서 블로그 관리하기

처음에 만들었던 2개의 repository중 두 번째 repository를 활용해 보자.

blog 디렉토리로 이동 후 다음 명령어를 입력한다.

```
git init 

git add .

git commit -m "message"

git remote add origin repository주소

git push origin master
```

이렇게 하면 다른 pc에서 해당 repository를 pull 받아 관리할 수 있다.

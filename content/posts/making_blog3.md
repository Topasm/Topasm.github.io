---
title: "Hugo 와 github action 을 이용해 블로그 만들기 - 3완"
date: 2021-09-06T10:54:16+09:00
categories: [web]
tags: [blog, hugo, web]
draft: false
---

저번 글까지 따라왔다면 로컬에 블로그 화면을 띄울 수 있을 것이다. 이제 github pages 와 github actions 기능을 이용해 커밋과 동시에 빌드해 사이트를 배포하도록 해본다. 그리고 커스텀 도메인을 사용하도록 설정 해본다.

### repository 만들기
커스텀 도메인을 이용하지 않는 경우 저장소(repository) 이름이 사이트 주소를 결정한다.
`닉네임.github.io` 으로 하면 주소가 `닉네임.github.io` 가 되고 `아무이름` 으로 하면 `닉네임.github.io/아무이름` 이런 식으로 주소가 개설 된다.

### github action 사용하기
1. personal access token 발급받기
github 접속 > developer settings > personal access token > generate new token
라고 하면
![image|584x499](https://rats.topasm.me/uploads/default/original/1X/f696454a2e0259bdc52e727b23b5b8f79e4b90ab.png)
창이 뜬다. 
- [x] public_repo 에 체크   

Note에 토큰 이름(영어로) ex)Hugo_Token


2. Token 사용 설정
토큰을 사용할 repository -> setting -> seeret -> new secret-> 만든 토큰 이름(Note), 아까 저장한 토큰 값을 적어준다(랜덤한 문자 숫자로 되어 있음).

3. github actions 활성화
저장소로 가면 Actions 항목이 있다. 클릭한 다음 `Set up this workflow`를 클릭한 후 action을 작성하면 된다. 아래 사이트에 자세한 설명이 있다.
참고: [actions-hugo](https://github.com/peaceiris/actions-hugo)

```
# action 이름. 원하는대로 정하면 된다. 
name: deploy ghpage

# on: 뒤에오는 event가 발생하면 action이 실행된다. 아래는 master branch에 push 나 pull request가 발생하면 action이 실행되는 코드이다. 보통 그냥 두면 된다. 
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

# jobs은 실행될 action을 포함하고 있다.  
jobs:
  
  build:
    runs-on: ubuntu-20.04
    #steps는 명령어 들이다. 
    # uses는 이미 만들어진 action을 사용하는 것, run은 명령어를 실행하는 것이다. 
    steps: 
    
    #1. 가상머신으로 checkout
    - uses: actions/checkout@v2
    
    #2. theme를 submodule로 등록했는데 그것도 checkout
    - name: Checkout submodules
      shell: bash
      run: |
        auth_header="$(git config --local --get http.https://github.com/.extraheader)"
        git submodule sync --recursive
        git -c "http.extraheader=$auth_header" -c protocol.version=2 submodule update --init --force --recursive --depth=1
        # run 다음 내용들은 submodule을 최신으로 udapte한것을 가져오는 내용 + a이다.
    
    #4. Hugo 설치 
    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: 'latest'

        
    #5. build (public 폴더에 저장 된다.)
    - name: Build Hugo Site
      run: |
        hugo --minify
       # minify는 압축시키는 것을 의미한다. 
    
    #6.Deploy 배포: git token이 필요하다. gh-pages로 publish하는 것 잊지 말자 
    #public 폴더를 github page의 gh-pages 브챈치에 배포한다는 의미이다. 
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.아까 만든 토큰 이름 }}
        publish_branch: gh-pages
        publish_dir: ./public
```
내가 사용하는 workflows 스크립트이다. 빌드하고 배포만 하는거라 그냥 복붙해서 사용하는게 좋다.

### github에 사이트 파일 업로드
Vscode 에서 터미널 실행한 후
```
git init  //깃 실행
git remote add origin https~~~~  //자신의 저장소 주소추가
git push -u origin master  //깃에 업로드
```
이렇게 하면 깃헙에 업로드 되고 사이트가 생성될것이다.

포스트를 썻다면
그냥 VScode 소스제어 항목에서 +로 변경을 모두 커밋하고 push 를 하는게 편하다.


### 커스텀 도메인 오류 해결
사이트를 개설하고 난 후 repository의 settings > pages 로 가면 커스텀 도메인을 넣을 수 있다. 문제는 빌드할 때마다 이 커스텀 도메인이 풀리는 문제가 있다.

```

.

├── config.toml

├── content/

│   └── posts/

├── static/

└── themes/

    └── PaperMod/

```
여기서 static폴더 아래에 CNAME 파일을 생성하고 커스텀 도메인주소를 입력한 후 저장한후 커밋하면 커스텀 도메인이 안풀린다. (`http 없이 주소만` 입력하고 확장자없고, CNAME 은 대문자로 해야 한다.)


생각보다 가이드 쓰는게 어렵다. 다음에는 좀 더 잘써봐야지..
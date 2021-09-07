---
title: "Hugo 와 github action 을 이용해 블로그 만들기 - 1"
date: 2021-08-25T14:26:08+09:00
categories: [web]
tags: [blog, hugo, web]
draft: false
---


윈도우 환경에서 내가 블로그 개발을 한 방법을 소개 한다.

레포지토리를 1개만 생성하고 github actions 를 이용해 커밋만 하면 자동으로 웹페이지로 배포 되도록 만들었다. 그리고 go 로 짜여진 hugo 를 이용하였다. 이유는 업데이트가 빠르고 빌드속도가 빠르기 때문이다.


### 준비물

- 깃헙 계정 [GitHub](https://github.com/)
-  윈도우 터미널 설치 [Windows Terminal installation | Microsoft Docs](https://docs.microsoft.com/en-us/windows/terminal/get-started)
- 깃 설치 [Git - Downloads (git-scm.com)](https://git-scm.com/downloads)
-  vscode 설치 [Visual Studio Code - Code Editing. Redefined](https://code.visualstudio.com/)
-  go 언어 설치 [The Go Programming Language (golang.org)](https://golang.org/)

### choco 와 hugo 설치

choco 는 윈도우의 비공식 패키지 매니저이다. 명령어로 동작하는 스토어 같은것이다.
hugo는 사이트 생성기이다.
1. choco 설치( [Chocolatey Software | Installing Chocolatey](https://chocolatey.org/install))
윈도우 터미널을 관리자 권한으로 열고 아래코드를 복사 붙여넣기 한다.
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

2. hugo 설치( [Install Hugo | Hugo (gohugo.io)](https://gohugo.io/getting-started/installing))
```
choco install hugo -confirm
```

이제 사이트를 생성하기 위한 준비 작업이 끝났다. 

### 사이트 소스 생성
사이트 소스를 저장할 폴더를 생성한다.
나는 c:\hugo 이런식으로 만들었다. 코드가 들어갈 경로는 항상 한글을 피하는게 좋다.
```
hugo new site sitename
cd sitename
git init
```
사이트 생성할 폴더와 코드를 생성해 주는 코드이다. **sitename** 은 원하는 대로 바꿔도 된다.  cd sitename은 **sitename** 폴더로 들어가는 명령어이다. git 사용을 위해 init 해준다.

이제 테마를 받아야 한다.
테마리스트 [Complete List | Hugo Themes (gohugo.io)](https://themes.gohugo.io/)

여기서 다운로드 버튼을 누르면 깃헙으로 들어가지는데 
난 [GitHub - adityatelange/hugo-PaperMod: A fast, clean, responsive Hugo theme.](https://github.com/adityatelange/hugo-PaperMod)
이걸 이용했다.
```
git submodule add [git 주소] themes/[테마 이름]
git submodule update --init --recursive
```
하면 되는데 papermod의 경우는
```
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

이렇게 됬다면
c:\hugo\sitename
이런식으로 폴더가 생성되어있고 sitename 내부에는 여러 폴더가 생성되어 있을것이다. 이 안에서 VScode를 실행시킨다.

Vscode 에서 폴더 열기로 들어가 sitename 폴더로 들어가면 된다.
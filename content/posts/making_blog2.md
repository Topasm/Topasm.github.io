---
title: "Hugo 와 github action 을 이용해 블로그 만들기 - 2"
date: 2021-08-25T20:51:28+09:00
categories: [web]
tags: [blog, hugo, web]
draft: false
---



이어서 VS 코드를 켰다면 
```
.
├── config.toml
├── content/
│   └── posts/
├── static/
└── themes/
    └── PaperMod/
```

이러한 폴더구조로 되어있다.
### config 수정

이제 config.toml 을 수정해야 한다. Vscode 에서 config.toml파일을 클릭해 수정해보자.
내가 사용하는 papermod 의 예시는 아래와 같다.

```
baseURL = "https://examplesite.com/"
title = "ExampleSite"
paginate = 5
theme = "PaperMod"
enableRobotsTXT = true
buildDrafts = false
buildFuture = false
buildExpired = false
googleAnalytics = "UA-123-45"

[minify]
disableXML = true
minifyOutput = true

[params]
env = "production"
title = "ExampleSite"
description = "ExampleSite description"
keywords = [ "Blog", "Portfolio", "PaperMod" ]
author = "Me"
images = [ "<link or path of image for opengraph, twitter-cards>" ]
DateFormat = "January 2, 2006"
defaultTheme = "auto"
disableThemeToggle = false
ShowReadingTime = true
ShowShareButtons = true
ShowPostNavLinks = true
ShowBreadCrumbs = true
ShowCodeCopyButtons = false
disableSpecial1stPost = false
disableScrollToTop = false
comments = false
hidemeta = false
hideSummary = false
showtoc = false
tocopen = false

  [params.assets]
  favicon = "<link / abs url>"
  favicon16x16 = "<link / abs url>"
  favicon32x32 = "<link / abs url>"
  apple_touch_icon = "<link / abs url>"
  safari_pinned_tab = "<link / abs url>"

  [params.label]
  text = "Home"
  icon = "/apple-touch-icon.png"
  iconHeight = 35

  [params.profileMode]
  enabled = false
  title = "ExampleSite"
  subtitle = "This is subtitle"
  imageUrl = "<img location>"
  imageWidth = 120
  imageHeight = 120
  imageTitle = "my image"

    [[params.profileMode.buttons]]
    name = "Posts"
    url = "posts"

    [[params.profileMode.buttons]]
    name = "Tags"
    url = "tags"

  [params.homeInfoParams]
  Title = "Hi there 👋"
  Content = "Welcome to my blog"

  [[params.socialIcons]]
  name = "twitter"
  url = "https://twitter.com/"

  [[params.socialIcons]]
  name = "stackoverflow"
  url = "https://stackoverflow.com"

  [[params.socialIcons]]
  name = "github"
  url = "https://github.com/"

[params.analytics.google]
SiteVerificationTag = "XYZabc"

[params.analytics.bing]
SiteVerificationTag = "XYZabc"

[params.analytics.yandex]
SiteVerificationTag = "XYZabc"

  [params.cover]
  hidden = true
  hiddenInList = true
  hiddenInSingle = true

  [params.editPost]
  URL = "https://github.com/<path_to_repo>/content"
  Text = "Suggest Changes"
  appendFilePath = true

  [params.fuseOpts]
  isCaseSensitive = false
  shouldSort = true
  location = 0
  distance = 1_000
  threshold = 0.4
  minMatchCharLength = 0
  keys = [ "title", "permalink", "summary", "content" ]

[[menu.main]]
identifier = "categories"
name = "categories"
url = "/categories/"
weight = 10

[[menu.main]]
identifier = "tags"
name = "tags"
url = "/tags/"
weight = 20

[[menu.main]]
identifier = "example"
name = "example.org"
url = "https://example.org"
weight = 30

```
config 부분은 테마마다 상이 하므로 테마의 문서를 확인하면서 변경해주어야 한다.
[blog/config.toml at master · Topasm/blog (github.com)](https://github.com/Topasm/blog/blob/master/config.toml)
위는 papermod를 사용한 내 블로그의 예시 이다.

### 글 작성

드디어 글을 작성할 차례이다. Vscode 에서 Ctrl + ` 키를 눌러 터미널을 띄운다. 그리고 아래 명령어를 입력하면 content 폴더 아래 posts 폴더가 생기고 md(마크다운) 파일이 생긴다.
```
hugo new posts/글_tile.md
```
 ### 로컬에서 테스트
글을 작성했다면 Ctrl + s 로 저장하고
```
Hugo server -D
```
를 하면 http://localhost:1313/ 에서 본인의 블로그 포스트를 확인할 수 있다.
글을 수정하거나 config.toml 파일을 변경해서 저장할 때마다 브라우저에서 바로 확인 할 수 있으므로, 초기 설정할 때 유용하다.

이제 깃헙에 올리고 빌드 스크립트를 짜면 블로그를 인터넷으로 접속할 수 있다.
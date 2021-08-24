---
title: "마크다운 문법 정리"
date: 2021-08-24T21:11:13+09:00
categories: [web]
tags: [markdown, tips, web]
draft: false
---


블로그 개설 후 글을 쓰려고 하니 블로그에 가독성 좋은 글을 쓰기 위해서는 마크다운 문법에 대한 복습이 필요하다고 생각이 들었다. 최대한 내가 쓸 문법들만 모아서 정리해보았다.


### Heading 제목
```
# H1   
## H2 
### H3
```
# H1   
## H2 
### H3  

### Bold 볼드 Italic 이탈릭 Strikethrough 줄긋기
```
**bold text**
*italicized text*
~~줄긋기~~
```
**bold text**
*italicized text*
~~줄긋기~~
### Blockquote 인용
```
> blockquote 인용하고 싶은글
```
> blockquote 인용하고 싶은글
### Ordered List 순서있는 리스트
```
1. First item
2. Second item
3. Third item
```
1. First item
2. Second item
3. Third item

### Unordered List 순서 없는 리스트
```
- First item
- Second item
- Third item
```
- First item
- Second item
- Third item
### Code 코드(한줄)
```
`code in the home`
```
`code in the home`
### Horizontal Rule 가로줄
```
---
```
---
### Link 링크
```
[링크 제목](https://github.com/Topasm)
```
[링크 제목은 내 깃헙](https://github.com/Topasm)
### Image 이미지
```
![alt text](https://이미지_주소images/image.png)
```
![20190628_140333](https://user-images.githubusercontent.com/24962064/123507466-8b996a80-d6a4-11eb-8924-91e980d115ab.jpg)


### Table 표
```
| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |
```

| Syntax | Description |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |
### 코드블록
\``` 이걸 위아래 붙여 준다.
```
{
  "c", "java"를 뒤에 붙여 주면
  언어에 맞게 하이라이팅 된다.
}
```


### Task List
```
- [x] 체크표시 있음
- [ ] 체크표시 없음
```

- [x] 체크표시 있음
- [ ] 체크표시 없음

### youtube

중괄호 2개 부등식기호1개로 하고 \{랑 \<로 ( youtube v머시기 코드)


https://youtu.be/vZ4Os97-wVQ
주소 뒷부분의 코드를 따서 붙여넣으면 된다  

{{< youtube vZ4Os97-wVQ >}}
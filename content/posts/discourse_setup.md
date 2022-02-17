---
title: "동아리 홈페이지용 Discourse 설치기"
date: 2022-01-15T22:35:38+09:00
categories: [rats, server, discourse]
tags: [web]
draft: false
---

동아리 홈페이지로 여러 국산 php 오픈소스를 사용하다가 최종적으로 discourse 로 넘어왔다.

국산 서비스의 장점
* 한글 지원 잘됨
* 가벼움, 용량 작음, 싸게 운영가능(램 500mb 부터는 쓸 수 있음)
* php 라 실시간으로 서버 수정이 가능함
* 익숙한 게시판 구조

국산 서비스의 단점
* 오래된 코드, 구조로 커스텀이 쉽지 않음
* 웹표준에 덜 적합
* 마크다운 지원 안함
* 유튜브 임베딩이 번거로움

국산 서비스 쓸만 하긴 하다 하지만 개인적으로 업데이트가 많이 됨에도 묘하게 현대적인 부분과 구형인 부분이 공존하게 된다. 커스텀 하면 되긴 하지만 너무 번거롭다. discourse 도 완벽하게 현대적이진 않지만 백업, 서버 구축 면에서 훨씬 쉽고 특히 서버 이전이 쉽다. 관리데이터도 깔끔하게 보이고 마크다운, 코드 하이라이팅이 잘 지원되고, 결정적으로 유튜브가 링크만 넣으면 임베딩이 된다.

단점도 있긴하다.
* 도커가 기본, ruby 언어로 구성되어 사양을 많이 먹음(램 1.5g 는 되야 한다)
* 사이트 수정이나 업데이트시 사이트 접속이 막힘
* 마크다운을 못쓰는 사람이 많음
* 포럼식 구조? 로 한국인한테 익숙하지 않은 구조
* 완벽하지 않은 한글화(관리자 영역을 제외하고는 전부 한글화 되어있다)


아무튼 동아리 홈페이지를 저렴하게 운영하기 위해 현재는 오라클 클라우드를 이용하고 있다.
참고적으로 구글 클라우드 램 1.5 hdd 50g cpu 최소 사양으로 했을때 월 3만원이 나왔다.
오라클은 램 1g(좀 버거움) hdd 100 cpu 1코어 평생 무료로 쓸 수 있다. 국산 서비스는 잘 구동 가능한데 discourse 돌리기엔 좀 버겁다. 사용자가 그렇게 많지 않으므로 일단 운영중인데 자체 서버를 구할 수 있으면 넘어갈 예정이다.

구글클라우드랑 오라클 클라우드를 살짝 비교하면 구글은 cpu 가 최소 사양인데 (월3만원이긴하다) discourse 빌드에 15분 정도 오라클은 무료서버 기준 1시간 정도 걸린다. ssh 접속도 구글은 웹으로 할 수 있어서 편하다. 구글클라우드에서 서버구성 했을때 에러가 거의 없었다. 오라클은 무료라 그런지 시행착오가 많았다.(특히 네트워크쪽 port 부분에 문제가 있는듯 하다)


아무튼 설치 과정은 아래와 같다.

### 동아리 서버용 디스코스 설치 명령어 모음

```
sudo apt update
sudo apt upgrade -y
```

패키지 업그레이드

```
sudo timedatectl set-timezone 'Asia/Seoul'
```
시간 변경

```
sudo wget -qO- https://get.docker.com/ | sh
```
도커 설치

```
docker version
```

도커버전 확인

```
sudo usermod -aG docker $USER
```

도커 권한 부여(이건 안넣어도 되는듯 하다)

```
sudo service docker restart
```
도커 재시작

```
sudo -s
git clone https://github.com/discourse/discourse_docker.git /var/discourse
cd /var/discourse
```
깃으로 다운로드

```
iptables -I INPUT -p tcp --dport 80 -j ACCEPT
iptables -I INPUT -p tcp --dport 443 -j ACCEPT
```
서버 포트 오픈

```
sudo netfilter-persistent save
sudo netfilter-persistent reload
```

세팅 저장

```
./discourse-setup
```

디스코스 설치 시작


```
Hostname for your Discourse? [discourse.example.com]: 홈페이지 주소
Email address for admin account(s)? [me@example.com,you@example.com]: 어드민 이메일(개인)
SMTP server address? [smtp.example.com]: stmp 서버(난 메일건 썻다)
SMTP port? [587]: 기본이 587
SMTP user name? [user@example.com]: 메일건 도메인세팅 가면 있다
SMTP password? [pa$$word]: 메일건 도메인세팅에서 리셋누르면 회색창으로 뜬다 카피
Let's Encrypt account email? (ENTER to skip) [me@example.com]: https 하는거
Optional Maxmind License key () [xxxxxxxxxxxxxxxx]:패스
```

```
./launcher rebuild app
```

리빌드및 업데이트

```
nano containers/app.yml
```

서버 정보 수정

기다림의 시간


계속 안되다가 드디어 됬는데 해결 방법으로는

vcn 설정 전부 날리고 고정 ip 주소를 oracle 로 다시 받았다. 오라클 클라우드 오류가 생긴다면 vcn, subnet 설정을 날리고 다시 해보자.
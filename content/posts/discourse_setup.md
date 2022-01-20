---
title: "Discourse_setup"
date: 2022-01-15T22:35:38+09:00
categories: [rats, server, discourse]
tags: [web]
draft: false
---

동아리 서버용 디스코스 설치 명령어 모음


sudo apt update
sudo apt upgrade -y

패키지 업그레이드

sudo timedatectl set-timezone 'Asia/Seoul'
시간 변경

sudo wget -qO- https://get.docker.com/ | sh

도커 설치

docker version


도커버전 확인

sudo usermod -aG docker $USER


도커 권한 부여

sudo service docker restart

도커 재시작
sudo -s
git clone https://github.com/discourse/discourse_docker.git /var/discourse
cd /var/discourse

깃으로 다운로드

iptables -I INPUT -p tcp --dport 80 -j ACCEPT
iptables -I INPUT -p tcp --dport 443 -j ACCEPT

서버 포트 오픈


sudo netfilter-persistent save
sudo netfilter-persistent reload


세팅 저장

./discourse-setup

디스코스 설치 시작


Hostname for your Discourse? [discourse.example.com]: 홈페이지 주소
Email address for admin account(s)? [me@example.com,you@example.com]: 어드민 이메일(개인)
SMTP server address? [smtp.example.com]: stmp 서버(난 메일건 썻다)
SMTP port? [587]: 기본이 587
SMTP user name? [user@example.com]: 메일건 도메인세팅 가면 있다
SMTP password? [pa$$word]: 메일건 도메인세팅에서 리셋누르면 회색창으로 뜬다 카피
Let's Encrypt account email? (ENTER to skip) [me@example.com]: https 하는거
Optional Maxmind License key () [xxxxxxxxxxxxxxxx]:패스



./launcher rebuild app

리빌드및 업데이트

nano containers/app.yml

서버 정보 수정

기다림의 시간


계속 안되다가 드디어 됬는데

vcn 설정 전부 날리고 고정 ip 주소를 oracle 로 받았다. 오라클 클라우드 오류가 생긴다면 vcn, subnet 설정을 날리고 다시 해보자.
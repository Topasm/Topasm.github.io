---
title: "WSL2_ros_install"
date: 2022-02-16T21:19:33+09:00
categories: []
tags: []
draft: true
---


WSL 설치법(윈도우10)

우선 윈도우 터미널 설치를 추천 한다.

https://www.microsoft.com/ko-kr/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab


설치되었다면,


powershell 또는 cmd 실행(관리자 모드)

```
wsl --install
```

설치 끝

많이 나는 오류
바이오스에서 cpu 가상화 옵션 허용
윈도우 기능에서 wsl 허용


https://sourceforge.net/projects/vcxsrv/

VcXsrv 설치

https://ropiens.tistory.com/157

링크 참조

sudo apt-get install dbus-x11 gnome-terminal



export DISPLAY=$(awk '/nameserver / {print $2; exit}' /etc/resolv.conf 2>/dev/null):0.0 >> ~/.bashrc


wsl 에서 ros 설치하기 ( neotic)


## locale 변경
```
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

http://wiki.ros.org/noetic/Installation/Ubuntu


뒤로는 링크와 같다

탐색기 실행

explorer.exe .


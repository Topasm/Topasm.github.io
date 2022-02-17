---
title: "WSL2_ros_install"
date: 2022-02-16T21:19:33+09:00
categories: []
tags: []
draft: true
---

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


sudo apt-get install dbus-x11 gnome-terminal



export DISPLAY=$(awk '/nameserver / {print $2; exit}' /etc/resolv.conf 2>/dev/null):0.0 >> ~/.bashrc


https://ropiens.tistory.com/157
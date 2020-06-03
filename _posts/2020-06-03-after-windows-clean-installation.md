---
title: Work after Windows 10 clean installation
description: The following are some of the things I have to do after installing windows. It will be very comfortable for me to use. I don’t know if it is suitable for you. Do you want to try it?
tags: [Windows, English]
style: border
color: success
language: en
comments: true
---

## Activation of your Windows 10
```sh
slmgr -ipk {your product key}
slmgr -skms {kms server address of your company}
slmgr -ato
```

## Installation of some useful tools
* [Msys2](https://www.msys2.org/)
* [AutoHotKey](https://www.autohotkey.com/)
* [Ricty](https://github.com/edihbrandon/RictyDiminished)

## Configuration of msys2
```sh
pacman -S git emacs tmux fish gcc python
cd ~
git clone https://github.com/xinii/xinconfig .xinconfig
cd .xinconfig
./setenv fish
exec fish
set_el auto
set_el cn
change_emacs xin
emacs
ssh-keygen -A
emacs /etc/ssh/sshd_config
 #Port ****
 #PasswordAuthentication no
cat {path to your pub key} > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
/usr/bin/sshd
```

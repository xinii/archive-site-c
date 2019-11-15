---
title: How to install Linux Mint from USB device
tags: [Linux, Linux Mint, Install, USB, Chinese]
style: fill
color: danger
description: 如何利用USB設備安裝Linux Mint
---

**重要**：在开始下面的工作之前，首先确保U盘没有存任何东西，或者里面没有放任何的重要数据（因为烧录会导致数据丢失），同时电脑上已经准备好空的分区（安装到的目标分区的数据也会被抹掉）。

## 準備一個用於安裝Linux Mint的USB設備

首先準備一個USB設備，可以是U盤也可以是USB的移動硬盤，
之後會在這個上面寫入供安裝Linux Mint的安裝程式。

* 如果你使用的是Windows操作系統，那麼點擊
[這裡](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-windows#0)
來查看Ubuntu官方的教程以創建一個可以安裝Linux的USB設備。

**注意**：上面的教程是教你如何製作一個用於安裝Ubuntu的USB設備，
安裝Linux Mint的情況下僅需要把涉及到iso文件的地方換成Linux Mint的iso文件，其他地方完全相同。

* 其中會用到的軟件叫做Rufus，上面的教程裡面也有提到，點擊
[這裏](https://rufus.akeo.ie/)
打開Rufus的官方網站，你也可以點擊
[這裏](https://github.com/pbatard/rufus/releases/download/v3.5/rufus-3.5.exe)
直接下載Rufus。

## Linux Mint的iso文件

前一節提到的Linux Mint的iso文件需要從下面的地方獲取。點擊
[這裏](https://linuxmint.com/)
打開Linux Mint的官方網站。或者你也可以點擊
[這裏](http://mirrors.evowise.com/linuxmint/stable/19.1/linuxmint-19.1-cinnamon-64bit.iso)
直接下載Linux Mint 19.1版本。

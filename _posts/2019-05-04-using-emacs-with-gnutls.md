---
title: The importance of gnutls for emacs
tags: [Emacs, Gnutls, HTTP, HTTPS, Chinese]
style: border
color: warning
description: 在使用emacs时gnutls的重要性
author: xin
language: zh
---

若当前环境没有gnutls，
那么在使用emacs源代码进行编译安装前的配置
（`./configure`）时可以临时使用`--with-gnutls=no`选项，
以使编译安装能够顺利进行。
例如下面的配置：

```sh
bash configure --prefix=$HOME/.local --with-gif=no --with-gnutls=no
```

上面的例子虽然可以正常安装emacs到`$HOME/.local`目录，
但缺少了gnutls的支持，
emacs内就只能使用http协议而并不能使用https协议，
虽然在emacs初始化时可以将melpa的链接都改为http协议解决问题，
但如果后期使用`google-translate`之类的包时还是会遇到问题。

例如即使在elpa下将`google-translate`包内的所有`.el` 文件中出现的`https`改为`http`，
中途还是会出现自动使用某些https服务的情况，从而导致翻译异常。
（这里需要注意，修改后需删除所有`.elc`文件以强制重新编译使修改生效）

上面问题的解决办法很简单，只需在当前环境安装gnutls即可。

以OpenSUSE为例，在终端下运行下面的语句即可完成安装。

```sh
sudo zypper install gnutls
```

另外，在安装emacs时，如果make后报以下错误，

```sh
checking for library containing tputs... no
configure: error: The required function 'tputs' was not found in any library.
The following libraries were tried (in order):
  libtinfo, libncurses, libterminfo, libcurses, libtermcap
Please try installing whichever of these libraries is most appropriate
for your system, together with its header files.
For example, a libncurses-dev(el) or similar package.
make: *** No targets specified and no makefile found.  Stop.
make: *** No rule to make target 'install'.  Stop.
```

那么对于OpenSUSE的环境可能需要ncurses-devel的包，
执行下面的语句安装即可。

```sh
sudo zypper install ncurses-devel
```

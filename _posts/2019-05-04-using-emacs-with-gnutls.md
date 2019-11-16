---
title: The importance of gnutls for emacs
tags: [Emacs, Gnutls, HTTP, HTTPS, Chinese]
style: fill
color: warning
description: 在使用emacs時gnutls的重要性
---

若當前環境沒有gnutls，
那麽在使用emacs源代碼進行編譯安裝前的配置
（`./configure`）時可以臨時使用`--with-gnutls=no`選項，
以使編譯安裝能夠順利進行。
例如下面的配置：

```sh
bash configure --prefix=$HOME/.local --with-gif=no --with-gnutls=no
```

上面的例子雖然可以正常安裝emacs到`$HOME/.local`目錄，
但缺少了gnutls的支持，
emacs內就只能使用http協議而並不能使用https協議，
雖然在emacs初始化時可以將melpa的鏈接都改為http協議解決問題，
但如果後期使用`google-translate`之類的包時還是會遇到問題。

例如即使在elpa下將`google-translate`包內的所有`.el` 文件中出現的`https`改為`http`，
中途還是會出現自動使用某些https服務的情況，從而導致翻譯異常。
（這裏需要註意，修改後需刪除所有`.elc`文件以強制重新編譯使修改生效）

上面問題的解決辦法很簡單，只需在當前環境安裝gnutls即可。

以OpenSUSE為例，在終端下運行下面的語句即可完成安裝。

```sh
sudo zypper install gnutls
```

另外，在安裝emacs時，如果make後報以下錯誤，

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

那麽對於OpenSUSE的環境可能需要ncurses-devel的包，
執行下面的語句安裝即可。

```sh
sudo zypper install ncurses-devel
```

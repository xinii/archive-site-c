---
title: SSH configuration
description: Very headache for ssh disconnection? Want to use ssh on the Android app termux? Click to see
tags: [SSH, Japanese]
style: fill
color: success
language: ja
comments: true
---

## sshの途切れる現象
- sshでリモートサーバにログインしているときに`Write failed: Broken pipe`と表示されて接続が切れてしまうことがある。
- sshはある程度の時間操作をせずにいるとタイムアウトにより自然に切断される仕組みになっているため，クライアント側やサーバ側でsshの設定を変更する必要がある。

#### 対処法
- クライアント側で対処

`/etc/ssh/ssh_config`または`~/.ssh/config`に以下の内容を記述する
```sh
ServerAliveInterval 15
ServerAliveCountMax 10
```
この設定で，15秒ごとに10回応答確認をサーバに送り，
それでも応答がない場合にタイムアウトになる。

- サーバ側で対処

`/etc/ssh/sshd_config`に以下の内容を記述する
```sh
ClientAliveInterval 30
ClientAliveCountMax 5
```
この設定で，30秒ごとにクライアントに5回応答確認をクライアントに送り，
それでも応答がなければタイムアウトになる。

#### その他
tmuxやscreenを使えば途中で接続が切れても
再度リモートサーバにログイン，
セッションをattachすれば済むのでお勧め。


## android termux sshd
#### Android側のインストール作業
```sh
apt install openssh
```

#### 鍵を設定
```sh
ssh-keygen
cat ~/.ssh/id_rsa.pub > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
```

#### テスト起動
```sh
sshd -d
```

#### 本番起動
```sh
sshd
```

#### PC側
Android側で生成したプライベートキー`~/.ssh/id_rsa`を持ってきて，
SSHクライアントに読み込んで設定して，
ユーザー設定なしで，IPとポート`8022`を指定して接続

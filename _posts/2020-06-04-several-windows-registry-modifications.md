---
title: Several windows registry modifications for the keyboard
description: Several windows registry modifications for the keyboard
tags: [Windows, Japanese]
style: fill
color: primary
language: ja
comments: true
---

## スキャンコードマップ

```
コンピューター\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout
```

新規 - バイナリ値(B) - Scancode Map

| Index  | Scancode      | 意味           | Scancode      | 意味             |
|--------|---------------|----------------|---------------|------------------|
| `0000` | `00 00 00 00` | バージョン     | `00 00 00 00` | フラグ           |
| `0008` | `08 00 00 00` | マッピング数   | `1D 00 3A 00` | LCtrl <- Caps    |
| `0010` | `3A 00 1D 00` | Caps <- LCtrl  | `1D E0 38 00` | RCtrl <- LAlt    |
| `0018` | `38 00 7B 00` | LAlt <- 無変換 | `38 E0 70 00` | RAlt <- かなキー |
| `0020` | `38 E0 79 00` | RAlt <- 変換   | `01 00 38 E0` | ESC <- RAlt      |
| `0028` | `00 00 00 00` | 終端ヌル値     |               |                  |

## 他の言語の入力法のキーボードレイアウトをKBD106に変更

```
コンピューター\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard Layouts\00000804
```
Layout File: KBDUS.DLL -> KBD106.DLL

## その他のレジストリー

```
コンピューター\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace
```

---
title: A pitfall when insert a figure into LaTeX
description: LaTeXのplatexを使う際のfigureに関する落とし穴
tags: [Pitfall, LaTeX, Figure, Japanese]
style: fill
color: dark
comments: true
---

platexを使う際に，
epsが問題がないが，
なぜかそのepsを入れたらビルドが失敗。

しかも失敗した時のログをみると，
なかなか問題がわからない。

例えば，全ての入れたfigureの定義が見つからないなどのレポート。
その時に，epsを正方形に近い形状を
矩形にしたら，問題が解決できた。
原因はまだ不明。
たまにこのようなことがあるので，
結構ハマったので，一応記録を

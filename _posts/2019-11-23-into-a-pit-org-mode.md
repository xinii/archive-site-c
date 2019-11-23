---
title: A pitfall when using org-mode with python code block
tags: [Pitfall, Org-mode, Emacs, Python, Japanese]
style: fill
color: danger
description: Org-modeの中にPythonを実装した際の落とし穴
author: xin
comments: true
---

僕は家計簿をorg-modeで記録しています，
しかし，以下のエラーが出たことがある。

```
  File "<stdin>", line 3
SyntaxError: Non-UTF-8 code starting with '\xe3' in file <stdin> on line 3, but no encoding declared; see http://python.org/dev/peps/pep-0263/ for details
```

例の`# -*- coding: utf-8 -*-`を先頭につけてもダメです。

解決法は以下のようなコードブロックのヘッダーを，

```
#+begin_src python :results file :var data=test
```

以下のように変換します。

```
#+begin_src python :results file :var data=test[, 0:2]
```

つまり，必要な数字や日付などのorg-modeのtableの列だけを
pythonに転送すると，以上の問題が解決できますが，
根本的に`# -*- coding: utf-8 -*-`をコードブロックの中に
効く方法はまだわかりません。
わかる方は教えていただければありがたいと思います。

コメントよろしくお願いします。

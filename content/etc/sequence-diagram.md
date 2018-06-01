+++
title = "シーケンス図を埋め込む話"
date = "2018-04-15T15:07:43+09:00"
draft = false
tags = ["etc", "blog"]
description = ""
image = "/images/avatar.jpg"

[author]
name = "依藤"
url = "https://e10ulen.github.io/"
avatar = "/images/avatar.jpg"
license = "by-sa"
github = "e10ulen"
twitter = "e10ulen"
[scripts]
mathjax = false
mermaidjs = true
+++

Hugoというツールだと、Markdown書式で記事を書くのですが、  
自作ツールに追加するかどうか調べる最中に、  
同じhugo製のサイトでシーケンス図がありまして、  
いつか使うかもしれないし、使い方の備忘録をしておこうと思ったので今回の記事です。

{{< fig-mermaid title="カバとカバン" >}}
sequenceDiagram
    カバ->>+カバン: あなた，泳げまして？
    カバン-->>-カバ: いえ
    カバ->>+カバン: 空は飛べるんですの？
    カバン-->>-カバ: いえ
    カバ->>+カバン: じゃあ，足が速いとか？
    カバン-->>-カバ: いえ
    カバ->>カバン: あなた，何にもできないのねぇ
    loop ひとりヘコむ
        カバン->>カバン: ううっ
    end
{{< /fig-mermaid >}}

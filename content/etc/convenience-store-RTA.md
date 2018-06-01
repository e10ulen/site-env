+++
title = "コンビニ精算RTA"
date = 2018-04-19
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
# なにこれ
[いつもお世話になってるSNS][1] にいる[うらひと][2] さんの[Qiita][3] 投稿を見てたら  
[コンビニ精算RTAをUMLのシーケンス図で書いてみる][4] を見つけて、  
開いて見たら実践してみた結果のところにセルフレジではどうかってあったのでちょっと考えてみる

## うらひとさんの考えるシーケンス図

{{< fig-mermaid title="NotセルフRTA" >}}
sequenceDiagram

客 ->> 店員: 品物を渡す
店員 -->> レジ: 品物をスキャン
客 ->> 店員: ポイントカードを渡す
店員 -->> レジ: ポイントカードをスキャン
レジ -->> 店員: ポイントカードを戻す
店員 -->> 客: ポイントカードを受け取る
レジ -->> 店員: 品物をレジ袋に入れる
客 -->> 店員: 「支払いICカードで」
店員 -->> レジ: ICカードの支払いに設定
店員 ->> 客: レジ袋を受け取る
客 -->> レジ: ICカードをタッチ
レジ -->> 客: ICカード精算完了
店員 ->> レジ: 精算完了ボタンを押す
レジ ->> 店員: レシートを印刷
店員 ->> 客: レシートを渡す

{{< /fig-mermaid >}}

## 依藤の考えるセルフレジシーケンス図
{{< fig-mermaid title="セルフレジRTA" >}}
sequenceDiagram
participant a as 客
participant c as レジ
a ->> c: 品物を台に置く
alt 袋は？
a -x c: レジ袋を購入
else
a ->> c: マイバッグを選択
end
c -->> a: ポイントつくよ
a ->> c: ポイントカードを通す


loop 品物スキャン
    a ->> c:品物をスキャン
    c -->>a:袋に入れて
end
a ->> c: 支払い方法選択
alt 支払いは？
a --x c: カードで
else
a ->> c: 現金で
end

alt 割引券を
c ->> c:印刷する
else
c -x c:印刷しない
end
c -->> a:お釣りを出す
c -->> a:レシートを印刷する
{{< /fig-mermaid >}}

## 結論
なんかごちゃごちゃしてしまった気がする。  
１時間程度しか思考しつつ書いてないので矛盾が矛盾があったりしそう。  
流れ、ってかけるといいね。  
[1]:https://ichiji.social
[2]:https://ichiji.social/@urahito_solution
[3]:https://qiita.com/urahito_solution
[4]:https://qiita.com/urahito_solution/items/d198407d3a2e3660c1a3
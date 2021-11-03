---
title: "Windows Subsystem for Linuxという異物"
date: 2021-10-29T02:55:43+09:00
author: ""
keywords: ["WSL", "Windows","Linux"]
cover: ""
summary: ""
pin: false
---

[WSLとは][1]なんだけど、それはWikipediaさんに任せて…。

年季の入ったうちのPC君は一応ゲーミングPCなので、  
Windowsを投げ捨ててLinuxに尻尾を振ることができないんですよ。  
~~あと単純にいざとなったときのメンテナンスがやり切れる自信がない~~  
という事で、単純ながらHow to WSLをいざという時用に書き記しておく。
<!--more-->
簡単ではあるんだけどね。

__WSL ではなく WSL2にすること__

1. WindowsTerminal install
2. Ubuntu-20.04 install

とりあえずここで一回起動して、  
起動したら順次アップデートなりをこなしていく。  
うちの環境はとりあえずgolangのPPAを突っ込んでおかないとgoの開発環境が作れない。  
今の環境上vimとかも用意してるけど単純に読みやすいという利点だけでWSLforVSCodeを使っている。  
あと、ロケールとかを日本に変更。あんまり差を感じないけどなにかと楽なので…  

```bash
sudo add-apt-repository -y ppa:longsleep/golang-backports
sudo apt update && sudo apt upgrade
sudo apt install language-pack-ja
sudo update-locale LANG=ja_JP.UTF-8
```

あとはgihubにsshを登録したりなんだりかんだり…をする。
VSCodeにgoの拡張機能を入れたりもする。

気になる技術
[Arch for WSL](https://github.com/yuk7/ArchWSL/blob/master/i18n/README_ja.md)

[1]:https://ja.wikipedia.org/wiki/Windows_Subsystem_for_Linux
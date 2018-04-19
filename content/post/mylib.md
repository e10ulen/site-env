+++
title = "自作ライブラリの使い方"
date = 2018-04-19
lastmod = ""
tags = ["blog", "Golang", "Github"]
archives = "2018"
toc = true
+++
# これなに
[自作ライブラリ](https://github.com/sandbox/lib)
##  IsTerminalの使い方メモ
呼び方
{{< highlight go "linenos=inline,linenostart=1" >}}
package main

import (
    "fmt"
    "github.com/e10ulen/sandbox/lib"
)
func main(){
    fmt.Println("Terminalかの判定処理")
	var foo bool
	var bar bool
	var baz string
	fmt.Println(lib.IsTerminal(foo, bar, baz))
}
{{< /highlight >}}
判定したはいいけど、使い道is何？（遠い目  
[go-isatty](https://github.com/mattn/go-isatty)がなんとなく使いたくてこの判定書いたけど使いみち考えてなかった。  

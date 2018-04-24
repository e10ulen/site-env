+++
title = "自作ライブラリの使い方"
date = "2018-04-19"
lastmod = "2018-04-24"
tags = ["blog", "Golang", "Github"]
archives = "2018"
toc = true
+++
# これなに
[自作ライブラリ](https://github.com/e10ulen/sandbox/lib)
## 使い方
{{< highlight go "linenos=inline,linenostart=1" >}}

package main  
  
import (  
    "os"
    "fmt"  
    "github.com/e10ulen/sandbox/lib"  
)  
  
func main(){  
    fmt.Println("Scanner使った一行読み込み")  
    lib.ScanLine(args)  
    fmt.Println("Terminalかの判定処理")  
    lib.IsTerminal()  
    fmt.Println("Markdown4html")  
    lib.Markdown4html()  
    fmt.Println("サーバー起動します")  
    port := "9090"  
    dir, _ := os.Getwd()  
    lib.MiniServe(port, dir)  
}  
{{< /highlight >}}

###  解説

必要ないかもしれませんが、解説していきます（自分で書いてて理解していない部分を理解するためにも  


#### lib.ScanLine(why)

{{< highlight go "linenos=inline, linenostart=17" >}}
func ScanLine(why string) string {
	fmt.Print(why)
	fmt.Print("input :")
	scanner := bufio.NewScanner(os.Stdin)
	scanner.Scan()
	scntext := scanner.Text()
	fmt.Println("input is", scntext)
	return scntext
}
{{< /highlight >}}
ScanLineが引数を一つ求めるのは、  
自作CLIツールで使っているケースでこのように使っている。
{{< highlight go "linenos=inline, linenostart=18">}}
	dir, _ := os.Getwd()
	port := "PortNo :"
	get := lib.ScanLine(port)
	lib.MiniServe(get, dir)
{{< /highlight >}}
なんのためのScanなんだろうって自分で読んでてわからなくなることが多々あったので、  
スキャンするときに何を入れて欲しいのか聞かせるかということでこの場合だと、こうなる  
{{< highlight bash >}}
go run main.go s
PortNo :
input :

{{< /highlight >}}
この時、input : の場所で入力待ちが行われる。  

#### lib.Markdown4html()
{{< highlight go "linenos=inline, linenostart=52">}}
func Markdown4html() {
	gfn := "ファイル名を入力してください\n"
	md, err := ioutil.ReadFile(ScanLine("Markdown" + gfn))
	if err != nil {
		logf.Warn(err)
	}
	html := blackfriday.MarkdownCommon(md)
	dir, _ := os.Getwd()
	fn := ScanLine(gfn)
	file, err := os.OpenFile(dir+"/"+fn, os.O_CREATE|os.O_APPEND|os.O_RDWR, 0666)
	if err != nil {
		logf.Warn(err)
	}
	defer file.Close()

	ioutil.WriteFile(fn, html, 0666)
}
{{< /highlight >}}
先ほどのlib.Scan(args)がここでも使われている。  
用途としては、読み込むファイル名（マークダウンファイル）と、保存先のファイル名（この場合htmlファイル）を求めているが、  
どちらを先に聞いているか、ここをわかりやすくするために、lib.Scan(args)の引数を追加した。  
MarkdownならMarkdownファイル名を求めるべきだし、htmlファイルとして保存するのかはユーザに委ねるべきだし  
ということで先に共通項を変数にして、markdownファイル名を聞くときにだけ、先頭にMarkdownの文字列を足している  
#### lib.MiniServe(port, dir)
{{< highlight go "linenos=inline,linenostart=71">}}
func MiniServe(port, dir string) {
	http.Handle("/", http.StripPrefix("/", http.FileServer(http.Dir(dir))))
	err := http.ListenAndServe(":"+port, nil)
	if err != nil {
		logf.Fatal("ListenAndServe: ", err)
	}
}
{{< /highlight >}}

ここで注意してもらいたいのが、portも文字列として引数に必要にしていること。  
なおかつルートディレクトリを決めないと動かない事、  
簡単なサーバーでしかないので、ルーティングとか決める際はこれを使わず自分で書いたほうがいいのかもしれない。  


### その他
[logf](https://github.com/spiegel-im-spiegel/logf)をlogに使っていたが、cologを使う方向で定めたので、近日中に置き換える。  
[go-isatty](https://github.com/mattn/go-isatty)がなんとなく使いたくてこの判定書いたけど使いみち考えてなかった。  



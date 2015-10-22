# curl教學

如果要貼code到工作站，又怕code格式跑掉，可以使用`curl`這個功能! 這個功能方便又有效!

感謝[丕祐](https://github.com/BeMg "丕佑的github")提供技術支援!

# 基本操作

* 進入[Gists](https://gist.github.com/ "Gists from github")，將code貼上，並按下create public gist
![Gists](https://github.com/henrybear327/Data-structure/blob/master/Tutorial/Curl/gists.png)

* 點螢幕中間的`raw`，會顯示_純文字_版本的code
![Raw](https://github.com/henrybear327/Data-structure/blob/master/Tutorial/Curl/raw.png)

* 複製網址，應該會類似這樣
![Link](https://github.com/henrybear327/Data-structure/blob/master/Tutorial/Curl/link.png)

```
https://gist.githubusercontent.com/anonymous/6f7be483bdd78b37a60d/raw/a667ea4f2576c9583ce8b0330b2543c16b1c481b/%25E6%25B8%25AC%25E8%25A9%25A6
```

* 登入工作站。 _注意:_ 要用turnin功能，需要在csie0.cs.ccu.edu.tw登入才能用!

* 在你要存檔案的地方，輸入`curl` 加上 `你剛剛複製的網址`，並且輸入 ` > `
加上`你希望的檔案名稱`，這樣就會把網址所指向的code存到`你希望的檔案名稱`中!

例如(這樣code就會被下載到test.txt中!! 也可以將檔名直接指定為test.c，端看個人喜好！):

```
curl https://gist.githubusercontent.com/anonymous/6f7be483bdd78b37a60d/raw/a667ea4f2576c9583ce8b0330b2543c16b1c481b/%25E6%25B8%25AC%25E8%25A9%25A6 > test.txt
```
![Curl terminal](https://github.com/henrybear327/Data-structure/blob/master/Tutorial/Curl/curl%20terminal.png)
![Downloaded txt](https://github.com/henrybear327/Data-structure/blob/master/Tutorial/Curl/test.txt.png)

* 輸入`turnin ds.HWA `，加上你要交的檔案名稱。 例如: `turnin ds.HWA main.c readme.txt` ，這樣就會一次繳交main.c 和 readme.txt

* 輸入`turnin -ls ds.HWA`，就可以看到剛剛交的作業囉!

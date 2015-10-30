# 工作站開檔讀檔教學

#### by: 曾俊宏，黃鈺程

這次DS Demo時應該有不少人被雷到開檔讀檔的問題，希望這兩招大家可以學起來，很方便的。

兩個方法基本上都沒有動到什麼code，所以儘量學起來吧！

### 方法一、重導

用這個方法就跟你直接將測資輸入到運行中的程式是一樣的，所以你**完全不需要**去更改程式碼。

在程式經過編譯後，假設你所產生的執行檔是`a.out`，你要丟的測資是
在`input.txt`中，要輸出的檔名是`output.txt`的話，下這樣的指令即可:
```
./a.out < input.txt > output.txt
```
這樣一來，就會將`input.txt`的資料讀入你的程式，並將結果記錄到`output.txt`中。

如果你只想將測資讀進來，而答案直接輸出在螢幕上的話，就下這樣的指令即可:
```
./a.out < input.txt
```

### 方法二、`stdio.h` 下的 `freopen()`

這方法只要在你的 main() 最開頭處，加上**兩行**code即可！！（當然，視需求可以只打其中任一個）

`freopen()`的基本呼叫方式如下:
```
freopen("檔名", "r或w", stdin或stdout);
```

所以說，如果測資在`input.txt`，程式的輸出要存在`output.txt`的話，就打
```
freopen("input.txt", "r", stdin);
freopen("output.txt", "w", stdout);
```

第一行代表將 `stdin` 這個串流（stream）重導到 `input.txt`，我們知道我們在程式中 `scanf/getchar` 等操作都是
從 `stdin` 這個串流中讀入資料。所以加上這行後，相當於變成我們是從 `input.txt` 裡讀入了。

同理，第二行代表我們是把程式的輸出寫到 `output.txt` 裡
（將串流 `stdout` 導向 `output.txt`，`printf/putchar` 是將內容寫到 `stdout` 這個串流）。

建議你要檢查`freopen()`檔案讀寫是否成功，因為如果demo時出問題，可以很快的就知道
是沒有讀取到該讀的檔案所造成的！

```
if(freopen("檔名", "r或w", stdin或stdout) == NULL)
    YOUR_ERROR_MESSAGE_HERE;
```

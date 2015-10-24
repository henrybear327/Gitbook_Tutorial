# diff 使用教學

如果以後有類似資料結構的老鼠走迷宮作業，有數千行的output要和answer對答案時，不需
要一個字一個字自己對到天荒地老，而是可以直接交給電腦幫你做這件事喔!

在進入正題之前，先教大家如何讀入測資、如何將你所輸入測資的結果存到檔案中吧! 

這通常有兩種做法，一是使用重導，二是使用freopen。

### 重導

用這個方法就跟你直接將測資輸入到運行中的程式是一樣的，所以你完全不需要去更改程式碼。

使用方法如下: 程式經過編譯後，假設你所產生的執行檔是`a.out`，你要丟的測資是
在`input.txt`中，且你要輸出的檔名是`output.txt`的話，就下這樣的指令即可:
```
./a.out < input.txt > output.txt
```
這樣一來，就會將`input.txt`的資料讀入你的程式，並將結果記錄到answer.txt中。

你也可以只打
```
./a.out < input.txt
```
這樣一來，答案就會直接顯示在畫面上，而不是記錄到檔案中!

### `freopen()`

這方法也幾乎不用更動你原本的code，只要在你的main()最開頭加上兩行code即可!!
```
freopen("檔名", "r或w", stdin或stdout);
```

所以說，如果測資在`input.txt`，程式的輸出要存在`output.txt`的話，就打
```
freopen("input.txt", "r", stdin);
freopen("output.txt", "w", stdout);
```

如果你要檢查`freopen()`檔案讀寫有無成功，可以檢查return值是否為NULL
```
if(freopen("檔名", "r或w", stdin或stdout) == NULL)
    YOUR_ERROR_MESSAGE_HERE;
```

# Diff 使用

假設你的答案是在`answer.txt`的話，你可以用 `diff answer.txt output.txt` 來做比較。

如果按下enter後什麼都沒顯示，代表說兩個檔案是一模一樣的! 如果有顯示任何東西，就代表
檔案有些地方不同，需要debug囉!

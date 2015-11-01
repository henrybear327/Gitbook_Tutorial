# Insight 基本使用 | 黃鈺程

## 安裝

請參考 [這](../Cross-Compiler-Usage/README.md)

## 基本使用

0. 開啟 Insight

    使用指令，假設我 arm 解壓出來的資料夾是放在 `~（HOME）` 下
    （即 `~/con/` or `~/foo/`，那指令就是
    ```
    ~/con/bin/arm-elf-insight
    ```

    ![](http://i.imgur.com/6A1tGJE.png)

    開啟來的畫面：

    ![](http://i.imgur.com/vqmLnqD.png)


1. 使用 File/Open

    開啟執行檔（有些人沒辦法雙擊點選檔案，這時可以手動輸入檔案名稱）

    ※ 請注意，編譯出該執行檔時，gcc 的參數要有加 `-g`

    ![](http://i.imgur.com/yaE4IAs.png)

    Target 選 Simulator

    ![](http://i.imgur.com/jTzP2Eo.png)

2. 若各個視窗（Register, Stack, Memory）沒有顯示，則在 View 底下開啟他們。

3. 按 Run（工具列中那個看起來像是一個人在跑的圖示），之後就會看到這樣：

    ![](http://i.imgur.com/btKrORi.png)

4. 單步執行（按 s），綠色那行代表 **準備要執行** 的指令。

    ![](http://i.imgur.com/tdVohDI.png)

5. 結束時，檔案會跳到 `atexit.c`，這很麻煩

    ![](http://i.imgur.com/Fj0Aeya.png)

    所以我們會在程式碼的最後一行加入

    ```arm
    nop
    ```

    ![](http://i.imgur.com/btKrORi.png)

    他的作用類似於古早以前寫 C 最後面要加 `system("pause");` 一樣。
    這樣使用 Insight 來 debug，程式執行結束時，顯示的檔案才不會跳掉。
    雖然說，可以在最下面那排工具列，最左邊的那個文字框調回來，不過每次都調很麻煩…

# Insight 問題排除 | 黃資閔，曾俊宏

## register 修改後仍舊不變

![test1](https://cloud.githubusercontent.com/assets/9114484/10852607/8186f3fe-7f6c-11e5-8ea3-6a3b4a0ed5b9.png)


如圖，在執行第6行前，改變 `r0 = 1000`

但第7行結果卻是 `r2 = 100 - 50 = 50`

恩... 在不想更動到設定時(重裝 `arm-elf-insight` or ... )

 可以學習利用 `gdb` 更改數值(後面會提到在 `insight` 開啟 `gdb` )

```
set $r0 = 100
```
## crt0.s 問題

![test2](https://cloud.githubusercontent.com/assets/9114484/10852764/6e69257a-7f6d-11e5-8309-23f977a0686b.png)

open file or run 跑進了 crt0.s 了!

此時，莫急莫慌莫害怕，先將這 code 的紅色點去掉(對它`左鍵`)

![test3](https://cloud.githubusercontent.com/assets/9114484/10852812/c0e1c7ee-7f6d-11e5-9074-be0d52774a11.png)

再來，選擇原本應該執行的檔案，如下圖 (此時有可能跳出一些警告之類的，無視他即可)
![test4](https://cloud.githubusercontent.com/assets/9114484/10852852/02702aac-7f6e-11e5-9769-1007edb2116c.png)

再來，對 main 的 label 下一行點出一個 breakpoint (或是右鍵 jump to here )

![test5](https://cloud.githubusercontent.com/assets/9114484/10853024/f546841a-7f6e-11e5-83f9-a2545e41d79a.png)

如果前面沒先去除`crt0.s`的 breakpoint ，之後再次 run又會跑進去喔

p.s. 不過再次開起還是有這問題，就只能詢問教授了

## 在 insight 開啟 GDB

在上面工具列尋找

![test6](https://cloud.githubusercontent.com/assets/9114484/10864123/6427e5d6-801e-11e5-9a14-537859f5ece7.png)

之後就能下指令啦!

例如：

* 開檔
```
file (用 -g 參數編譯的執行檔檔名)
```

* 開始執行
```
run 或是 r
```

詳細GDB使用方式可以參考[這篇文章](./../../Linux/GDB/README.md)。

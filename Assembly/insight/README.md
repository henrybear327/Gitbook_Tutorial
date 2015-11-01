# Insight 問題排除 與 簡易 GDB 教學 | 黃資閔、曾俊宏

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

* 執行下一行指令
```
next 或是 n
```

* 執行下一道指令，連function都會進去一行一行執行
```
step
```

* 看某的變數的數值
```
print (變數名) 或是 p (變數名)
```

* 在每一次的 next 時,都顯示其中一個的 value
```
display (變數名)
```

* 設置 break point
```
break (行數) 或是 b (行數)
```

* 看看目前display, breakpoint等等的設定狀態
```
info break/display/...
```

* 開啟內建說明
```
help
```

** 使用terminal直接開啟 gdb

前置準備動作會多一些，但是run起來之後就跟用inight相同囉!

* 建議可以加 `-tui`，這樣會有GUI出現!!
```
./arm-elf-gdb -tui (用 -g 參數編譯的執行檔檔名，如hw1.exe)
```

* 要跑ARM的code，需要使用到模擬器
```
target sim
```

* Load (To download the compiled application to the target for debugging, invoke the command)
```
load
```

* 可以先手動加入`main()`的breakpoint
```
break main
```

* 開始執行
```
run
```

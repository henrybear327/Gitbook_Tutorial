# Insight 問題排除| 黃資閔

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

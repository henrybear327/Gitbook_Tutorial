# register 修改後仍舊不變

#### by: 黃資閔

![test1](https://cloud.githubusercontent.com/assets/9114484/10852607/8186f3fe-7f6c-11e5-8ea3-6a3b4a0ed5b9.png)

如圖，在執行第6行前，改變 `r0 = 1000`

但第7行結果卻是 `r2 = 100 - 50 = 50`

恩... 在不想更動到設定時(重裝`arm-elf-insight` or ...)

可以學習利用 `gdb` 更改數值

```
(gdb) set $r0 = 1000
```

# crt0.s 問題

![test2](https://cloud.githubusercontent.com/assets/9114484/10852764/6e69257a-7f6d-11e5-8309-23f977a0686b.png)

open file or run 跑進了 crt0.s了!

此時，莫急莫慌莫害怕，先將這code 的紅色點去掉(對它按下`左鍵`)

![test3](https://cloud.githubusercontent.com/assets/9114484/10852812/c0e1c7ee-7f6d-11e5-9074-be0d52774a11.png)

再來，選擇原本應該執行的檔案，如下圖 (此時有可能跳出一些警告之類的，無視他即可)

![test4](https://cloud.githubusercontent.com/assets/9114484/10852852/02702aac-7f6e-11e5-9769-1007edb2116c.png)

再來，對main的 label 下一行點出一個breakpoint (或是右鍵 jump to here)

![test5](https://cloud.githubusercontent.com/assets/9114484/10853024/f546841a-7f6e-11e5-83f9-a2545e41d79a.png)

如果前面沒先去除 `crt0.s` 的 breakpoint，之後再次 run 又會跑進去喔!

p.s. 不過再次開起還是有這問題，這就只能詢問教授了

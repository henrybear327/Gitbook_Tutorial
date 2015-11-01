# GDB 使用教學 | 曾俊宏

GDB是個非常方便且好用的debugger，雖然純文字介面有點嚇人，但是其實功能很強大、很實用的！！

# 開啟 GDB

在terminal裡，輸入指令
```
gdb (用 -g 參數編譯的執行檔檔名)
```

如果想要同時看到source code，可以加上`-tui`
```
gdb -tui (用 -g 參數編譯的執行檔檔名)
```

開啟之後，直接下 `run` 指令就可以囉！

# GDB 基本指令

* 開啟要被debug的檔案 (如果你用`gdb (執行檔檔名)` 啟動 GDB 的話，這個`file`指令就不必做了)
```
file (用 -g 參數編譯的執行檔檔名，例如：main.o)
```

* 開始執行
```
run 或是 r
```

* 執行下一行指令，function call會背當作一行，不會進去一行一行執行
```
next 或是 n
```

* 執行下一道指令，連function都會進去一行一行執行
```
step
```

* 看某的變數的數值
```
print (變數名) 或 p (變數名)
```

* 設置 break point
```
break (行數) 或 b (行數)
```

* 在每一次的 next/step 後,都要顯示數值的變數
```
display (變數名)
```

* 看看目前display, breakpoint等等的設定狀態
```
info break/display/...
```

* 開啟內建說明
```
help
```

## 使用 `arm-elf-gdb`

前面所提到的是一般的 C或C++ code 的 GDB 使用方式。
如果是用 `arm-elf-gdb`， 前置準備動作會多一些，但是 `run` 起來之後就沒什麼差別了！

* 開啟 `arm-elf-gdb`
```
./arm-elf-gdb -tui (用 -g 參數編譯的執行檔檔名，如hw1.exe)
```

* 要跑ARM的code，需要使用到模擬器
```
target sim
```

* 要記得 Load (To download the compiled application to the target for debugging, invoke the command)
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

* 看所有register的數值(直接輸入info可以查詢指令)
```
info all-registers
```

其餘的指令就查上面提到的部份就可以囉！

# GDB 使用教學 | 曾俊宏

GDB是個非常方便且好用的debugger，雖然純文字介面有點嚇人，但是其實功能很強大、很實用的!

多多動手操作試試看，你會發現 GDB 的強大之處!

# 開啟 GDB

在terminal裡，輸入指令(不用`./`)
```
gdb (用 -g 參數編譯的執行檔檔名)
```

如果想要同時看到source code，可以加上`-tui`，開啟陽春 GUI 版本的 GDB
```
gdb -tui (用 -g 參數編譯的執行檔檔名)
```

開啟 GDB 之後，直接下 `run` 指令就可以開始 debug 囉！

# GDB 基本指令

* 開啟要被debug的檔案 (如果你用`gdb (執行檔檔名)` 啟動 GDB 的話，這個`file`指令就不必做了)
```
file (用 -g 參數編譯的執行檔檔名，例如：main.o)
```

* 開始執行 (下過這個指令後，debug程序才正式展開! **注意!** 沒有設定break point的話，程式會一直執行到結束喔!!
break point的目的就是要debugger在特定地方停下來!)
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

* 設置 break point (建議 `run` 之前就先設定好基本的break point)
```
break (行數) 或 b (行數)
```

* 在每一次的 next/step 後, 都要顯示出數值的變數
```
display (變數名)
```

* 看看目前display, breakpoint等等的設定狀態
```
info break/display/...
```

* 看看 source code
```
list
```

* 開啟內建說明
```
help
```

## 使用 `arm-elf-gdb`

前面所提到的是一般的 C或C++ code 的 GDB 使用方式。
如果是用 `arm-elf-gdb`， 前置準備動作會多一些，但是 `run` 起來之後就沒什麼差別了！

* 到放`arm-elf-gcc`的資料夾，啟動 `arm-elf-gdb` (`-tui`可以同時讓你看到source code)
```
./arm-elf-gdb (用 -g 參數編譯的執行檔檔名，如hw1.exe)
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

其餘的指令就跟前面提到的部份相同囉！

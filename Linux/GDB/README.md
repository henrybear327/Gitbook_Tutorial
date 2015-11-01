# GDB 使用教學 | 曾俊宏

gdb 是個非常方便且好用的debugger，雖然純文字介面有點嚇人，但是其實功能很強大、很實用的!

多多動手操作試試看，你會發現 gdb 的強大之處!

基本上，gdb的操作流程是: 啟動gdb -> 載入檔案 -> 加入breakpoint等等 -> `run`。

# 啟動 gdb

在terminal裡，輸入指令 `gdb (用 -g 參數編譯的執行檔檔名)` ，**不用** 加`./`喔! 

範例指令如下:
```
gdb hw1.exe
```

如果想要同時看到source code，可以加上參數`-tui`，啟動陽春 GDB GUI 版本 

範例指令如下:
```
gdb -tui hw1.exe
```

啟動成功之後，基本上就是視情況需要，下指令操作 gdb 囉!

# GDB 基本指令

* 開啟要被debug的檔案 (如果你用`gdb (執行檔檔名)` 啟動 GDB 的話，這個`file`指令就不必做了)
```
file (用 -g 參數編譯的執行檔檔名例) 例如：file hw1.exe
```

* 執行要被debug的程式 (下過這個指令後，debug程序才正式展開! 這就像是你用`./`去執行一個程式一樣的意思。)

  **注意!** 沒有設定breakpoint的話，程式會一直執行到結束喔!! Breakpoint的目的就是要debugger在特定地方停下來!
```
run 或是 r
```

* 執行下一行指令，function call會被當作一行指令，不會進去function裡面一行一行執行
```
next 或是 n
```

* 執行下一道指令，連function都會進去一行一行執行
```
step
```

* 看某變數的數值
```
print (變數名) 或 p (變數名)
```

* 設置 breakpoint (建議 `run` 之前就先設定好基本的breakpoint)
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

* 看所有register的數值(直接輸入 `info` 可以查詢指令)
```
info all-registers
```

* 開啟內建說明
```
help
```

## 使用 `arm-elf-gdb`

前面所提到的是一般的 C 或 C++ code 的 gdb 使用方式。
如果是用 `arm-elf-gdb`， 前置準備動作會多一些，但是 `run` 起來之後就沒什麼差別了！

步驟一、 進入放 `arm-elf-gcc` 的資料夾，啟動 `arm-elf-gdb` (加上參數 `-tui` 可以讓你同時看到source code)
```
./arm-elf-gdb (用 -g 參數編譯的執行檔檔名，如hw1.exe)
```

步驟二、 如果要跑ARM的code，需要使用到模擬器
```
target sim
```

步驟三、 要記得 Load (To download the compiled application to the target for debugging, invoke the command)
```
load
```

步驟四、 可以先手動加入`main()`的breakpoint
```
break main
```

步驟五、 開始執行
```
run
```

其餘的指令就跟前面提到的完全相同囉！

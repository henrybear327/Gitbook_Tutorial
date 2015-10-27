# 版本說明

這個教學基本上是用老師原先公布的[Linux 64bit cross-compiler](https://drive.google.com/file/d/0B9W0GR7tEgdYcjhocDljdWZaNTA/view?usp=sharing)版本，
但是如果你是用32bit的也沒差，因為操作的方式是一樣的(而且老師有說64-bit的其實好像有一些小bug，像說用insight要開檔案時比較麻煩)。

# 基本terminal操作

如果你對`cd`和`ls`等等指令不熟，請先看[這篇教學](https://github.com/henrybear327/Tutorial/tree/master/Linux/Terminal-Common-Instruction)，
畢竟這會一直用到!

# 編譯
 
cross-compiler的執行檔位在你解壓縮出來的資料夾裡面的`bin`資料夾，所以不管是要用assembler或是gcc，都要先進
到這個`bin`資料夾裡面，才能繼續操作。
![cd to bin](https://github.com/henrybear327/Tutorial/blob/cross-compiler-usage/Assembly/Cross-Compiler-Usage/Screenshot/new%20cd%20to%20bin.png)

呼叫assembler和gcc的方式都是一樣的，當你已經在bin資料夾時，你就直接打
```
./arm-elf-as 要編譯的檔案位置+檔名 -o 要輸出的檔案位置+檔名
./arm-elf-gcc 要編譯的檔案位置+檔名 -o 要輸出的檔案位置+檔名
```

所以說，假設我要用assembler編譯一個存在桌面上的檔案`hw1.s`，並且希望要編譯成`hw1.o`並且也存在桌面上，就打
```
./arm-elf-as ../../hw1.s -o ../../hw1.o
```
![compile](https://github.com/henrybear327/Tutorial/blob/cross-compiler-usage/Assembly/Cross-Compiler-Usage/Screenshot/compile.png)

`../`是代表回上一層目錄的意思。所以說，我原本是在`~/Desktop/con/bin`這個目錄裡，當你說`../../hw1.s`時，
電腦就會去現在目錄(也就是`bin`)的上兩個目錄的地方(也就是`Desktop`)找`hw1.s`。

你也可以偷懶(但是非常不建議這樣做)，直接把要編譯的檔案`hw1.s`放進bin資料夾，那就可以只打
```
./arm-elf-as hw1.s -o hw1.o
```

非常不建議這樣的原因: 雖然指令很短很easy，但是畢竟未來程式一多起來，你的bin資料夾會很亂，
所以強烈建議不要用這個偷懶法，而是要把你的原始碼放在別的地方，再用指定路徑的方式去找到他!

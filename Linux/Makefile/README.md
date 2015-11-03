# Makefile 教學

其實 makefile 不是什麼特別難學的東西，他基本上就是一種工具，可以讓你不用很煩的一直重複打編譯的指令。

# Makefile 檔案原始碼

如果你的檔名是 `main.c`，想要輸出的執行檔檔名是`main.o`，且要用 `gcc -std=c99 -Wall -Wextra main.c -o main.o` 編譯的話，
你就只要如同下面這樣，直接開一個檔案叫 `makefile`(不用類似`.txt`之類的副檔名)，並將下面的code貼進去即可。

```makefile
main: main.c
	gcc -std=c99 -Wall -Wextra -o main.o main.c
```

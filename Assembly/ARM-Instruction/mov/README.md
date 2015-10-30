# MOV

#### by: 陳丕祐

```MOV``` 在ARM中是一個可以簡單達到賦值的指令，使用的方法大致如下

```as
MOV r0 , #100
```

此行的效用等同於

```
r0 = 100;
```

需要注意的地方，賦值的值只有8個bit，所以可以用```MOV```賦值的區間僅有**0~255**。

# 延伸閱讀

[Invalid constant after fixup?](http://stackoverflow.com/questions/10261300/invalid-constant-after-fixup)

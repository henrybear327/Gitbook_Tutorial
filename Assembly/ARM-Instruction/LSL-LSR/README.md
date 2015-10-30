# LSL-LSR

#### by: 陳丕祐

 `LSL` 與 `LSR` 是兩種對 register 進行位元操作的指令

* LSL -> Logical Shift Left
* LSR -> Logical Shift Right

## 使用

首先要知道，每個register空間的容量都只有**32bits**，記住這件事對於撰寫程式中將會有所益處。

```arm
MOV r1 , r0 , LSL #5
```

要解讀這行程式碼需要從後面開始解讀。

```arm
r0 , LSL #5
```

這行程式是將整個r0向左平移5格，而**右邊多出來的部分會補上0**。

![LSL](http://i.imgur.com/08m0Liw.png)

```arm
MOV r1 , (r0 , LSL #5)
```

將被平移後的r0 `MOV` 給r1。

依此類推

```arm
MOV r1 , r0 , LSR #5
```

這行程式是將整個r0向右平移5格，而**左邊多出來的部分會補上0**。

將被平移後的r0 `MOV` 給r1。

![LSR](http://i.imgur.com/owef1iw.png)

# Conditional Execution | 陳丕祐

## Introduction
`Conditional Execution` 是基於 `ARM` 內建的 `Flags` 去使用多樣化的 `Branch` 以實現 `LOOP` 的效用。

```
建議先看完 branch 再來看， Conditional Execution。
```

## Usage

### flags

`Flags` 在 `ARM` 是由4個變數去實現的。

>* N - Negative
>
>   是否為負
>
>* Z - Zero
>
>   是否為零
>
>* C - Carry
>
>   Unsighed 溢位
>
>* V - Overflow
>
>   sighed 溢位

能影響 `Flag` 的指令不只一個，不過在這裡只介紹`CMP`。

```arm
CMP r0, r1 /*r0 - r1*/
```
`CMP` 實際上就是在內部執行 `r0-r1` 這個動作，並將其做為 **result** 給 `Flags` 做為其 **true or false** 的依據。

### More Branch

多說無益，看圖。

![branch](http://i.imgur.com/tUEipZd.png)

每個 `Branch` 會依照上表最後一個欄位所述，由 `Flag` 決定是否執行。

`CMP` 影響 `Flags` ， `Flags` 影響 `Branch`。

這就達成了 `Conditional Execution` 的基礎。

### Example

```c
for(int i=0; i<10; i++){
    sum+=i;
}
```

這是一段簡單用 `C` 寫成的LOOP。

將其改寫為 `ARM`

```arm
LOOP:
    ADD r1 ,r0
    ADD r0 ,#1
    CMP r0 ,#10
    BNE LOOP
```
********
```c
if (a > b)
    a++;
```
這是一段簡單用 `C` 寫成的 `if condition`。

改寫為 `ARM`

```arm
@if
    CMP r0,r1
    BMI FIN
    ADD r0 , #1
FIN:
    .end
```

## 參考資料

[Introduction to ARM: Conditional Execution](http://www.davespace.co.uk/arm/introduction-to-arm/conditional.html)

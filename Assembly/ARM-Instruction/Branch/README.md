# Branch | 陳丕祐

## Introduction

`Branch` 是在程式中增添一些跳躍以便其運行，可以使用它達成**迴圈**或者**條件判斷**的效果。

## Usage

```arm
LABEL:
    ... /*其他動作*/
    B LABEL
    ... /*其他動作*/
```
這份程式的涵意就是，當我們的程式執行到 `B LABEL` 時，他便會跳回到 `LABEL` 重新開始，就是從這個最基本的指令實現我們的**迴圈**與**條件判斷**。

在此其中， `LABEL` 不做任何的限制，可是任意取名，唯一要記得的事，
必須在名字的後面加上 `:` 以便 `assembler` 辨別。

## 延伸閱讀

[Introduction to ARM: Branch Instructions](http://www.davespace.co.uk/arm/introduction-to-arm/branch.html)

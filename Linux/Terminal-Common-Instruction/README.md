# 簡易terminal指令

## 指令總覽

- ```ls``` 顯示當前目錄下的檔案
- ```mkdir 資料夾的名稱``` 建立一個新的資料夾
- ```cd 路徑``` 移動到指定的路徑
- ```rm 檔案``` 移除檔案
- ```mv 原檔案/路徑 新檔案/路徑``` 檔案的移動與更名
- ```cp 原檔案/路徑 新檔案/路徑``` 複製檔案

### 圖文解說

```crtl+alt+t``` 啟動terminal

# 顯示當前目錄下的檔案

```
ls
```

![](http://i.imgur.com/jH2mXfw.png)

# 顯示隱藏的檔案
```
ls -a
```

![](http://i.imgur.com/ZAswBZz.png)

# 建立資料夾

```
mkdir 檔案名
```

在當前路徑下建立一個新的資料夾，用ls確認有沒有成功建立。

![](http://i.imgur.com/vQWmEH8.png)

# 移動到指定路徑

```
cd 路徑
``` 

冒號後面有告訴你當前路徑。

![](http://i.imgur.com/90BwrLF.png)

# 啟動文字編輯器
```
gedit 檔案名
```

gedit是內建於ubuntu相對於windows下記事本的存在，在這裡我們用於建立測試用的檔案。

![](http://i.imgur.com/IY95axG.png)

# 移動到上一層目錄

```sh
cd ..
```

![](http://i.imgur.com/2BxYhNP.png)

# 檔案的移動或更名

```sh
mv 原檔案路徑 新檔案路徑
```

更名 ```mv 原檔案名 新檔案名```

![](http://i.imgur.com/ao01Mqk.png)

移動```mv 檔案路徑 目錄路徑```可以不用打完整的路徑，預設的會是當前的目錄的路徑。
所以```mv 檔案名 目錄名```也通，不過前提是兩者皆在當前目錄下，或者可以 ```mv 檔案名 目錄路徑```，任意排列組合。

![](http://i.imgur.com/jcFUWHd.png)

移動後原檔案就消失了。

到資料夾裡面看看。

![](http://i.imgur.com/Ib0D57c.png)

# 移除檔案
```sh
rm 檔案
```

![](http://i.imgur.com/wNmPTZW.png)

使用```rm -r``` 移除資料夾

![](http://i.imgur.com/ppNjH8z.png)

# 複製檔案

```sh
cp 欲複製的檔案 新複製的檔案
```
![](http://i.imgur.com/kpjsFtl.png)


# 安裝linux

### 簡易流程
- 下載並安裝虛擬機
- 下載linux作業系統映象檔
- 使用虛擬機安裝linux

## 安裝虛擬機

虛擬機可以讓你省去許多在重灌或設定為雙作業系統的麻煩。在此以virtualbox作為範例。

- [virtualbox](https://www.virtualbox.org/) 開源，免費。

進入[下載](https://www.virtualbox.org/wiki/Downloads)頁面，依照你的作業系統選擇要下載的安裝檔，看不懂英文的話，找這一行```VirtualBox 5.0.2 for Windows hosts```，點選後面的```x86/amd64```即會開始下載。

![virtualbox](http://i.imgur.com/TQtoD9A.png)

安裝過程不多加說明，就一直點下一步，然後耐心等候。

## 下載linux映象檔

linux有很多種，有興趣的可以查一下[wiki](https://zh.wikipedia.org/wiki/Linux)或者看看[最近的排名](http://distrowatch.com/dwres.php?resource=popularity)，來選擇你要用哪一種，在這邊我們就用ubuntu做範例。

進入ubuntu的[下載頁面](http://www.ubuntu-tw.org/modules/tinyd0/)，選擇你需要的版本。

![ubuntu_download](http://i.imgur.com/0dawvPv.png)

## 使用virtualbox安裝linux

啟動方才安裝好的virtualbox，應該會看到下圖的，點選左上角的新增。

![interfrec](http://i.imgur.com/avUFYcH.png)

下面有很多設定可以依照需求更改，最後會在左手邊新增一個機器。

![](http://i.imgur.com/loxckk2.png)
![](http://i.imgur.com/u4fm9gY.png)
![](http://i.imgur.com/T55fAEK.png)
![](http://i.imgur.com/vwyJpLa.png)

將映象檔置入虛擬機

先點你剛設定好的機器，點選```設定值```->```存放裝置```，光碟小圖示中的光碟小圖示，```選擇虛擬光碟檔案```。
找到你剛剛下載的ubuntu映象檔，點選確定後點擊啟動(向右手邊的箭頭)。
![iso](http://i.imgur.com/vCadsSD.png)

安裝

虛擬機經過一陣文字後，會出現下圖，可選擇語言，試試看或直接安裝。

![](http://i.imgur.com/btCndnQ.png)

後續有許多設定不過基本上不重要，反正裝壞了，就依照上述步驟重新安裝。


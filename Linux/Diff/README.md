# Linux 下的 `diff` 使用教學

#### by: 曾俊宏

如果以後有類似資料結構的老鼠走迷宮作業，光一個答案檔就有數千行的output要和answer
比較時，不需要一個字一個字自己對到天荒地老，可以直接交給電腦幫你做這件事喔!

在進入正題之前，請先看一下[開檔讀檔教學](./../read_write_file/README.md)
的教學吧!


# `diff` 的使用方法

假設你的答案是在`answer.txt`的話，你可以用 `diff answer.txt output.txt` 來做比較。
(建議可以使用`-u`參數，這樣的比較結果比較淺顯易懂: `diff answer.txt output.txt -u`)

如果按下enter後什麼都沒顯示，代表說兩個檔案是一模一樣的! 如果有顯示任何東西，就代表
檔案有些地方不同，需要debug囉!

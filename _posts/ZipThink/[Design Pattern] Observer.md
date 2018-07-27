# 設計模式是一組答案

模式是為了解決問題而發展出來的一組答案，如同不可能的任務2 中提到的：*為了讓英雄貝雷風的存在有意義，我們創造出了怪獸凱梅拉。*


```
模式之所以能夠成為解決方案，是因為有了一個解待決的問題在那裡。
```

模式都是為解決某個特定問題而發展出來的，所以可以這麼說：[pattern 是一種整理知識的過程與結果，也是種解決問題的框架][PatternIs]

因此開始套設計模式之前，其實應該要先知道：

```
如何確認問題？
```

顯然這並不是設計模式要解決的問題，當然也就不是本文要討論的範圍，但還是建議可以參考一下[QBQ 這本書][QBQ]，這本書不厚，看完花不了太多時間，但其實書名就是整本書的核心「Question Behind the Question」（問題背後的問題）。

# 設計模式解決那些問題

Teddy 整理了 GoF 的三個分類，共 23 個模式要解決的問題：

* creational pattern : [上集][CP1]、[中集][CP2]、[下集][CP3]
* structural pattern : [上][SP1]
* behavioral pattern : [一][BP1]

# Observer
* Context

    某些商業邏輯的觸發源於不同的事件，以計算機為例子，如果顯示畫面為一個獨立模組，即時反應當前輸入結果，使用者透過點擊畫面輸入，顯示畫面模組的更新依賴於按鍵觸發。

* Problem：

    被動執行個體與狀態改變如何勾掛？

* Force
    * 兩者需要解耦，如此新增按鍵功能時，顯示畫面模組不用異動。

* Solution



[QBQ]:http://www.books.com.tw/products/0010776691 "QBQ 問題背後的問題"
[PatternIs]:http://designerica.cc/2015/06/a-pattern-is-a-thing-and-a-process/ "pattern是一種整理知識的過程與結果，也是種解決問題的框架"
[CP1]:http://teddy-chen-tw.blogspot.com/2012/10/creational-patterns.html "Creational Patterns要解決什麼問題(上)?"
[CP2]:http://teddy-chen-tw.blogspot.com/2012/11/creational-patterns.html "Creational Patterns要解決什麼問題(中)?"
[CP3]:http://teddy-chen-tw.blogspot.com/2012/11/creational-patterns_26.html "Creational Patterns要解決什麼問題(下)?"
[SP1]:http://teddy-chen-tw.blogspot.com/2012/11/structural-patterns.html "Structural Patterns要解決什麼問題(上)?"
[BP1]:http://teddy-chen-tw.blogspot.com/2013/03/behavioral-patterns.html "Behavioral Patterns要解決什麼問題(一)?"

[whatispattern1]:http://teddy-chen-tw.blogspot.com/2015/05/pattern-1pattern.html "什麼是 Pattern (1)"


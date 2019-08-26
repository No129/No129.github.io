---
layout: post
title: "透過 ClosedXML 設定 Excel 頁首"
categories: TechWeekly ClosedXML
tag: 
date: 2019-08-08 23:59:59 UTC+8 
last_modified_at: 2019-08-08 23:59:59 UTC+8 
---

# 引子
先前提供同仁一個工具，用於資料的匯入及整理、最後會將結果整理為表格輸出到 Excel 文件，因為以往跟 Excel 執行程式打交道的不好印象，所以那次採用了 [ClosedXML][ClosedXML] 這套框架與 Excel 文件互動。

聽說其他單位也有類似操作，因此想就這段期間使用的感想提出一些調整後，給更多單位的同仁使用。

# 需求
其中一個是在匯出的 Excel 報表中，因為項目名稱有時會很長，需要折行並且拉大行高才能完整顯示，但如此一來，原本插入資料的方式就有問題了，為什麼呢？

因為原本是在文件內動態插入表頭，然後在固定行數之後再插入另一個表頭，如此達成列印時每頁都有表頭的需要，同時可以滿足首頁表頭不同的需要，因此若是為了完整顯示內容而異動行高，就會造成列印結果的錯亂。

# 調整
在同事的提醒下，確認了 Excel 內建的表頭功能具備「首頁與其他頁不同」的設定，這樣如果改用 Excel 表頭，就可以避免程式要判斷頁次的需要，只要將表格內容填入即可，斷頁就交給 Excel 去決定。

# 設定
最重要的是 [ClosedXML][ClosedXML] 是有提供對應設定的，可以看[官方文件][HeadersAndFooters]說明，在實際測試過程中，有兩個小問題。

## 標楷體的字型設定
對於中文的字型設定不知道為什麼，直接給定「標楷體」是沒有作用的，不知道是不是跟作業系統的語系或是其他環境設定有關，但是透過 [維基百科][wiki] 提到的英文名稱「DFKai-SB」就可以設定，有需要的可以這樣試試。

## 8 針的字型大小設定
對於字型大小的設定不知道為什麼就 8 這個大小會無法正常反應，而且因為原來的表頭文字大小就是 8 針，所以一開始還以為字型大小的設定不正常，來來回回測試才發現其他大小都可以正常反應，有成功也希望回饋給我，謝謝。


[ClosedXML]:https://github.com/ClosedXML/ClosedXML "ClosedXML"
[HeadersAndFooters]:https://github.com/ClosedXML/ClosedXML/wiki/Headers-and-Footers-Tab "Headers And Footers"
[wiki]:https://zh.wikipedia.org/wiki/%E6%A8%99%E6%A5%B7%E9%AB%94 "Wiki:標楷體"
---
layout: post
title: "透過 ClosedXML 設定 Excel 頁首"
categories: TechWeekly ClosedXML
tag: 
date: 2019-08-08 23:59:59 UTC+8 
last_modified_at: 2019-08-08 23:59:59 UTC+8 
---
先前一個工具提供資料整理功能，最後會將結果整理為表格輸出到 Excel 文件，採用 [ClosedXML][ClosedXML] 這套框架與 Excel 文件互動。

近來工具要改版，因為項目名稱有時會很長，需要折行並且拉大行高才能完整顯示，但如此一來，原本插入資料的方式就有問題了。

原本是在文件內插入表頭，然後在固定數量的行之後再插入另一個表頭，如此達成列印時每頁都有表頭的需要，因此若是為了完整顯示內容而異動行高，就會造成列印結果的錯亂。

因此改用 Excel 內建的表頭設定功能，並設定首頁與其他頁不同，這樣就不用自行判斷多少行為一頁的問題，而是交由 Excel 列印決定。

而最重要的是 [ClosedXML][ClosedXML] 是有提供對應設定的，可以看[官方文件][HeadersAndFooters]說明。


[ClosedXML]:https://github.com/ClosedXML/ClosedXML "ClosedXML"
[HeadersAndFooters]:https://github.com/ClosedXML/ClosedXML/wiki/Headers-and-Footers-Tab "Headers And Footers"
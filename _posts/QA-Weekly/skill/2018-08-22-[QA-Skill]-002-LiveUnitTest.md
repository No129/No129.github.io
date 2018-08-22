---
layout: post
title: "即時反應測試覆蓋情形與執行結果 - Live Unit Testing"
categories: QA-Skill
tag: 
date: 2018-08-22 23:59:59 UTC+8 
last_modified_at: 2018-08-22 23:59:59 UTC+8 
---

# 前言

話說單元測試會有一項 Code Coverage ( [代碼覆蓋率](https://zh.wikipedia.org/wiki/%E4%BB%A3%E7%A2%BC%E8%A6%86%E8%93%8B%E7%8E%87)) 的參數，提供確認程式碼被測的百分比，但是不容易知道那些是尚未被測試碼覆蓋的產品碼 ( 除非是足以[摧毀新專案的 100% 的覆蓋率](https://www.puritys.me/docs-blog/article-230-%E9%81%8E%E9%AB%98%E7%9A%84-Test-Code-Coverage-%E5%B0%87%E6%91%A7%E6%AF%80%E4%B8%80%E5%80%8B%E6%96%B0%E5%B0%88%E6%A1%88.html) ) 。

現在，地表最強的 IDE 沒有之一的 Visual Studio 2017 提供 **Live Unit Testing** 功能 ( [Enterprise](https://visualstudio.microsoft.com/zh-hant/vs/?rr=https%3A%2F%2Fdevmanna.blogspot.com%2F2017%2F03%2Fvs2017-live-unit-testing.html) 版本才有 )，讓你的單元測試與產品碼的互動更緊密，可以即時知道程式碼的覆蓋情形及測試結果。

# 啟用 **Live Unit Testing** 功能

啟用 **Live Unit Testing** 功能只要在 ***Function Bar/Test/Live Unit Testing/Start*** 就可以。

![LiveUnitTesting](/assets/2018-08-22/LiveUnitTesting.gif)

# 啟用後的不同

切換到產品碼，可以看到左邊區塊增加了提示圖案：
- 紅色的叉：測試失敗
- 綠色的勾：測試通過
- 藍色的棒：尚未有對應測試碼

因為 **Live Unit Testing** 執行需要時間，所以短暫的會在原有的圖示右下附上圓形計時器圖案。

![LiveUnitTestingIconWaiting](/assets/2018-08-22/LiveUnitTestingIcon.png)

# 舊測試如何支援新功能

原本**Live Unit Testing** 功能僅支援「MSTest V2」規格的測試專案，但自 15.4 版本後也支援「MSTest V1」版本的測試專案，所以最簡單的方式就是昇級你的 Visual Studio 2017 版本。

# 參考

* [[Nero's blog] - Live Unit Testing](http://erdao123.oschina.io/nero/2017/11/12/UnitTest/Live-Unit-Testing/)
* [[MSDN] = Live Unit Testing 的使用者入門](https://docs.microsoft.com/zh-tw/visualstudio/test/live-unit-testing-start?tabs=csharp)
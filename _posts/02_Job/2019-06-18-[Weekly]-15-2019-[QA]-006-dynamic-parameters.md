---
layout: post
title: "透過 Visual Studio 建立效能及負載測試：動態變數"
categories: Job QA QA-Skill TechWeekly Stress-Test
tag: 
date: 2019-06-18 23:59:59 UTC+8 
last_modified_at: 2019-06-18 23:59:59 UTC+8 
---

# 情境
有些受測頁面使用動態參數來處理部分要求，例如授權，在受保護的頁面會要求使用者登入後才能操作，採用黑箱測試的情形下，也就不能透過給定一組固定的授權碼，而必須在執行階段才能取得，如此一來待測頁面的授權碼就必須採用動態變數方式處理。

# 說明
可以參考[這篇官方說明][msdoc:dynamic]，但主要的關鍵在以下兩個步驟。
## 設定動態變數
建立效能測試完畢後執行，在登入頁面的「回應索引」頁面，選取動態變數，然後透過滑鼠左鍵清單的「Add Extraction Rule」功能，建立萃取條件，建立完畢後，會在該呼叫下看到看到「Extraction Rules」的項目。

這裡請參考官方說明的[執行測試找出未偵測到的動態參數][msdoc:dynamic-1]一節的第 7 點說明，執行測試後，在執行結果中選取動態變數提供的呼叫，從「Response」中的頁面內容，透過滑鼠選取動態變數的來源字串，然後將它加為擷取規則。

## 使用動態變數
在[官方說明][msdoc:dynamic-1]中是採用 Find and Replace 的方式，將原先的動態變數字串，替換為雙層大括號的參數字串。

另外，若是套用到「Query String Parameters」中，新增一個參數，然後在 Value 中則可以下拉選單就可以繫結到前面建立的動態變數了

# 結語
這是一個手動將前一呼叫回傳值，傳給後面呼叫的解法，可以參考[這篇官方說明][msdoc:dynamic]因為一直相信在不同呼叫間傳遞參數應該是可以做到的設定，但官方說明我看了兩天才發現原來動態變數的設定這麼變態的簡單，江湖一點訣，說破不值錢。



[msdoc:dynamic]:https://docs.microsoft.com/zh-tw/visualstudio/test/fix-non-detectable-dynamic-parameters-in-a-web-performance-test?view=vs-2017 "在 Web 效能測試中修正無法偵測的動態參數"
[msdoc:dynamic-1]:https://docs.microsoft.com/zh-tw/visualstudio/test/fix-non-detectable-dynamic-parameters-in-a-web-performance-test?view=vs-2019#run-the-test-to-isolate-the-non-detected-dynamic-parameter "執行測試找出未偵測到的動態參數"
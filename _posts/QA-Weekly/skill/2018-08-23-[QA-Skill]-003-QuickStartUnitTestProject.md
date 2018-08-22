---
layout: post
title: "從既有程式建立單元測試專案"
categories: QA-Skill
tag: 
date: 2018-08-23 23:59:59 UTC+8 
last_modified_at: 2018-08-23 23:59:59 UTC+8 
---

# 前言

千里之行始於足下，如何踏出單元測試的第一步，是很多尚未開始的工程師的第一個疑問，通常會類似開發產品碼一般，新增專案、類別然後函式，但是地表最強 IDE 的 Visual Studio 其實提供從既有程式建立對應測試的功能。

# 從既有程式建立單元測試

滑鼠右鍵，點擊「**Create Unit Tests**」項目，就會跳出建立精靈，逐項填寫後安下確認，就會在同一方案 ( Sulotion ) 下建立測試專案，並且連對應的單元測試類別都建好。

![Create Unit Tests](/assets/2018-08-23/CreateByVisualStudio.gif)

- Test Framework: 測試專案所採用的測試框架，在 vs2017 中，預設提供：
    - MSTest 
    - MSTestv2

- Test Project: 選擇測試專案，下拉選單會列出目前方案中已存在的測試專案供選擇，若要新增測專案就選取 **\<New Test Project\>** 項目，就會在當前方案建立新的測試專案。

- Name Formate for Test Project: 若是前一項 ( Test Project ) 採用新增測試專案方式，則會需要提供測試專案的名稱，預設提供待測專案的名稱空間 ( Namespace ) 加上自訂文字，當然也可以完全自訂；若已選擇特定專案則此欄就會反灰無法填寫。

- Namespace: 測試類別的名稱空間。

- Output File: 測試函式的檔案，會列出 **Test Project** 目前的測試類別檔案，並且可以選擇新增檔案( **\<New Test File>** )，若是 **Test Project** 為新增專案，則此項則僅提供新增檔案的項目。

- Name Formate for Test Class: 測試類別的名稱，此項目會參考前面的 **Namespace** 及 **Output File** 的設定，若在同一檔案中具備相同名稱空間的同名類別則不會額外新增，若是指定已存在檔案中尚未包含指定的名稱空間，則會先建立對應的名稱空間段落，再在該段落內建立類別。

- Name Formate for Test Method: 測試函式名稱，則在相同檔案且相同名稱空間的同名類別中有同名函式，則會加上序號。

- Code for Test Method: 提供測試函試的預設內容，包含三種不同型態：
    
    - Empty Body: 空函式，若未進一步處理會是**綠燈**。
    - Throw NotImplementedException: 擲出 **NotImplementedException** 例外，若未進一步處理會是紅燈。
    - Assert failure: 斷言失敗，若未進一步處理會是紅燈。
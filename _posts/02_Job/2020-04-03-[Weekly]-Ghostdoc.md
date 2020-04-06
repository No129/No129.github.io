---
layout: post
title: "GhostDoc-將寫註解半自動化的 Visual Studio 延伸模組"
categories: VisualStudio
tag: 
date: 2020-04-03 22:23:51 UTC+8 
last_modified_at: 2020-04-03 22:23:51 UTC+8 
---
# 楔子
作為程式開發人員，撰寫程式註解可以說是程序人員必須做，但又最不想做的事，沒有之一。   

程式的註解可以手工打字撰寫，部分固定的片段則可以透過程式碼片段 ( Code Snippet ) 預先建立好，再透過快捷字串產出，而這次要介紹的 Visual Studio 的 Extension ( 延伸模組 ) [GhostDoc Community for VS2017 and Later][ghost] 則是可以透過依據條件，在 Visual Stidio [插入 XML 註解][vs#1]時加上自訂的註解內容。

# 安裝
* 取得延伸組件  
    開啟 Visual Studio 2017/2019 的 ***[延伸模組]-->[管理延伸組]*** 切換到 ***[線上]*** 項目，再透過搜尋「GhostDoc」關鍵字，執行下載。
    ![取得延伸組件](/assets/20200403/P1-GetExtension.png)
    
* 安裝延伸組件  
    關閉 Visual Studio 2017/2019 後，會自動啟動安裝對話視窗，同意更動系統後，就會啟動 VSIX Installer 的安裝視窗，同意之後就會進行安裝。  
    ![VSIX](/assets/20200403/P2-VSIX.png)  
    ![VSIX](/assets/20200403/P2-VSIX_1.png)  
    ![VSIX](/assets/20200403/P2-VSIX_2.png)  

# 設定
完成安裝後重新開啟 Visual Studio 2017/2019 後，在 ***[工具]*** 頁籤下會新增一個 ***[GhostDoc]*** 項目，可以透過 ***[工具]->[GhostDoc]-->[Options]*** 開啟設定對話視窗。
![GhostDoc-Options](/assets/20200403/P3-Options.png)



切換到 ***[Rules]*** 項目下可以就不同的程式段落進行註解設定。
![GhostDoc-Options](/assets/20200403/P3-Options_1.png)


[ghost]:https://marketplace.visualstudio.com/items?itemName=sergeb.GhostDoc
[vs#1]:https://docs.microsoft.com/zh-tw/visualstudio/ide/reference/generate-xml-documentation-comments?view=vs-2019
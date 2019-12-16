---
layout: post
title: "在 Visual Studio 中 SandCastle 的 Intellisense 功能失效"
categories: Job SandCastle
tag: 
date: 2019-08-07 23:59:59 UTC+8 
last_modified_at: 2019-08-07 23:59:59 UTC+8 
---
撰寫 [SandCastle][SHFB] 時若缺少了 Intellisense 的提示功能，那寫起來會很卡，當然熟記各個節點的屬性的高手例外。

這篇文章是因為有一陣子沒有透過 Visual Studio 2017 撰寫 SandCastle 文件，驚覺以往有的提示功能失效了，上網查找到[這篇文章][Visual Studio IntelliSense]提到，應該是因為路徑的關係，所以要自己手動設定 Visual Studio 2017 的路徑檔。

按圖施工後果然就功能就回來了，因為每次 Visual Studio 更新可能更新這個設定檔，所以可能更新後都需要再執行一次，所以就記下來，免得以後要再花時間找文章。

[SHFB]:https://github.com/EWSoftware/SHFB "SandCastle"
[Visual Studio IntelliSense]:http://ewsoftware.github.io/MAMLGuide/html/746fc19e-2670-440b-8277-a1ef7dc074d5.htm "Visual Studio IntelliSense"
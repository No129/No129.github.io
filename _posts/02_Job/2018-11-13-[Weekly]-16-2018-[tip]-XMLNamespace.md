---
layout: post
title: "[XML]建立具備名稱空間前置詞的 XML 節點"
categories: Job tip
tag: 
date: 2018-11-13 00:00:00 UTC+8 
last_modified_at: 2018-11-13 00:00:00 UTC+8 
---

# 前言

最近工作上需要建立具備名稱空間的 XML 文件。

以往對於名稱空間不熟悉，都是以文字方式硬串，沒辦法，因為對 XML 的格式不熟，不過總不是辦法，畢竟這樣的程式太難以理解，而且...，想不到什麼理由，反正就很難看。

所以，這次要調整對應功能時，決定要採用標準的 XML 定義方式進行撰寫，因此就找了資料，發現其實都有還滿容易操作的，但還是整理一下。

# [Add new Namespace](https://www.codeproject.com/Questions/161436/C-XML-add-a-new-Namespace)

預期結果，有一個根節點 OrderPush 包含名稱空間 bml 的定義是「http://netlab.gmu.edu/IBML」的路徑，其子節點都有前置詞 bml 說明此節點歸屬於 bml 名稱空間設定。

```xml
<OrderPush     
    xmlns:bml="http://www.pwctw.com">        
    <bml:Task />
</OrderPush>
```

## 步驟一、建立根節點的名稱空間資訊

```csharp
var objOrderPush = 
    new XElement("OrderPush", 
        new XAttribute(XNamespace.Xmlns + "bml", @"http://www.pwctw.com" ));

```


## 歩驟二、加入名稱空間前置的子節點

```csharp
XNamespace ns = "http://www.pwctw.com";  //重要：不是「bml」而是要與根節點的內容一致
var objTask = new XElement(ns + "Task");

objOrderPush.Add(objTask);
```

這樣就可以建立具備對應名稱空間的 XML 節點了。

---
layout: post
title: "部落格的建立 ( 零 )"
categories: TECH
tag: 
date: 2018-04-08 22:23:51 UTC+8 
last_modified_at: 2018-04-08 22:23:51 UTC+8 
---
# 本地建構 Jekyll 環境

[windows 安裝 Jekyll](http://www.195440.com/?p=782)

[githup-page](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)

[安裝 Jekyll](http://jekyllcn.com/docs/installation/)

##  在 Windows 環境
[Run jekyll on Windows](http://jekyllcn.com/docs/windows/#installation)




## 安裝 Jekyll 
發生 https 錯誤時，改用 http 
```
gem source -a http://rubygems.org/
gem install jekyll
```

# 為什麼採用 gitpage + jekyll + vscode 這樣的組合？

## 免費並且使用的人數眾多
因為免費所以沒有費用的問題，使用的人數很多，所以有問題或有想要的大概都有文章可以參考。

## 可以同時學習並練習：
1. 使用 markdown 語法寫文章
2. 前端開發的 html, css, javascript 

abc
``` csharp
namespace PwCTW{
    class Employee{
        ///姓名
        string name{get;set;}
    }
}
```
# 動態建立文章目錄

可以動態提供文章目錄
[javascript + jQuery](https://github.com/ghiculescu/jekyll-table-of-contents/blob/master/toc.js "jekyll-table-of-contents")
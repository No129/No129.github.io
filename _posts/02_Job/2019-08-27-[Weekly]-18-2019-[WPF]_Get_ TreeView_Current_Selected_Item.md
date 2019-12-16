---
layout: post
title: "[WPF] 取得 TreeView 控制項目前選取項目"
categories: Job TechWeekly WPF
tag: 
date: 2019-08-27 23:59:59 UTC+8 
last_modified_at: 2019-08-27 23:59:59 UTC+8 
---
# 前言
在 WPF 使用者介面中採用 [TreeView][TreeViewInMSDN] 控制項是相當常見的情形，然而同時在 WPF 中採用 MVVM 模式時，如何取得 [TreeView][TreeViewInMSDN] 這個控制項目前的選取項目則有一些困難。

因為 [TreeView][TreeViewInMSDN] 這個控制並沒有類似 [Tab][TabInMSDN] 控制項有 SelectedIndex 或是 [DataGrid][DataGridInMSDN] 控制項有 SelectedItem 這樣的屬性可供繫結，以取得目前選取項目的索引值或項目本身的繫結資料，然而沒有辦法透過繫結引擎連結 View 與 Model 就難以處理 MVVM 模式。

# 方案
以往是透過 Behind Code 透過 [TreeView][TreeViewInMSDN] 物件的 SelectedItem 屬性，完善 MVVM 的 Model 實體屬性，但這樣的方式需要在流程上，自行撰寫控制項屬性與 Model 屬性的對應。

這樣的處理方式往往也都僅只於單方向的 View 到 Model 的對應，對於修改 Model 反應回 View 的處理則不好處理，此外，這樣的處理模式對於「MVVM 的 View 與 Model 是透過繫結引擎串起」這樣的原則也是一種例外，而對於例外總是覺得不舒服。

然而，最近又用到 [TreeView][TreeViewInMSDN] 這個控制項，不意外的需要選取的項目資訊，於是再 Google 看看其他人如何在 MVVM 模式下取得 [TreeView][TreeViewInMSDN] 選取的項目資訊，結果就在 stackoverflow 上看到了[這篇文章][TreeView]。

透過 **Style** 設定 **TreeViewItem** 的 **IsSelected** 屬性繫結到資料項，這樣就可以在 ViewModel 中透過 linq 對資料篩選，取得目前的資料項，同時也可以透過不同資料項的屬性設定，反向的更新畫面目前的選取項目。

[DataGridInMSDN]:https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.datagrid?view=netframework-4.8 "DataGrid"

[TreeViewInMSDN]:https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.treeview?view=netframework-4.8 "TreeView"

[TabInMSDN]:https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.tabcontrol?view=netframework-4.8 "Tab"

[TreeView]:https://stackoverflow.com/questions/7153813/wpf-mvvm-treeview-selecteditem "WPF MVVM TreeView SelectedItem"
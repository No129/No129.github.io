---
layout: post
title: "Visual Studio Template (一) - 透過匯出精靈建立自訂範本"
categories: Job QA
tag: 
date: 2019-12-17 23:59:59 UTC+8 
last_modified_at: 2019-12-17 23:59:59 UTC+8 
---

# Visual Sudio 範本的種類
在 Visual Studio 中有兩種範本，分別為：
* 專案範本( Project Template)
* 項目範本( Item Template )  

所謂**專案範本**是指新增專案時，列示的那些選項，例如新開一個 MVC 專案時，你會去選擇對應的專案範本，而不會新增一個空專案再手動新增必要的關連、參照及檔案夾等等的操作。
![Add New Project](/assets/VS-Template/AddNewProject.png)

而**項目範本**則是新增項目時，列示的選項，例如新增一個 WPF Window 時，直接選擇對應的項目，會自動建立對應的 XAML 及 behind code 的檔案，同時建好對應的關連。
![Add New Item](/assets/VS-Template/AddNewItem.png)

# 專案範本
專案範本如上所述，旨在提供組織對新專案初始時因應組織所需，在新增之初就必需進行的設定及新增程序，將其預先完備後以範本型態提供使用，可有效減少組織在新增專案的重覆工時及人員的學習與缺漏的成本。

## 專案範本匯出
最簡單產生**專案範本**的方式是透過匯出精靈，直接將手頭的專案匯出。先將組織中對新增專案的初始步驟都先處理完畢，例如參照、nuget 安裝、檔案夾及檔案等。  
接下來就可以透過 [**Project->Export Template**] 操作呼叫出匯出精靈對話視窗。(Visual Stuido 2017)  

![Add New Item](/assets/VS-Template/Project_ExportTemplate.png)


* 步驟一：選擇 **Project template**  
匯出精靈首先要決定匯出的範本型別，在此選擇 **Project Template** 選項，並從下拉選單選擇要匯出的專案範本，這個清單會自動將目前 **方案( Solution )** 所包含的專案都列示出來，但匯出功能僅能匯出個別專案作為範本。
![Chose Template Type](/assets/VS-Template/Wizard_ChoseTemplateType.png)

* 步驟二：填寫範本參數  
接著會需要填寫範本的相關參數，接著按下 **Finish** 按鍵就完成匯出程序，得到一個專案範本。
![Select Template Options](/assets/VS-Template/Wizard_SelectTemplateOptions.png)  
其中 **Template Name** 、 **Template description** 及 **Icon Image** 三項對應新增專案的畫面資訊，而不可修改的 **Output localtion** 則是輸出路徑，可以看到輸出的檔案格式是副檔名為 **.zip** 的壓縮檔。
![Select Template Options Mppping New Project Dialog](/assets/VS-Template/Wizard_SelectTemplateOptionsMapNewProject.png)
兩個勾選項目則分別是：
    * Automatically import the template into Visual Studio  
輸出後自動套用為目前的 Visual Studio 的範本。這裡建議先不要勾選，透過後面說明的方式手動套用，在範本管理上比較方便。
    * Display an explorer window on the output files folder  
輸出後開啟檔案總管檢視輸出目錄。  

## 專案範本的使用  
前面的說明中可以看到匯出的範本是一個壓縮檔，套用範本的方式也相當單純，就是放到 Visual Studio 預設的路徑下，然後 Visual Studio 在開啟時就會自行到該路徑下將解讀該壓縮檔。  
所以說，那個路徑在那裡呢？可以區分為兩個不同層級，分述如下：
* 應用層級
* 使用者層級
### 應用層級
依[這篇說明](https://docs.microsoft.com/en-us/visualstudio/ide/how-to-locate-and-organize-project-and-item-templates?view=vs-2019)可以安裝到在以下路徑，再依據程式語言及文化語系放置，但沒有實際成功就是：  

    C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\ProjectTemplates


### 使用者層級
使用自訂範本則可以放在以下路徑，我在 Visual Studio 2017 中，放上去後就可以在 Visual Studio 2017 中選到自訂的範本，同時可以透過檔案夾來建立新增畫面的分類：  

    C:\Users\[User Name]\Documents\Visual Studio 2017\Templates\ProjectTemplates
# 項目範本
項目範本提供使用者一組定義的類別組合，省去特定角色的設定與新增程序，例如新增一個 WPF 的 **Window** 角色時，會同時新增 **.xaml** 及 **.cs**( 或 **.vb**) 兩個檔案，同時會將建立兩個檔案的關連，對於自訂類別( 例如套用自訂框架時，會固定繼承或實做 )的設定，避免了缺漏的可能，也減少了輸入的時間。

## 項目範本的匯出
**項目範本**也可以透過匯出精靈，直接將手頭的專案的類別匯出。先建立待匯出的類別內容，接下來就可以透過 [**Project->Export Template**] 操作呼叫出匯出精靈對話視窗。(Visual Stuido 2017)  
* 步驟一：選擇 **Item template**  
匯出精靈首先要決定匯出的範本型別，在此選擇 **Item template** 選項，並從下拉選單選擇要匯出的專案範本，這個清單會自動將目前 **方案( Solution )** 所包含的專案都列示出來，但匯出功能僅能匯出個別專案作為範本。
![Chose Template Type](/assets/VS-Template/Wizard_ChoseTemplateTypeItemTemplate.png)

* 步驟二：選擇要匯出的檔案  
這裡會提供所選擇的專案下所有的類別檔案，你可以從中選取要作為新增項目的檔案，但僅能選一個，且不能選檔案夾。
![Select Item To Export](/assets/VS-Template/Wizard_SelectItemToExport.png)

* 步驟三：選擇參照的函式庫
這裡要決意的是，範本並不會打包此處的參照函式庫，它會在使用時在專案加入對應的參照，所以若是使用範本的專案所在的對應路徑缺少對應的參照組件，使用上可能會有問題。
![Chose Item Reference](/assets/VS-Template/Wizard_SelectItemReferences.png)

* 步驟四：填寫範本參數  
接著會需要填寫範本的相關參數，接著按下 **Finish** 按鍵就完成匯出程序，得到一個專案範本。
![Select Template Options](/assets/VS-Template/Wizard_SelectTemplateOptions.png)  
其中 **Template Name** 、 **Template description** 及 **Icon Image** 三項對應新增專案的畫面資訊，而不可修改的 **Output localtion** 則是輸出路徑，可以看到輸出的檔案格式是副檔名為 **.zip** 的壓縮檔。
![Select Template Options Mppping New Project Dialog](/assets/VS-Template/Wizard_SelectTemplateOptionsMapNewItem.png)
兩個勾選項目則分別是：
    * Automatically import the template into Visual Studio  
輸出後自動套用為目前的 Visual Studio 的範本。這裡建議先不要勾選，透過後面說明的方式手動套用，在範本管理上比較方便。
    * Display an explorer window on the output files folder  
輸出後開啟檔案總管檢視輸出目錄。  

## 項目範本的使用
前面的說明中可以看到匯出的範本是一個壓縮檔，套用範本的方式也相當單純，就是放到 Visual Studio 預設的路徑下，然後 Visual Studio 在開啟時就會自行到該路徑下將解讀該壓縮檔。  
所以說，那個路徑在那裡呢？可以區分為兩個不同層級，分述如下：
* 應用層級
* 使用者層級
### 應用層級
依[這篇說明](https://docs.microsoft.com/en-us/visualstudio/ide/how-to-locate-and-organize-project-and-item-templates?view=vs-2019)可以安裝到在以下路徑，再依據程式語言及文化語系放置，但沒有實際成功就是：  

    C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\ItemTemplates


### 使用者層級
使用自訂範本則可以放在以下路徑，我在 Visual Studio 2017 中，放上去後就可以在 Visual Studio 2017 中選到自訂的範本，同時可以透過檔案夾來建立新增畫面的分類：  

    C:\Users\[User Name]\Documents\Visual Studio 2017\Templates\ItemTemplates

# 參考文章
* [MSDN:Project and item template](https://docs.microsoft.com/en-us/visualstudio/ide/creating-project-and-item-templates?view=vs-2017)
* [MSDN:How to:Create item templates](https://docs.microsoft.com/en-us/visualstudio/ide/how-to-create-item-templates?view=vs-2017)
* [Alan Tsai 的學習筆記:[打造自己的 template-建立一致性程式碼[03]透過匯出建立Project Template]](https://blog.alantsai.net/posts/2017/08/buildyourowntemplate-create-vs-template-using-export)
* [Alan Tsai 的學習筆記:[打造自己的 template-建立一致性程式碼[06]建立Item Template]](https://blog.alantsai.net/posts/2017/08/buildyourowntemplate-create-item-template)
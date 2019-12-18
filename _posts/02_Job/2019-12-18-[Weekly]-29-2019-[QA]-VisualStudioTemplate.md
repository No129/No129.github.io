---
layout: post
title: "Visual Studio Template (二) - 範本設定檔簡單介紹"
categories: Job QA
tag: 
date: 2019-12-18 23:59:59 UTC+8 
last_modified_at: 2019-12-18 23:59:59 UTC+8 
---

# 解讀範本檔
對於 Visual Studio 匯出的範本檔( 包含專案範本及項目範本，以下皆同 )的檔案格式為 **.zip** 的壓縮檔，如果將其解壓縮，會發現資料夾內容與一般專案類似，但明顯多了 **.vstemplate** 的範本設定檔。  

# .vstemplate 檔案
**.vstemplate** 提供了範本的相關資訊為一個 **XML** 檔案，以 **VSTemplate** 為根節點。

## VSTemplate
開啟匯出的範本設定檔，會包含兩個特性值及必要節點：
* Version: 版本別。
* Type: 範本型態，若是**專案範本**就會以 **Project** 填入，若是**項目範本**就會以 **Item** 填入。


必要節點：
* TemplateData: 包含範本資訊。
* TemplateContent: 定義有那些檔案要包含在這個範本。

### TemplateData 節點
本節點透過以下子節點表達範本的各項基本資料。
* 必要節點：
    * Name：範本名稱，新增視窗的範本名稱。
    * Description：範本描述，新增視窗的右邊的說明資訊。
    * Icon：範本圖標，新增視窗的範本圖標。
    * ProjectType：範本歸屬於那個分類項下。
* 自選節點：
    * defaultName：新增視窗提供的預設專案名稱。
    * 自選節點：NumberOfParentCategoriesToRollUp|自訂可顯示此範本的母項層數，方便自訂範本可以顯示在較上層的項目清單。

更多參數可以參考[MSDN: TemplateData element (Visual Studio Templates)](https://docs.microsoft.com/en-us/visualstudio/extensibility/templatedata-element-visual-studio-templates?view=vs-2017)

### TemplateContent 節點
透過 **Project** 子節點，說明專案的各項資訊。 

更多參數可以參考[MSDN: TemplateContent Element](https://docs.microsoft.com/en-us/visualstudio/extensibility/templatecontent-element-visual-studio-templates?view=vs-2017) 
#### Project
**Project** 節點包含 **TargetFileName** 、 **File** 及 **ReplaceParameters** 三個特性值，會將 **TargetFileName** 指定的名稱以參數替換後，套在以 **File** 指定檔案所拷貝的檔案。而其包含的子節點則用來說明專案所包含的檔案及目錄資訊。
* ProjectItem：專案檔案，包含 **ReplaceParameters** 及 **TargetFileName** 兩個特性值，其 **Value** 對應實際的檔案名稱。
* 自選節點：Folder|專案目錄，包含 **Name** 及 **TargetFolderName** 兩個特性值，並且可以再透過子節點表達放在此目錄下的檔案及目錄。

更多參數可以參考[MSDN: Project Element](https://docs.microsoft.com/en-us/visualstudio/extensibility/project-element-visual-studio-templates?view=vs-2017)

# CS 檔案被調整的內容-Paraemter
開啟一個範本裡的 **.cs** 檔案，它原本是透過新增 **Class** 產生的 **.cs** 檔，沒有做任何額外處理，然而在匯出為範本時，有被進行一些調整，可以看到 **$safeprojectname$** 取代了原本的 **namespace** 內容。  
還記得在 **ProjectItem** 中有一個 **ReplaceParameters** 的特性值，是用來指定該檔案的內容是進行參數替換，而 **$safeprojectname$** 則會將該字串在新增時替換為你新增的專案名稱。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace $safeprojectname$
{
    public class Class1
    {
    }
}
```
更多替換參數可以參考 [MSDN: Template parameters](https://docs.microsoft.com/en-us/visualstudio/ide/template-parameters?view=vs-2019) 說明。

# 結語
透過 Visual Studio 的匯出功能可以方便的建立範本，但僅能建立較為單純的範本，若要更靈活的範本，例如複數專案範本，就要手動進行參數調整才能處理。

# 參考文章
* [MSDN: VSTemplate element (Visual Studio)](https://docs.microsoft.com/en-us/visualstudio/extensibility/vstemplate-element-visual-studio-templates?view=vs-2017)
* [Alan Tsai 的學習筆記:[打造自己的 template-建立一致性程式碼[04]了解 vstemplate 來微調匯出的 Template 和強制 VS 更新 Template 的方式]](https://blog.alantsai.net/posts/2017/08/buildyourowntemplate-understand-vstemplate-make-vs-refresh-template-cache)

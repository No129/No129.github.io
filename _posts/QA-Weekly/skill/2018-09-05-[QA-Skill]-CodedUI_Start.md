---
layout: post
title: "[Coded UI]-快速開始 Coded UI 錄製使用者操作"
categories: QA-Skill
tag: 
date: 2018-09-05 23:59:59 UTC+8 
last_modified_at: 2018-09-05 23:59:59 UTC+8 
---

# 前言
 
  要執行端到端的測試，就是要模擬使用者真實操作，透過圖形化介面的真槍實彈的驗證，這次介紹 Visual Studio 2017 Enterprise/Ultimate 提供的 Coded UI 測試專案，可以快速且直覺的錄製使用者操作，並將其應用於測試。  

# 確認開發工具

 確認使用的 Visual Studo 2017 版本，因為 Coded UI 的專案形態是僅提供給 Visual Studio 2017 Enterprise / Ultimate 版本的功能。

 此外，在安裝時需要額外勾選個別安裝套件，這樣才會提供 Coded UI 的專形態在專案清單中，可參考下圖：

 ![Coded-UI-Test-Component](/assets/2018-09-05/coded-ui-test-component.png)

# 準備動作

## 建立待測專案

 新增一個待測的目標專案，因為測試的目標是使用者介面，所以採用「WPF App(.NET Framework)」專案形態，並取名為 DEMO_SUT 表示是待測系統範例。

 在預設的 MainWindow 中新增 Taxtbox 及 Button 控制項，如下圖所示。

 ![MainWindow](/assets/2018-09-05/Edit_MainWindow.jpg)

## 新增測試專案
 
 新增一個對應的測試專案，因為要採用 Coded UI 方式，所以採用「Coded UI Test Project」專案形態，你應該可以在語言別 ( Visual c# / Visual Basic ) 下的「Test」項下看到，如下圖所示。

 ![CreateCodedUIProject](/assets/2018-09-05/Create_CodedUIProject.jpg)

 新增完畢後會先直接詢問是否要錄製操作，如下圖，這個步驟先取消。
 
 ![GenerateCodeForCodedUITest](/assets/2018-09-05/Win_GenerateCodeForCodedUITest.jpg)
 
 
# 錄製操作

 1. 執行待測試專案編譯出的執行檔。
 2. 新增「Coded UI Map」檔案，可參考下圖。
    
    ![AddCodedUIMap](/assets/2018-09-05/Add_NewItemOfCodedUITestMap.jpg)

 3. 點擊新增後可以看到錄製面版如下圖，通常是出現在畫面右下角處。
   
    ![RecordingPanel](/assets/2018-09-05/Win_RecordingPanel.jpg)

    接下來就可以操作錄製面板進行動作的錄製如下圖，錄製了輸入框內容的更新及按下按鍵的動作。

    ![Recording01](/assets/2018-09-05/recording_01.gif)

 4. 整合錄製動作與測試函式

    開啟預設建立的測試類別，調整原來的測試函式如下。
   
   ```csharp
    [TestMethod]
    public void CodedUITestMethod1()
    {
        var sAppFullPath = @"your\app\full\path\app.exe";
        var objApp = ApplicationUnderTest.Launch(sAppFullPath);
        var objMap = new UIMap1Classes.UIMap1();

        objMap.RecordedMethod1();

        objApp.Close();            
    }
   ```

5. 執行測試

   接下來就執行測試，應該就可以看到錄製的操作自己動起來，過程中要注意不要移到游標，不然會干擾到自動操作，可能造成未正常結果。

# 參考 

 * [[MSDN]-UI 測試自動化](https://docs.microsoft.com/zh-tw/visualstudio/test/use-ui-automation-to-test-your-code?view=vs-2017)

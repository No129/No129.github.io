---
layout: post
title: "測試工具地圖"
categories: QA
tag: 
date: 2020-05-05 22:23:51 UTC+8 
last_modified_at: 2020-05-05 22:23:51 UTC+8 
---

# 測試工具地圖  

## 單元測試
### 後端 ( 商業邏輯 )
* [Visual Studio][VS]
    * [開始使用單元測試][Ref011]
    * [使用 MSTest 與 .NET Core 為 C# 進行單元測試][Ref015]
    * [使用 Microsoft Fakes 隔離測試中的程式碼][Ref029]

### 前端 ( 互動控制 ) - 網頁應用
* [Visual Studio Code][VS]
* [Node.js][nodejs]
* [Vue CLI][vuecli]
    * [[vue] 使用 jest 和官方的 vue test utils 來寫單元測試 ( vue 單元測試系列-5 )][Ref013]
    * [Vue Test Utils][Ref014]

### 前端 ( 互動控制 ) - 桌面應用
* [Visual Studio (  UI Automation )][UIAutomation]
    * [使用 UI Automation 实现自动化测试入门 1][Ref026]
    * [使用 UI Automation 实现自动化测试][Ref027]
    * [基于 UI Automation 的自动化测试工具设计指南][Ref028]
    * [WPF 自訂控制項的 UI 自動化][MSDN:UIAutomation]
    * [測試回合: 自動化在 WPF 應用程式的 UI 測試][MSDN:UIA]    
    * [UWP 开发砸手机系列（二）—— “讲述人”识别自定义控件 Command][Ref994]
    * [微软 UI 自动化测试的技术演变 ( 上 )][Ref992]
    * [微软 UI 自动化测试的技术演变 ( 下 )][Ref991]
    * [浅谈 window 桌面 GUI 技术及图像渲染性能测试实践][Ref990]
    * [C# 4.0 動態型別應用例：動態載入 DLL 模組][Ref989]
    * [WPF UIAutomation 测试套件开发][Ref988]
    * [是否可以为整个 WPF 4.0 应用程序禁用 UI 自动化？][Ref997]
        * [WPF performance issue due to UI Automation][Ref996]
        * [WPF UI Automation issue][Ref995]
    * 桌面 UI 測試工具未能取得控制項，可能是因為 [Custom Controls and UI Automation][Ref999] 所提到的情形，該控制項未實做 AutomationPeer 類別，另外在 [如何访问未实现 AutomationPeer 类的 WPF 自定义控件的内部元素？][Ref998] 一文中則有提到不同的處理方式可以試試。

## 整合測試 / 負載測試

### 預存程序
* [SQLQueryStress][SqlQueryStress]  
    * [[SQL Server] SQLQueryStress, Stress testing, 壓力測試][Ref010]

### 網頁應用
* [Visual Studio ( Web 效能和負載測試專案 )][VS_WebLoading]
    * [雲端式負載測試服務生命週期結束][Ref017]
* [Selenium][selenium] 
    * [網站自動化測試之美][Ref016]
* [JMeter][JMeter]  
    * [使用 JMeter 對 Web 伺服器壓力測試][Ref001]

### 桌面應用
* [Visual Studio ( Coded UI )][CodedUI]
    * [Visual Studio 將棄用 Coded UI Test，建議開發者轉使用開源測試工具][Ref012]
* [Visual Studio ( TestStack.White )][TestStack.White]
    * [使用 TestStack.White 進行 Windows UI 的自動化測試 (1) 基礎篇][Ref018]
    * [Windows Automation Testing Framework – TestStack.White (一)][Ref019]
    * [TestStack.White (二) – 取得元件的方式][Ref020]
    * [TestStack.White (三) – 與 UI Automation 的比較][Ref021]
    * [TestStack.White (四) – 初探 White 時遇到的困難][Ref022]
    * [[自動化測試] WPF UI 自動化測試使用 TestStack.White (上)-基本設定與語法][Ref005]
    * [[自動化測試] WPF UI 自動化測試使用 TestStack.White (中)-測試架構][Ref006]
    * [[自動化測試] WPF UI 自動化測試使用 TestStack.White (下)-第三方Control對應][Ref007]
* [AutoIt][AutoIt]
    * [AUTOIT 視窗程式自動化 WinForm Test automation][Ref003]
    * [AUTOIT 自動化完成程式安裝][Ref004]
* [Appium][appium]
    * [[Appium][WinAppDriver] Appium + WinAppDriver 測試 Windows 桌面應用程式 UI][Ref009]
* [SWAPY][SWAPY] + [PyWinAuto][pywinauto]
    * [Windows 應用程式的自動化測試 by Python][Ref002]
* [Accessibility Insights][AccessibilityInsights]
    * [for Windows][Ref023]
    * [for Web][Ref024]
    * [for Android][Ref025]
* [Spy++][Spy++]
    * [VS2019 安裝 Spy++][Ref008]


[VS]:https://visualstudio.microsoft.com/zh-hant/
[nodejs]:https://nodejs.org/en/
[vuecli]:https://cli.vuejs.org/
[JMeter]:https://jmeter.apache.org/
[SqlQueryStress]:https://github.com/ErikEJ/SqlQueryStress
[AutoIt]:https://www.autoitscript.com/site/autoit/downloads/
[SWAPY]:https://github.com/pywinauto/SWAPY
[pywinauto]:https://github.com/pywinauto/pywinauto
[appium]:https://github.com/appium/appium
[selenium]:https://www.selenium.dev
[Spy++]:https://docs.microsoft.com/zh-tw/visualstudio/debugger/spy-increment-help?view=vs-2019
[TestStack.White]:https://github.com/TestStack/White
[CodedUI]:https://docs.microsoft.com/zh-tw/visualstudio/test/use-ui-automation-to-test-your-code?view=vs-2019
[VS_WebLoading]:https://docs.microsoft.com/zh-tw/visualstudio/test/quickstart-create-a-load-test-project?view=vs-2019
[AccessibilityInsights]:https://accessibilityinsights.io/
[UIAutomation]:https://docs.microsoft.com/zh-tw/dotnet/framework/ui-automation/ui-automation-overview

[MSDN:UIAutomation]:https://docs.microsoft.com/zh-tw/dotnet/framework/wpf/controls/ui-automation-of-a-wpf-custom-control
[MSDN:UIA]:https://docs.microsoft.com/zh-tw/archive/msdn-magazine/2009/march/test-run-automating-ui-tests-in-wpf-applications

[Ref001]:https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/553469/
[Ref002]:https://www.qa-knowhow.com/?p=2559
[Ref003]:https://aa1235561.pixnet.net/blog/post/329784699-%5Bautoit%5D%E8%A6%96%E7%AA%97%E7%A8%8B%E5%BC%8F%E8%87%AA%E5%8B%95%E5%8C%96-winform-test-automation
[Ref004]:https://blog.xuite.net/yzporyco/blog/35663225-AutoIT+%E8%87%AA%E5%8B%95%E5%8C%96%E5%AE%8C%E6%88%90%E7%A8%8B%E5%BC%8F%E5%AE%89%E8%A3%9D

[Ref005]:http://aminggo.idv.tw/blog/?p=777
[Ref006]:http://aminggo.idv.tw/blog/?p=787
[Ref007]:http://aminggo.idv.tw/blog/?p=817
[Ref008]:https://blog.darkthread.net/blog/install-spyxx-in-vs2019/
[Ref009]:https://www.dotblogs.com.tw/yc421206/2019/03/19/via_Appium_and_WinAppDriver_UI_Test_Automation_on_Windows_Applications
[Ref010]:http://sharedderrick.blogspot.com/2017/08/stress-testing-sqlquerystress-portable.html
[Ref011]:https://docs.microsoft.com/zh-tw/visualstudio/test/getting-started-with-unit-testing?view=vs-2019
[Ref012]:https://www.ithome.com.tw/news/130084
[Ref013]:https://dotblogs.com.tw/kinanson/2017/10/17/222548
[Ref014]:https://vue-test-utils.vuejs.org/zh/
[Ref015]:https://docs.microsoft.com/zh-tw/dotnet/core/testing/unit-testing-with-mstest
[Ref016]:https://learngeb-ebook.readbook.tw/
[Ref017]:https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/
[Ref018]:https://dotblogs.com.tw/wellwind/2015/12/22/white-windows-form-ui-testing-1
[Ref019]:https://kkboxsqa.wordpress.com/2014/05/09/windows-automation-testing-framework-teststack-white-%e4%b8%80/
[Ref020]:https://kkboxsqa.wordpress.com/2014/05/20/teststack-white-%e4%ba%8c-%e5%8f%96%e5%be%97%e5%85%83%e4%bb%b6%e7%9a%84%e6%96%b9%e5%bc%8f/
[Ref021]:https://kkboxsqa.wordpress.com/2014/05/29/teststack-white-%e4%b8%89-%e8%a9%95%e4%bc%b0%e4%bd%bf%e7%94%a8/
[Ref022]:https://kkboxsqa.wordpress.com/2014/06/13/teststack-white-%e5%9b%9b-%e5%88%9d%e6%8e%a2-white-%e6%99%82%e9%81%87%e5%88%b0%e7%9a%84%e5%9b%b0%e9%9b%a3/
[Ref023]:https://accessibilityinsights.io/docs/en/windows/overview
[Ref024]:https://accessibilityinsights.io/docs/en/web/overview
[Ref025]:https://accessibilityinsights.io/docs/en/android/overview
[Ref026]:https://www.cnblogs.com/Luouy/p/4045903.html
[Ref027]:https://www.cnblogs.com/kangyi/category/209042.html
[Ref028]:https://blog.csdn.net/zhengzhe1937/article/details/8499811?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158866813819726867841898%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=158866813819726867841898&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v25-18
[Ref029]:https://docs.microsoft.com/zh-tw/visualstudio/test/isolating-code-under-test-with-microsoft-fakes?view=vs-2019


[Ref999]:https://docs.microsoft.com/en-us/archive/blogs/patrickdanino/custom-controls-and-ui-automation
[Ref998]:https://www.orcode.com/question/1240975_k0836d.html
[Ref997]:https://bugjia.net/200216/228820.html
[Ref996]:https://stackoverflow.com/questions/5716078/wpf-performance-issue-due-to-ui-automation
[Ref995]:https://stackoverflow.com/questions/6362367/wpf-ui-automation-issue
[Ref994]:https://www.cnblogs.com/manupstairs/p/5065228.html
[Ref992]:https://www.cnblogs.com/stbchina/archive/2010/01/25/tech-trend-of-microsoft-ui-automation-testing-part-1.html
[Ref991]:https://www.cnblogs.com/stbchina/archive/2010/01/28/Tech-Trend-of-Microsoft-UI-Automation-Testing-Part-Two.html
[Ref990]:https://blog.csdn.net/zuozewei/article/details/82656926
[Ref989]:https://www.huanlintalk.com/2009/02/dynamically-loaded-dll-with-cshar-4.html
[Ref988]:https://blog.csdn.net/mzl87/article/details/102833669

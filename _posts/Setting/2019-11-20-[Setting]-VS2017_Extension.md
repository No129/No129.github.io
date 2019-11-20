---
layout: post
title: "Visual Studio 常用擴展整理"
categories: Setting
tag: 
date: 2019-11-20 23:59:59 UTC+8 
last_modified_at: 2019-11-20 23:59:59 UTC+8 
---
雖然 Microsoft Visual Studio 號稱地表最強 IDE 還是不免俗的需要擴展來再加強個別功能，為了避免換用電腦或重灌後就忘掉或少掉什麼擴展，也順便梳理一下那些是真的常用的擴展。

# IDE 層級擴展
* **Veracode Greenlight for Visual Studio**  
提供靜態掃描。
* **SonarLint for Visual Studio 2017**  
提供靜態掃描。
* **SpecFlow for Visual Studio 2017**  
提供 SpecFlow 的文件建立，要另外搭配專案層級的擴充，可以參考[這篇文章][Specflow]。
* **GhostDoc Community for VS2017 and Later**  
自動生成程式註解，可以參考[這篇文章][GhostDoc]。
* **VsVim**  
提供類似 Vim 的全鍵盤操作可能，可以參考[這篇文章][VsVim]。
* **RelativeLineNumbers**  
在行號旁提供[相對行號][Numbers]，方便在 Vim 模式的移動操作中快速知道要前往位置的相對行號。
* **SHFB**  
提供說明文件(Help)專案，它的 Github 在[這裡][SHFB]。
* **Snippet Designer**  
程式片段設計工具，可以參考[這篇文章][SnippetDesigner]。
* **Microsoft Visual Studio Installer Projects**  
提供安裝專案，在 VS2017 後原生沒有提供安裝專案，可以參考[這篇文章][InstallerProjects]。

# Project 層級擴展
* **System.Windows.Interactivity.WPF**  
提供 WPF 前端介面要套用 MVVM 時，可在 XAML 中將事件轉為繫結至命令物件。
* **Specflow**  
提供 Specflow 功能，配合 IDE 層級的 SpecFlow for Visual Studio 2017 使用，可以參考[這篇文章][Specflow]。



[SHFB]:https://github.com/EWSoftware/SHFB
[Specflow]:https://dotblogs.com.tw/yc421206/2014/12/22/unit_test_specflow_hello_world
[GhostDoc]:https://dotblogs.com.tw/wasichris/2016/01/21/172429
[VsVim]:https://dotblogs.com.tw/mystic_pieces/2018/03/03/003303
[SnippetDesigner]:https://dotblogs.com.tw/kinanson/2014/09/22/146654
[InstallerProjects]:https://blogs.msdn.microsoft.com/msdntaiwan/2014/04/17/visual-studio-visual-studio-installer-project-installshield-limited-edition/
[Numbers]:https://www.weiyeying.com/ask/6131796
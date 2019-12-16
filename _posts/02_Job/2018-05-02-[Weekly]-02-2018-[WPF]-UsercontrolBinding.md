---
layout: post
title: "[WPF] UserControl 的資料繫結"
categories: Job WPF
tag: 
date: 2018-05-02 00:00:00 UTC+8 
last_modified_at: 2018-05-02 00:00:00 UTC+8 
---

# 狀況 CONTEXT

當我們寫了一個 UserControl 控制項，如何透過資料繫結方式動態控制該控制項？


# 準備 PREPARE
1. 新增一個名稱 DEMO 的 WPF App 專案 。

2. 新增一個名稱為 MyTextBlock 的 UserControl 控制項，並加入一個 TextBlock 控制項，其 Xaml 如下：

    ``` XML
    <UserControl x:Class="DEMO.MyTextBlock"
                xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
                xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
                xmlns:local="clr-namespace:DEMO"
                mc:Ignorable="d" 
                d:DesignHeight="450" d:DesignWidth="800">
        <Grid>
            <TextBlock Text="It's alive!!!" />
        </Grid>
    </UserControl>
    ```

    CodeBehide 的程式預設應該如下：
    ``` csharp
    using System.Windows.Controls;

    namespace DEMO
    {
        /// <summary>
        /// Interaction logic for MyTextBlock.xaml
        /// </summary>
        public partial class MyTextBlock : UserControl
        {
            public MyTextBlock()
            {
                InitializeComponent();
            }
        }
    }
    ```

在使用啟動視窗插入 MyTextBlock 控制項。

``` XML
<Window x:Class="DEMO.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:DEMO"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <local:MyTextBlock />
    </Grid>
</Window>
```

# 方案 SOLUTION

## 一、 UserControl 繫結特定屬性

使用者控制項 ( MyTextBlock ) 直接繋結到容器物件 ( MainWindow ) 的屬性。

1. 調整 MyTextBlock 控制項

    將原來固定的文字內容改為繫結方式決定。

    ``` xml
    <TextBlock Text="{Binding Description}" />
    ```
2. 調整 MainWindow 視窗

    * XAML 
        ``` xml
        <local:MyTextBlock x:Name="MyTextBlockControl" />
        ```

    * Code 
    
        建立提供繫結的屬性，並在建構元指定控制項資料來源。

        ``` csharp
        public MainWindow()
        {
            InitializeComponent();
            this.MyTextBlockControl.DataContext = this;
        }

        public string Description { get; set; }= "It's alive!!! by Binding MainWindow.Description";
        ```

## 二、 UserControl 繫結 UserControl 屬性

1. 在 MyTextBlock 建立 Descrption 相依屬性 。
    ```csharp
        public readonly DependencyProperty DescriptionProperty =
                DependencyProperty.Register(nameof(Description), typeof(string), typeof(MyTextBlock), new PropertyMetadata());

        public string Description
        {
            get { return (string)this.GetValue(DescriptionProperty); }
            set { this.SetValue(DescriptionProperty, value ); }
        }  
    ```
2. 調整 MainWindow 視窗

    ```xml
    <local:MyTextBlock Description="It's alive!!! by xaml setting" />
    ```

3. 設定繫結方式：
    
    繫結方式可以透過程式或 XAML 完成，在此例子中效果相同。

    * 透過程式設定繫結：

        * MyTextBlock 的 XAML
            ```xml
            <TextBlock Text="{Binding Description}" />
            ```

        * MyTextBlock 的 Code
        
            初始程式中指定控制項的 DataContext 為自已，並建立對應的相依屬性。

            ```csharp
                public MyTextBlock()
                {
                    InitializeComponent();
                    // 指定資料來源。
                    this.DataContext = this;
                }
            ```

    * 透過 XAML 設定繫結：

        調整的地方有兩個，首先加上 UserControl 的名稱，然後調整 TextBlock.Text 的繫結語法，透過 ElementName 設定指定資料來源。

        ```xml
        <UserControl x:Class="DEMO.MyTextBlock"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
             xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
             xmlns:local="clr-namespace:DEMO"
             mc:Ignorable="d" 
             d:DesignHeight="450" d:DesignWidth="800"
             x:Name="MainControl">
            <Grid>
                <TextBlock Text="{Binding Description, ElementName=MainControl }" />
            </Grid>
        </UserControl>
        ```
        

## 三、 UserControl 繫結指定屬性

1. 調整 MyTextBlock 控制項

    這部分可以參考「 UserControl 繫結 UserControl 屬性」說明，透過 Code 或 XAML 達成，下面以 XAML 示範。

    * Code 
        ```csharp
            public readonly DependencyProperty DescriptionProperty =
                    DependencyProperty.Register(nameof(Description), typeof(string), typeof(MyTextBlock), new PropertyMetadata());

            public string Description
            {
                get { return (string)this.GetValue(DescriptionProperty); }
                set { this.SetValue(DescriptionProperty, value ); }
            }  
        ```

    * XAML    

        ```xml
        <UserControl x:Class="DEMO.MyTextBlock"
                xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
                xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
                xmlns:local="clr-namespace:DEMO"
                mc:Ignorable="d" 
                d:DesignHeight="450" d:DesignWidth="800"
                x:Name="MainControl">
            <Grid>
                <TextBlock Text="{Binding Description, ElementName=MainControl }" />
            </Grid>
        </UserControl>
        ```

2. 調整 MainWindow 視窗
    
    * XAML 
        ```xml
        <<UserControl x:Class="DEMO.MyTextBlock"
                xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
                xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
                xmlns:local="clr-namespace:DEMO"
                mc:Ignorable="d" 
                d:DesignHeight="450" d:DesignWidth="800"
                x:Name="MainControl"  >
            <Grid>
                <TextBlock Text="{Binding Description, ElementName=MainControl }" />
            </Grid>
        </UserControl>
        ```
    
    * Code

        ```csharp
        public string Description { get; set; } = "It's alive!!! by MainWin.Description";
        ```

# 分析 ANALYSIS

方案一最簡單，但是控制項繫結的對象被定義在控制項內，使用的容器物件指定 DataContext 時配合控制項的設定，若是無法知道控制項繫結設定，就無法或難以正確的給定繫結資料，僅適合在快速建立且後續不維護的單一專案。

方案二透過相依屬性的建立，提供控制項的資料繫結來源可由容器自訂的彈性，方案三則由方案二延伸而來，展示容器自訂的部分也由透過繫結完成，兩種型式都可視情況選用，例如按鍵的說明，通常不會在執行階段異動，採用方案二的方式，在 XAML 直接給定即可，兼顧方便與直覺；但如果是操作訊息之類，會在執行階段異動，若採用方案二，在異動邏輯會有操作控制項的必要，如此可能打破 WPF 前端的 MVVM 架構，此時採用方案三並繫結到相依屬性後，就可以透過重設屬性來更新控制項，達成以資料更新進行控制項操作的 MVVM 架構。


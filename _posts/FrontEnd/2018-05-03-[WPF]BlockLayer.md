---
layout: post
title: "[WPF] 畫面遮蔽效果實作"
categories: TECH WPF
tag: WPF
date: 2018-05-03 00:00:00 UTC+8
last_modified_at: 2018-05-03 00:00:00 UTC+8 
---

# 效果 EFFECT

在系統進行長時間處理程序時，必須限制使用者操作，為了提供更友善的操作經驗，可以透過遮蔽畫面的效果，讓使用者無法觸及受限的控制項，但仍能進行其他操作。

# 準備 PREPARE

1. 新增一個名稱 DEMO-BlockingLayer 的 WPF App 專案。

2. 在 MainWindow 布置控制項。

    * XAML

        這裡將畫面區分為上下兩部分，上部是遮蔽的目標區，下部是遮蔽的控制按鍵。

        ``` XML
        <Window x:Class="DEMO_BlockingLayer.MainWindow"
                xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
                xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
                xmlns:local="clr-namespace:DEMO_BlockingLayer"
                mc:Ignorable="d"
                Title="MainWindow" Height="450" Width="800">
            <Grid>
                <Grid.RowDefinitions>
                    <RowDefinition Height="*" />
                    <RowDefinition Height="80PX" />
                </Grid.RowDefinitions>
                <Grid Grid.Row="0">                    
                    <Button Width="125px" Height="25px" Content="受限按鍵" Margin="10" Click="Button_Click" />
                </Grid>
                <StackPanel Grid.Row="1" Orientation="Horizontal" HorizontalAlignment="Center">
                    <Button Width="125px" Height="25px" Content="開啟遮蔽" Margin="10" Click="StartBlockingButton_Click" />
                    <Button Width="125px" Height="25px" Content="結束遮蔽" Margin="10" Click="EndBlockingButton_Click" />
                </StackPanel>
            </Grid>
        </Window>
        ```

    * CODE

        提供按鍵點繫對應操作，判斷遮蔽是否成功。

        ```csharp
        private void Button_Click(object sender, RoutedEventArgs e)
            {
                MessageBox.Show("It's alive!!!");
            }
        ```

        控制遮蔽的對應操作事件。

        ```csharp

         private void StartBlockingButton_Click(object sender, RoutedEventArgs e)
        {

        }

        private void EndBlockingButton_Click(object sender, RoutedEventArgs e)
        {

        }

        ```

# 操作 OPERATE

只要簡單的插入 Canvas 控制項及增加對應的事件控制碼，啟動程式後可以透過兩個按鍵決定是否遮蔽受限按鍵。

* XAML

    加入 Canvas 控制項在待遮蔽的 Grid 控制項。

    ```xml
    <Grid Grid.Row="0">
        <Canvas x:Name="BlockingLayer" Panel.ZIndex="1" Background="Gray" Visibility="Hidden" Opacity="0.25"   />
        <Button Width="125px" Height="25px" Content="受限按鍵" Margin="10" Click="Button_Click" />
    </Grid>
    ```

* CODE

    操作事件中加上對 Canvas 控制項的顯示控制。

    ```csharp
    private void StartBlockingButton_Click(object sender, RoutedEventArgs e)
    {
        this.BlockingLayer.Visibility = Visibility.Visible;
    }

    private void EndBlockingButton_Click(object sender, RoutedEventArgs e)
    {
        this.BlockingLayer.Visibility = Visibility.Hidden;
    }
    ```

# 應用 APPLY

遮蔽功能可應用於等待畫面的建立，接下來就延續前面的示範，實作受限按鍵點擊後觸發遮蔽，並在長時間處理後自行恢復的情境。

* XAML

    加入 StackPanel 控制項，並命名為 WaitPanel 方便程式操作。

    ```xml
    <Grid Grid.Row="0">
        <Canvas x:Name="BlockingLayer" Panel.ZIndex="1" Background="Gray" Visibility="Hidden" Opacity="0.75" />
        <StackPanel x:Name="WaitPanel" Panel.ZIndex="1" Background="Gray" Visibility="Hidden" HorizontalAlignment="Center" VerticalAlignment="Center">
            <StackPanel Orientation="Vertical"  Background="White" Width="300px">
                <StackPanel Orientation="Horizontal" >
                    <Label Margin="0,15,0,5" Content="處理中..." VerticalAlignment="Center" Height="36px" />
                </StackPanel>
                <ProgressBar Height="20" Value="80" IsIndeterminate="True"/>
            </StackPanel>
        </StackPanel>
        <Button Width="125px" Height="25px" Content="受限按鍵" Margin="10" Click="Button_Click" />
    </Grid>
    ```

* CODE

    將 Button_Click 函式內容調整，透過 [Task][Task] 建立子執行緒，模擬長時間處理，最後在子執行緒結束 ( OnTaskDown ) 時重設顯示狀態。

    ```csharp
    private void Button_Click(object sender, RoutedEventArgs e)
    {
        this.BlockingLayer.Visibility = Visibility.Visible;
        this.WaitPanel.Visibility = Visibility.Visible;
        // 子執行緒處理長時間程序。
        Task.Factory.StartNew(this.RunTask).ContinueWith(this.OnTaskDown);
    }

    private void RunTask()
    {
        // 模擬長時間處理。
        System.Threading.Thread.Sleep(2000);
    }

    private void OnTaskDown(Task pi_objTask)
    {
        Dispatcher.Invoke( () =>
        {
            this.BlockingLayer.Visibility = Visibility.Hidden;
            this.WaitPanel.Visibility = Visibility.Hidden;
        });
    }
    ```

# 注意 NOTE

此實做主要是透過 [Panel.ZIndex][zindex] 的設定，藉由讓控制項「浮」在待遮蔽的控制項的表面，使用者的點擊都作用於表層的控制項而不會作用到被覆蓋的控制項，要特別注意的是，除了設定 [Panel.ZIndex][zindex] 之外，屬性 Background 也必須指定，才會有遮蔽效果，最後再配合 Visibility 屬性控制是否顯示來動態決定遮蔽交果。



[Task]:https://msdn.microsoft.com/zh-tw/library/system.threading.tasks.task(v=vs.110).aspx "Task 類別"
[zindex]:https://msdn.microsoft.com/zh-tw/library/system.windows.controls.panel.zindex(v=vs.110).aspx "Panel.ZIndex 附加屬性"


# 狀況 CONTEXT

在 WPF 中經常會透過 ICommand 來處理對應的操作及判斷是否可以操作，有時判斷的條件來自使用者是否有輸入及輸入的值，如何在使用者輸入過程進行 CanExecute 的判斷，而無需待失去焦點時才觸發？

# 準備 PREPARE

準備輸入框失去焦點後才進行 CanExecute 判斷的情境。

1. 新增一個 DEMO-JustInTimeCheckCanExecute 的 WPF App 專案。
2. 建立一個名稱為 DoSomethingCommand 的類別，並加入以下程式。

```csharp
Namespace DEMO-InTimeCheckCanExecute
{

}
```



[UpdateSourceTrigger][UpdateSourceTrigger]

[UpdateSourceTrigger]:https://msdn.microsoft.com/zh-tw/library/system.windows.data.updatesourcetrigger(v=vs.110).aspx "繫結屬性更新時機列舉"
[BindingByResourse]:https://social.msdn.microsoft.com/Forums/en-US/6df77aab-9acb-42e5-83e1-891322026b32/wpf-how-to-use-binding-by-elementname-in-resources?forum=wpf "繫結資源"
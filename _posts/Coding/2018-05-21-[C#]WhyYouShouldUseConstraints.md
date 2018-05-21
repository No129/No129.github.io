---
layout: post
title: "[C#] 為什麼你該使用泛形約束"
categories: TECH
tag: 
date: 2018-05-21 00:00:00 UTC+8 
last_modified_at: 2018-05-21 00:00:00 UTC+8 
---

# 「泛形」是什麼？

在進入泛形約束之前，該先知道泛形是什麼，可以看看下面幾篇：

* [Wiki - 泛型][1]
* [偉大的泛型][2]
* [泛型 (C# 程式設計手冊)][3]
* [泛型的優點 (C# 程式設計手冊)][4]
* [Visual Basic 中的泛型類型 (Visual Basic)][5]

# 「泛形約束」是什麼呢？

對於泛形約束可以參考 [MSDN][a] 的說明。

# 為什麼泛形還要加上約束呢？

在 [MSDN 的這篇文章中提到：為什麼使用條件約束][b]

```
透過限制型別參數，即可增加條件約束類型和其繼承階層中所有類型所支援項目的允許作業和方法呼叫數目。當您設計泛型類別或方法時，如果要對簡單指派以外的泛型成員執行任何作業，或呼叫 System.Object 不支援的任何方法，則必須將條件約束套用至型別參數。例如，基底類別條件約束會告知編譯器只有這個類型的物件或衍生自這個類型的物件才會用作型別引數。編譯器具有這項保證之後，就可以允許在泛型類別中呼叫該類型的方法。
```

這段描述說明的其實是「加上約束之後可以做什麼」，讓我們來看看文章中附的例子。

首先是一個 Employee 類別。

```csharp
public class Employee
{
    public Employee(string s, int i) => (Name, ID) = (s, i);
    public string Name { get; set; }
    public int ID { get; set; }
}
```
再來是泛形清單的實做：

```csharp
public class GenericList<T> where T : Employee
{
    private class Node
    {
        public Node(T t) => (Next, Data) = (null, t);

        public Node Next { get; set; }
        public T Data { get; set; }
    }

    private Node head;

    public void AddHead(T t)
    {
        Node n = new Node(t) { Next = head };
        head = n;
    }

    public IEnumerator<T> GetEnumerator()
    {
        Node current = head;

        while (current != null)
        {
            yield return current.Data;
            current = current.Next;
        }
    }

    public T FindFirstOccurrence(string s)
    {
        Node current = head;
        T t = null;

        while (current != null)
        {
            //The constraint enables access to the Name property.
            if (current.Data.Name == s)
            {
                t = current.Data;
                break;
            }
            else
            {
                current = current.Next;
            }
        }
        return t;
    }
}
```

所以我們就可以從 Employee 衍生自訂的 MyEmployee 類別，並且可以使用 GenericList 來儲存

```csharp
public class MyEmployee :Employee
{
    public MyEmployee(string s, int i, string e) : base(s, i) { this.Extension = e; }
    public string Extension { get; set; }
}
```
透過主控台程式呼叫使用：
```csharp
static void Main(string[] args)
{
    var EmployeeList = new GenericList<MyEmployee>();

    EmployeeList.AddHead(new MyEmployee("a", 1, "111"));
    EmployeeList.AddHead(new MyEmployee("b", 2, "222"));

    var EmployeeB = EmployeeList.FindFirstOccurrence("b");
    Console.WriteLine(EmployeeB.Extension);
    Console.ReadKey();
}
```

此例中，重點在於 `FindFirstOccurrence` 方法，因為泛形 T 加上了約束必須繼承自 Employee 類別，所以在這個方法中，變數 t 可以為 null 同時 Current.Data 可以有 Name 的屬性。


如果不加上約束就做不到嗎？其實還是可以的啊！

```csharp
public T FindFirstOccurrence(string s)
{
    Node current = head;
    T t = default(T);

    while (current != null)
    {
        var objCurrent = current.Data as Employee;

        if (objCurrent != null)
        {
            //The constraint enables access to the Name property.
            if (objCurrent.Name == s)
            {
                t = current.Data;
                break;
            }
            else
            {
                current = current.Next;
            }
        }
    }
    return t;
}
```

先將約束條件取消，會先看到 `T t = null;` 這行是有問題的，因為泛形不知道指定形別是否可以為 null 形態，所以改用 `default(T)` 指定為該形別預設值，然後就是將 `current.Data` 轉換型別為 Employee 後處理，程式就可以跟原來寫法一樣使用。

# 泛形約束可以帶來什麼好處？

在談到「為什麼」時，通常是指能帶來什麼好處而言，那麼泛形加上約束能有什麼好處嗎？

先看到下面這個例子，這是一個可以將傳入的資料表轉換為自訂類別清單的函式：

```csharp
public List<T> TableToList<T>(DataTable dt)
{
    List<T> list = new List<T>();
    Type type = typeof(T);

    PropertyInfo[] pArray = type.GetProperties();
    foreach (DataRow row in dt.Rows)
    {
        T entity = Activator.CreateInstance<T>();
        foreach (PropertyInfo p in pArray)
        {
            var obj = Convert.ChangeType(row[p.Name], p.PropertyType);

            p.SetValue(entity, obj, null);
        }
        list.Add(entity);
    }
    return list;
}
```

這個函式其實隱含著一個限制，就是指定的類別必須具備無參數的建構元，不然在 `T entity = Activator.CreateInstance<T>();` 動態生成時會有例外，但是在設計階段或是編譯階段都不會有問題，必須到執行階段時才會報錯。

如果利用泛型約束加上 `where T : new()` 就可以在設計階段發現，同時程式的寫法也可以精簡為 `T entity = new T();` 來生成物件，而不需使用到反射。

```csharp
public List<T> TableToList<T>(DataTable dt) where T : new()
{
    List<T> list = new List<T>();
    Type type = typeof(T);

    PropertyInfo[] pArray = type.GetProperties();
    foreach (DataRow row in dt.Rows)
    {
        //T entity = Activator.CreateInstance<T>();
        T entity = new T();
        foreach (PropertyInfo p in pArray)
        {
            var obj = Convert.ChangeType(row[p.Name], p.PropertyType);

            p.SetValue(entity, obj, null);
        }
        list.Add(entity);
    }
    return list;
}
```

# 結語

當你問 [換用 499 方案的用戶][499] 「為什麼」換方案時，應該不會得到「從此每個月可以繳 499 元」這個答案，而是「便宜，從此每月可以只繳 499 元」這個答案，因為繳 499 元決對不是目的，比原來繳的便宜才是目的。

同理，泛形約束`即可增加條件約束類型和其繼承階層中所有類型所支援項目的允許作業和方法呼叫數目。`只是使用泛型約束可以達到的效果，為什麼使用泛形約束的目的應該是：

* 設計階段 VisualStudio 就可以反應傳入型別是否合法
* 泛形處理過程可以不用轉型或是透過反射建構

在設計階段 VisualStudio 就可以反應傳入型別是否合法 ( 最晚在編譯階段就會報錯 )，還可以透過 VisualStudio 協助生成對應的程式碼，可以有效的減少開發的時間，不會在程式執行階段，甚至上線後才發現；而泛形處理過程可以不用轉型或透過反射建構，則可以有效提昇執行時期執行效率，因為不用 boxing/unboxing 物件。

`使用泛形而不加約束，有時並不影響功能的撰寫，但加上約束可以節省開發時間與執行時間。`


[1]:https://dotblogs.com.tw/supershowwei/2016/03/25/011226 "Wiki - 泛型"
[2]:http://epaper.gotop.com.tw/pdf/AXP013300.pdf "偉大的泛型"
[3]:https://msdn.microsoft.com/zh-tw/library/512aeb7t.aspx "泛型 (C# 程式設計手冊)"
[4]:https://msdn.microsoft.com/zh-tw/library/b5bx6xee.aspx "泛型的優點 (C# 程式設計手冊)"
[5]:https://docs.microsoft.com/zh-tw/dotnet/visual-basic/programming-guide/language-features/data-types/generic-types "Visual Basic 中的泛型類型 (Visual Basic)"

[a]:https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/keywords/where-generic-type-constraint "where (泛型類型條件約束) (C# 參考)"
[b]:https://docs.microsoft.com/zh-tw/dotnet/csharp/programming-guide/generics/constraints-on-type-parameters "型別參數的條件約束 (C# 程式設計手冊)"

[499]:https://zh.wikipedia.org/wiki/499%E5%90%83%E5%88%B0%E9%A3%BD%E4%B9%8B%E4%BA%82 "499吃到飽之亂"
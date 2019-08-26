WPF X MVVM
* 取得 TreeView 目前選取項目 --> 透過在每個項目的 IsSelect 屬性查找
* 取得 DataGrid 目前選取 Cell --> 取得 Column 資訊( DataGridCell )
* 取得 DataGrid 目前選取 Item --> 取得 Row 資訊( 繫結資料 )



建立實體的方法

* Serialization

** without a template, without caching

```csharp
public static class FormatterServicesBuilderWithoutCachingWithoutGeneric
{
    public static object Build(Type t)
    {
        var o = FormatterServices.GetUninitializedObject(t);
        var ctor = t.GetConstructors()[0];
        return ctor.Invoke(o, new object[] { });
    }
}
```

* 參考資料  
1. [Activator.CreateInstance Alternatives with Benchmarks][1]
2. [C# 快速動態建立物件實體技巧][2]


[1]:http://grantbyrne.com/post/activatorcreateinstancealternativetesting/ "Activator.CreateInstance Alternatives with Benchmarks"

[2]:https://dotblogs.com.tw/code6421/2019/08/15/csharpfastobject?fbclid=IwAR1mFR9ZFIxJFVAyJhWOw3ZlbGhF128v8Vnx4REu9DBZfBwIGBGA-ogKt04 "C# 快速動態建立物件實體技巧"
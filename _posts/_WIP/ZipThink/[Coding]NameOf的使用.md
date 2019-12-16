撰寫程式的過程，應該避免一些「魔術常數」，其中很常發魔鬼字串的時機就是在輪詢屬性時，針對特定屬性進行不同處理。

```csharp
For Each objProperty As PropertyInfo In Me.GetType().GetProperties()
    Select Case objProperty.Name
        Case "PropertyName1"
            'do something.
        Case "PropertyName2"
            'do something.
    End Select
Next
```

這樣屬性名稱一但異動，很容易就漏改到判斷句中的字串。

透過 NameOf 函式就可以避免魔鬼字串的出現，傳入的是物件的成員，所以在設計階段就很好用，屬性名稱異動，如果透過 VS 的功能可以統一修改，若是手動異動，則在編譯時期就會報錯，除非有同名的成員。

```csharp
For Each objProperty As PropertyInfo In Me.GetType().GetProperties()
    Select Case objProperty.Name
        Case NameOf(Property1)
            'do something.
        Case NameOf(Property2)
            'do something.
    End Select
Next
```
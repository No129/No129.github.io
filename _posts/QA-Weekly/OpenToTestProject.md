# 情境

開發功能時，為了符合專案層級的開放封閉原則，並不會讓所有的類別都是公開，可能很多都是專案內部呼叫，但如此一來也同時將測試專案拒於門外，但這些內部類別仍有單元測試的必要，如何能夠維持專案層級的開放封閉原則，同時讓測試專案可以取得待測類別。

# 開放特定專案

透過在待測專案中加上 [InternalsVisibleToAttribute] 設定：

```xml
<assembly: InternalsVisibleTo("測試專案名稱")>
```

# 參考

* MSDN:[InternalsVisibleToAttribute]


[InternalsVisibleToAttribute]: https://msdn.microsoft.com/en-us/library/system.runtime.compilerservices.internalsvisibletoattribute.aspx 
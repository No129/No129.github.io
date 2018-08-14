---
layout: post
title: "專案內部類別對測試專案開放"
categories: QA
tag: 
date: 2018-08-14 23:59:59 UTC+8 
last_modified_at: 2018-08-14 23:59:59 UTC+8 
---
# 情境

開發時，為了符合專案層級的開放封閉原則，實務上並不會也不該讓所有的類別都設定為公開，更多的類別應該都只提供專案內部呼叫，以避免被外部誤用，但如此一來也同時將測試專案拒於門外，但這些僅供專案內部呼叫的類別仍有單元測試的必要，因此需要能夠維持專案層級的開放封閉原則，同時讓測試專案可以讀取待測類別。

# 開放特定專案

透過在待測專案中加上 [InternalsVisibleToAttribute] 設定，則原本只提供專案內容存取的類別也可以讓指定的專案讀取。

# 專案具備強式名稱設定

若是待測試專案有加上強式名稱的簽名設定，則在設定時需要額外提供公開鑰匙，此時，先讓測試專案加上強式名稱簽名，則 Visual Studio 會在撰寫 [InternalsVisibleToAttribute] 時，自動補上公開鑰匙的序號。

此外，也可以透過[強式名稱工具](https://docs.microsoft.com/zh-tw/dotnet/framework/app-domains/how-to-create-a-public-private-key-pair) ( [取得 sn.exe 工具](https://stackoverflow.com/questions/1535871/cannot-find-sn-exe-to-sign-assembly) ) 手動取得公鑰序號。

## 手動取得既有私鑰的公鑰序號

透過 Windows 的命令列模式，逐步操作下述命令：

1. 從既有私鑰取得公鑰檔案

```
sn -p PrivateKey.snk PublicKey.snk
```

2. 從公鑰檔案取得序號，下述命令執行後會在命令列視窗列出該序號。
```
sn -tp PublicKey.snk
```


[InternalsVisibleToAttribute]: https://msdn.microsoft.com/en-us/library/system.runtime.compilerservices.internalsvisibletoattribute.aspx 
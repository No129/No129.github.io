---
layout: post
title: "[CODING]子執行緒存取 Access 資料庫連線不穩定"
categories: Job Troubleshoot
tag: 
date: 2018-05-03 00:00:00 UTC+8 
last_modified_at: 2018-05-03 00:00:00 UTC+8 
---

# 狀況 ISSUE

目前在 Winbase 的開發環境中，存取 Access 資料庫 ( .access ) 時，發現若是反覆進行連線資料庫 ( OleDbConnection ) 時，會不定時發生 [AccessViolationException](https://msdn.microsoft.com/zh-tw/library/ms164911.aspx) 例外，如下圖，[這是作業系統層級的嚴動例狀況，因為侵犯到了其他行程的記憶體，所以程式必須強制關閉](https://social.msdn.microsoft.com/Forums/zh-TW/948bb276-1249-40ad-a49e-923c18e9083f/-accessviolationexception-?forum=233)


![例外](/assets/2018-05-03-SubThreadConnectToAccessUnstable/screenshot.87.jpg)


# 方案 SOLUTION

採用 OleDbDataReader 存取資料庫，如果需要 DataTable 則可以[將 DataReader 取得的資料轉至 DataTable](http://blog.xuite.net/s0341969690/wretch/173473860-%E5%B0%87DataReader%E5%8F%96%E5%BE%97%E7%9A%84%E8%B3%87%E8%BD%89%E8%87%B3DataTable) ，可以參考下列程式碼。

```csharp
    var dataset = new DataSet();
    var datatable = new DataTable();
    var sql = "select * from Table";
    OleDbCommand com = null;
    OleDbDataReader reader = null;
    OleDbConnection cn = new OleDbConnection();
    cn.ConnectionString = "Provider = Microsoft.ACE.OLEDB.16.0: Data Source = [Access File Path]; Jet OLEDB:Database Password = ;OLE DB Services=-2;";

    cn.Open();
    com = new OleDbCommand(sql, cn);
    reader = com.ExecuteReader();
    datatable.Load(reader);
    reader.Close();
    com.Dispose();
    com = null;
    dataset.Tables.Add(datatable);
```

# 後記 Notes

其實只要透過主執行緒就不會最前面提到的情況，但是在 Winbase 的系統中，若是採用主執行緒處理，則前端的使用者介面就會整個被涷住，無法與使用者做互動，例如視窗的縮小操作都沒有反應，若是缺少適當的提示，很容易讓使用者認為系統當掉了，但其實正在努力的處理使用者的要求。

延伸視窗凍結的情況，則系統無法提供非同步處理，例如在使用者輸入時，同時進行預先檢查或提供選項，都會因為視窗凍結而無法提供。

此外，其實並未找到相關文件說明，在狀況發生的確切原因，而所提供的解決方案則是試誤法下，反覆測試後，相對穩定的撰寫方式，不代表為最佳解，及無法保證必然能解決。

# 參考 REFREENCE

* [Invode](http://www.cnblogs.com/guogangj/archive/2013/01/22/2870590.html)
* [OleDbConnection.ConnectionString 屬性](https://msdn.microsoft.com/zh-tw/library/system.data.oledb.oledbconnection.connectionstring(v=vs.110).aspx)
* [Connection Pooling with Access database](https://stackoverflow.com/questions/10012627/connection-pooling-with-access-database)
* [Overriding Provider Service Defaults](https://msdn.microsoft.com/en-us/library/ms724518(v=vs.85).aspx)

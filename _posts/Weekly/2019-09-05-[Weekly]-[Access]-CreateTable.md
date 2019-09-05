---
layout: post
title: "[Access] 如何在 Access 資料庫新增一個資料表"
categories: TechWeekly Access
tag: 
date: 2019-09-05 23:59:59 UTC+8 
last_modified_at: 2019-09-05 23:59:59 UTC+8 
---

# 前言
因為維護在桌面應用系統的過程中要透過程式在 [*ACCESS*][MSAccess] 資料庫中新增一個資料表，但因為一直以來都是透過 [OLEDBConnection][OleDb] 與資料庫連線，所以要透過 *SQL* 語法建立對應的欄位有些陌生，花了時間找了文章加上在 [*ACCESS*][MSAccess] 中手動測試後，整理了各個欄位型別在 *SQL* 語法中的寫法。

# 對照

|Access type            |SQL        |C# Type|
|---|---|---|
|Short Text             |TEXT       |string|
|Long Text              |MEMO       |string|
|Number(byte)           |BYTE       |byte|
|Number(single)         |SINGLE     |single|
|Number(double)         |DOUBLE     |double|
|Number(decimal)        |--         |decimal|
|Number(Long Integer)   |INTEGER    |int32|
|Number(integer)        |SHORT      |int16|
|Number(Replication ID) |--         |--|
|LargeNumber            |--         |--|
|Date/Time              |DATETIME   |datetime|   
|Currency               |CURRENCY   |decimal|
|Autonumber             |Autonumber |int|
|Yes/no                 |YESNO      |bool|
|OLE object             |IMAGE      |byte[]|
|Hyperlink              |--         |--|
|Attachment             |--         |--|
|binary                 |BINARY     |--|

# 語法範例
以下語法將會建立一個名稱為「TableName」的資料表，在此新增的資料表中包含一個名稱  為「Column1」的欄位，而此欄位的資料型別在 [Access][MSAccess] 的設計檢視中看到的資料型別為[「Sort Text」][MSADataTypeIntro] 同時它的長度被設定為 15 個單元。

```SQL
CREATE TABLE [TableName] ( [Column1] TEXT(15))
```

# 參考文章
* [INFO: OleDbType Enumeration vs. Microsoft Access Data Types](:https://support.microsoft.com/en-us/help/320435/info-oledbtype-enumeration-vs-microsoft-access-data-types)

[oledb]:https://docs.microsoft.com/zh-tw/dotnet/api/system.data.oledb.oledbconnection?view=netframework-4.8 "OleDbConnection Class"

[MSAccess]:https://www.microsoft.com/zh-TW/p/access/cfq7ttc0k7q8?=&OCID=AID2000136_SEM_Nvw2hlvj&MarinID=sNvw2hlvj%7c332895000849%7cms+access%7ce%7cc%7c%7c61150178523%7ckwd-26962656&lnkd=Google_O365SMB_NI&gclid=Cj0KCQjwwb3rBRDrARIsALR3XeYWCcFbHWTdLeNOosAJIckrr8qNuHyZRWLzdmIpQFIz7Fyxygv8iiwaAok_EALw_wcB&activetab=pivot%3aoverviewtab "Microsoft Access"

[MSADataType]:https://docs.microsoft.com/zh-tw/sql/odbc/microsoft/microsoft-access-data-types?view=sql-server-2017 "Microsft Access 資料類型"
[MSADataTypeIntro]:https://support.office.com/en-us/article/introduction-to-data-types-and-field-properties-30ad644f-946c-442e-8bd2-be067361987c ""
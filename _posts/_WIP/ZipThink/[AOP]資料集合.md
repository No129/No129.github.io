# AOP 橫向設計

* 可以透過 CallContext 進行資料傳遞




[透過 Castle.Windsor 實做 AOP ](https://dotblogs.com.tw/hatelove/2014/05/04/implementation-aop-by-castle_windsor)

透過 Decorator Pattern 實作是一種半套的做法，因為如果將椅子往 坐，視野拉大一些，那麼決定是否要加上 Log 的責任還是被參雜在呼叫端類別。

[1]:https://www.lanhusoft.com/Article/240.html "C#.NET利用ContextBoundObject和Attribute实现AOP技术--AOP事务实现例子"
[2]:https://dotblogs.com.tw/steventsai/2017/06/08/143849 "【Asp.Net MVC】使用 ContextBoundObject 搭配 Attribute 實現 AOP Logging 機制"

[MSDN-1]:https://msdn.microsoft.com/zh-tw/library/system.runtime.remoting.contexts.contextattribute(v=vs.110).aspx "ContextAttribute 類別"
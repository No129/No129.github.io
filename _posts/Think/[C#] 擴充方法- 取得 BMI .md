
# 情境 SCENARIO

假設目前系統有一個 People 類別，現在想增加 BMI 值

```csharp
    public class People
    {
        public int Height { get; set; }
        public int Weight { get; set; }
    }
```

不同方式實做，也影響如何被使用。

* 直接在 People 類別中加上屬性
```csharp 
var John = new People();
var JohnBMI = John.BMI;
```

* 透過 Counter 類別提供計算功能
```csharp
var John = new People();
var Counter = new BMICount();
var JohnBMI = Counter.Counting(John);
```

* 透過 Counter 類別提供計算功能，採用靜態方法
```csharp
var John = new People();
var JohnBMI = Counter.Counting(John);
```

* 在 People 類別中加上計算介面，並將 Counter 類別傳入
```csharp
var John = new People();
var Counter = new BMICount();
var JohnBMI = John.BMI(Counter);
```

* 利用擴充方法，提供 People 類別 BMI 方法
```csharp
var John = new People();
var JohnBMI = John.BMI;
```



[1]:https://docs.microsoft.com/zh-tw/dotnet/csharp/programming-guide/classes-and-structs/extension-methods "擴充方法"
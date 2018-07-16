---
layout: post
title: "訪問者模式 ( Vistor Design Pattern )"
categories: TECH
tag: 
date: 2018-07-13 24:00:00 UTC+8 
last_modified_at: 2018-07-16 24:00:00 UTC+8 
---
# 適用情境
* 「物件結構」的「元素」種類不常變動，但「動作」經常增減；因此，若未符合以下任一描述，基本就不用考慮此模式：
    * 需要輪詢一組「元素」物件，針對「不同元素」的作出不同處理。( 此段所指「元素」為基底類別或介面，「不同元素」是指其衍生或實做類別 )
    * 需要輪詢一組「元素」物件，執行跨元素的處理，例如累計或篩選。( 此段所指「元素」皆指執行個體 )

# 缺點：
* 破壞資料結構的封裝，因為元素必須提供操作必要資料。
* 違反「依賴倒轉」原則，角色 Visitor 是對元素的實作類別設計而不是對介面。
* 增加元素類別種類時對整體影響很大，因為元素類別增加時需要對於既有的 Visitor 類別都必須更新以提供新增元素類別的處理。

# 類別圖：
![Vistor Design Pattern](/assets/DesignPattern/VisitorDesignPattern.jpg)

# 釋例-計算折扣
本節透過一個商品價格計算的例子說明，商品區分為 Food 及 Book 兩類，價格計算則區分為平日或假日兩種處理邏輯，之後可能因應各種情境需要不同計算邏輯。

* 首先建立商品的兩種型態 Food 及 Book 對應的類別：

```csharp
    public class Food
    {
        public double Price;

        public Food(double pi_nPrice)
        {
            this.Price = pi_nPrice;
        }
    }

    public class Book
    {
        public double Price;

        public Book(double pi_nPrice)
        {
            this.Price = pi_nPrice;
        }
    }
```

* 建立 Vistor Design Pattern 的元素與操作角色，在此以抽象類別撰寫，採用介面也可以：

```csharp
    //元素角色的基底類別。
    public abstract class BaseProduct
    {
        public abstract void Accept(BaseCalculator pi_objCalculator);
    }

    //操作角色的基底類別。
    public abstract class BaseCalculator
    {
        //處理 Food 的計算。
        public abstract void Visit(Food food);
        //處理 Book 的計算。
        public abstract void Visit(Book book);

    }
```

* 讓 Food 及 Book 類別繼承 BaseProduct 抽象類別，具有「被訪問」的能力：

```csharp
    public class Food : BaseProduct
    {
        public double Price;

        public Food(double pi_nPrice)
        {
            this.Price = pi_nPrice;
        }

        //覆寫基底類別方法。
        public override void Accept(BaseCalculator pi_objCalculator)
        {
            pi_objCalculator.Visit(this);
        }
    }

    public class Book : BaseProduct
    {
        public double Price;

        public Book(double pi_nPrice)
        {
            this.Price = pi_nPrice;
        }

        //覆寫基底類別方法。
        public override void Accept(BaseCalculator pi_objCalculator)
        {
            pi_objCalculator.Visit(this);
        }
    }
```

* 建立「訪問者」角色的 CommonCalculator 類別提供平日的計算功能：

```csharp
    //提供平日計算邏輯。
    public class CommonCalculator : BaseCalculator
    {

        public override void Visit(Food food)
        {
            Console.WriteLine("Food's common price:" + food.Price);
        }

        public override void Visit(Book book)
        {
            Console.WriteLine("Book's common price:" + book.Price);
        }
    }
```

* 假日需要不同的折扣所以增加一個 HolidayCalculator 類別：

```csharp
    //提供假日的計算邏輯
    public class HolidayCalculator : BaseCalculator
    {

        public override void Visit(Food food)
        {
            Console.WriteLine("Food's holiday price:" + food.Price * 0.8);
        }

        public override void Visit(Book book)
        {
            Console.WriteLine("Book's holiday price:" + book.Price * 0.95);
        }
    }
```

* 客戶端的呼叫：

```csharp
    class Program
    {
        static void Main(string[] args)
        {
            var objMilk = new Food(100);
            var objEZABC = new Book(100);

            var objCommon = new CommonCalculator();        
            var objHoliday = new HolidayCalculator();
            
            Console.WriteLine("-- 平日時段 --");
            objMilk.Accept(objCommon);
            objEZABC.Accept(objCommon);
            
            Console.WriteLine("-- 假日時段 --");
            objMilk.Accept(objHoliday);
            objEZABC.Accept(objHoliday);

            Console.ReadKey();
        }
    }
```

* 輸出結果：
```
    -- 平日時段 --
    Food's common price:100
    Book's common price:100
    -- 假日時段 --
    Food's holiday price:80
    Book's holiday price:95
```

* 但這個例子並無法表現出 Visitor Design Pattern 的優點，畢竟客戶端可以直接如下例呼叫，就可以得到相同結果，單純利用多形的特色就可以將資料與操作分離，完全不用套模式。

```csharp
    class Program
    {
        static void Main(string[] args)
        {
            var objMilk = new Food(100);
            var objEZABC = new Book(100);

            var objCommon = new CommonCalculator();        
            var objHoliday = new HolidayCalculator();
            
            Console.WriteLine("-- 一般時段 --");
            objCommon.Visit(objMilk);
            objCommon.Visit(objEZABC);
            
            Console.WriteLine("-- 假日時段 --");
            objHoliday.Visit(objMilk);
            objHoliday.Visit(objEZABC);

            Console.ReadKey();
        }
    }
```

* 採用 Vistor Design Pattern 的威力在 ObjectStructure 中展現，在下例中新增一個 List 項作為購物車，將兩個產品放到清單中，如此一來就可以逐項呼叫：

```csharp
    class Program
    {
        static void Main(string[] args)
        {
            var objMilk = new Food(100);
            var objEZABC = new Book(100);

            var objCommon = new CommonCalculator();
            var objHoliday = new HolidayCalculator();

            var objCart = new List<BaseProduct>() { objMilk, objEZABC };

            Console.WriteLine("-- 一般時段 --");
            foreach (BaseProduct objProduct in objCart)
            {
                objProduct.Accept(objCommon);
            }

            Console.WriteLine("-- 假日時段 --");
            foreach (BaseProduct objProduct in objCart)
            {
                objProduct.Accept(objHoliday);
            }

            Console.ReadKey();
        }
    }                                   
```

# 結論
首先，訪問者模式將原本在操作時需要進行型別判斷的程序直接透過類別本身處理，可以將原本需要透過型別判斷的判斷句取消，統一透過 Accept 函式處理掉了；此外，訪問者一般會遍歷所有項目，所以可以做到跨項目的功能，例如前面的結帳功能，就能在計算同時行加總的功能。

```csharp
    public class CommonCalculator : BaseCalculator
    {
        private double l_nSummery = 0;

        public override void Summery()
        {
            Console.WriteLine("Summery:" + this.l_nSummery);
        }

        public override void Visit(Food food)
        {
            this.l_nSummery += food.Price;
            Console.WriteLine("Food's common price:" + food.Price);
        }

        public override void Visit(Book book)
        {
            this.l_nSummery += book.Price;
            Console.WriteLine("Book's common price:" + book.Price);
        }
    }
```
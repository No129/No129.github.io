---
layout: post
title: "程式備註標籤如何連結到 Sandcastle 的文件"
categories: Job tip SandCastle
tag: 
date: 2019-02-25 23:59:59 UTC+8 
last_modified_at: 2019-02-25 23:59:59 UTC+8 
---

[Sandcastle]:[Sandcastle] 工具可以讀取程式的註解，分析後產生類別的說明內容，同時也能透過其獨立的應用介面，或是高度的整合於 Visual Studio 開發環境的編輯介面，撰寫額外的說明文件，應該是最常用的說明檔產生工具。

程式的註解及文件之間，彼此之間相互參照，透過文件的說明可以了解整體運行邏輯及類別的互動關係，或是設計背景，然後結合類別的註解，達到整體及細部資訊的整合。

# Sandcastle 文件指向類別說明
在 [Sandcastle][Sandcastle] 文件中，只需透過標籤 [codeEntityReference][codeEntityReference] 可以在文件中建立一個連結到類別說明的超連結，提供使用者即時關連過去，相當簡單方便。

## [codeEntityReference][codeEntityReference]
「[codeEntityReference][codeEntityReference]」標籤可提供名域空間、型別（包含類別、列舉、介面及結構）、參數、事件、屬性及方法的超連結方式，其中對於建構元及泛形參數的呼叫需要額外注意。

## 建構元
要建立超連結到類別的建構元說明，是透過 M 前置詞，也就是採用方法的描述方式，但與一般方法描述不同的是採用「#ctor」來取代建構元方法名稱，可以參考官方文件例子。

## 泛型
以 [這篇提問的個案][generic] 為例，假設有一個包含泛形的擴展方法如下，方法定義的泛型同時也傳入參數的型別。

```csharp
namespace SampleProject
{
    public static class ExtensionMethods
    {
        public static bool SomeExtension<T>(this T some) => true;
    }
}
```

若要關連到此範例中的 SomeExtension 方法，就要注意到關連方法的泛型及參數的型別也是泛型定義，下面示範了在 [Sandcastle][Sandcastle] 文件中建立到此方法說明的超連結標籤寫法，透過字元「\``」表達泛型，方法後綴的「\``1」表示有一個泛形，而參數的「\``0」則是表示第一個泛型定義。

```xml
<codeEntityReference>
    M:SampleProject.ExtensionMethods.SomeExtension``1(``0)
</codeEntityReference>
```

[generic]:https://stackoverflow.com/questions/33606679/codeentityreference-to-method-on-a-sandcastle-developerhowtodocument "codeEntityReference to method on a Sandcastle developer How to Codument"

# 類別註解指向 Sandcastle 文件
 透過 [Sandcastle][Sandcastle] 建立的說明檔 ( .chm ) 本質上就是一組靜態網頁，所以可以透過對 href 特性的設定建立類別到文件的超連結。對於跨類別的說明，或個別類別的進一步說明，在個別類別的備註中不易說明時，就可以透過另外的文件加以描述，再透過超連結從類別說明指向說明文件，則維護類別時可以有完整而整體的資訊。  

原本 [see][see] 及 [seealso][seealso] 這兩個標籤就可以透過 [cref][cref] 特性建立類別之間關連的超連結；而透過 href 特性則可以建立外部連結，例如 [這篇提問][href_example] 想要的外連自訂的說明網站，例如下面的寫法，在 Sandcastle 解析即會建立對應的超連結。

 ```csharp
 ///<Summary>
 /// This is a math function I found <see href="http://some.where.on.web">hear</see>.
 ///</Summary>
 ```

 而要連到說明文件可以參考[這篇提問][href_link]的回應，首先是 href 特性值要填上說明文件對應的頁面名稱外，此外則要額外再加上 target 特性，讓超連結指向文件本身。

 ```csharp
/// <seealso href="AllMembers_T_MyNamespace_Class1.htm" target="_self">Class1 Members</seealso>  
 ```


[Sandcastle]:https://github.com/EWSoftware/SHFB/releases "Sandcastle"
[codeEntityReference]:http://ewsoftware.github.io/MAMLGuide/html/bc490dbf-7d46-432d-a816-3ae16ab6af54.htm "codeEntityReference"

[see]:https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/xmldoc/see "<see> C# Programming Guide"
[seealso]:https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/xmldoc/seealso "<seeals> C# Programming Guide"

[cref]:https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/xmldoc/cref-attribute "cref Attribute"

[href_example]:https://stackoverflow.com/questions/6960426/c-sharp-xml-documentation-website-link "c# XML Documentation Website Link"

[href_link]:https://stackoverflow.com/questions/34403891/how-can-i-reference-a-members-page-from-a-seealso-tag "How can I reference a Members page from a <seealso> tag?"



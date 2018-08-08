# 前言

如何在 XML 加上名稱空間設定？


# [Add new Namespace](https://www.codeproject.com/Questions/161436/C-XML-add-a-new-Namespace)

預期結果，在 OrderPush 節點設定名稱空間的設定：

```xml
<OrderPush 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:bml="http://netlab.gmu.edu/IBML">
    <OrderPush>
        <bml:TaskersIntent/>
        <bml:Task>
            <bml:GroundTask>
                <bml:TaskeeWho

>
```

## 方法一

```csharp
XmlDocument.DocumentElement.SetAttribute("xmlns:xsi", "http://www.w3.org/2001/XMLSchema-instance"); XmlDocument.DocumentElement.SetAttribute("xmlns:bml", "http://netlab.gmu.edu/IBML");
```


## 方法二

```csharp
XNamespace ns = "http://www.w3.org/2001/XMLSchema-instance";  
string s = new XElement("OrderPush", 
            new XAttribute(XNamespace.Xmlns + "xsi", ns),
            new XAttribute(ns + "noNamespaceSchemaLocation", "namespace.xsd")).ToString();
```


## 方法三 （with XmlWriter)

```csharp
const string ns = "http://www.w3.org/2001/XMLSchema-instance"; writer.WriteStartDocument(); writer.WriteStartElement("OrderPush"); writer.WriteAttributeString("xmlns", "xsi", "", ns); writer.WriteAttributeString("xsi", "noNamespaceSchemaLocation",       ns, "namespcae.xsd"); writer.WriteEndDocument();
```
[.net 單元測試的藝術](https://read01.com/zh-tw/Po83Oa.html#.W3O4AOgzaUk)

# 獨體模式與靜態類別

獨體類別或靜態類別的單元測試撰寫，往往很容易相互干擾，造成單元測試結果的不穩定，為解決此一問題，最好的模式就是不寫單元測試。然而，要能夠不寫獨體類別與靜態類別的單元測試，首先應該將獨體模式或靜態類別所包含的商業邏輯獨立出來，如此一來獨體類別或靜態類別本身沒有處理商業邏輯，就不具備單元測試的價值，因此，獨體類別或靜態類別不需進行單元測試。

# 複製貼上

產品碼著重在同一商業邏輯應該透過同一處程式碼，在該商業邏輯異動時，只需異動一處程式碼，若是撰寫產品碼時，反覆複製同一段程式碼在不同處，則當商業邏輯異動時，將造成系統多處必須修改，容易漏改或改錯，在撰寫產品碼時 [DRY ( Don't repeat yourself )](https://zh.wikipedia.org/wiki/%E4%B8%80%E6%AC%A1%E4%B8%94%E4%BB%85%E4%B8%80%E6%AC%A1) 原則幾乎是最基本必須遵守的原則。

但是與產品碼不同，測試碼強調

* 個別測試之間應保持獨立，以利個別執行及除錯。
* 測試碼描述必須保持直觀，除了便於閱讀，亦是避免測試碼的邏輯造成干擾。
* 測試碼應採最低成本維護，避免耗費過多資源。

因此，相對於產品碼來說，測試碼的程式複製貼上的情形是可以被接受，甚至是必須的；不過也應該考慮，適當的重構測試碼是否有助於提昇前述要點的成效，適時進行重構。

## 範例

* 情境說明：
    
    假設需要 XDocument 物件作為測試之用。
    
    一般產品碼大概都會透過物件動態組成，後續可能再重構：

    ```csharp
        private XDocument GetDocument()
        {
            var objReturn = new XDocument();
            XNamespace objXSD = "http://www.w3.org/2001/XMLSchema";
            var objSchema = new XElement(objXSD + "schema",
                new XAttribute(XNamespace.Xmlns + "xsd", "http://www.w3.org/2001/XMLSchema"));
            var objImport = new XElement(objXSD + "import",
                new XAttribute("namespace", "ar"),
                new XAttribute("schemaLocation", "ar.xsd"));

            objSchema.Add(objImport);
            objReturn.Add(objSchema);
            return objReturn;
        }
    ```

    但在測試碼中應該這麼寫：
    ```csharp
        private XDocument GetDocument()
        {
            var objReturn = new XDocument();
            var sSource = 
                "<xsd:schema xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\">" +
                "   <xsd:import namespace=\"ar\" schemaLocation=\"ar.xsd\" />" +
                "</xsd:schema>";
            objReturn = XDocument.Parse(sSource);

            return objReturn;
        }
    ```
    
    因為在測試碼中應該注重的是更快理解，而非程式重用。
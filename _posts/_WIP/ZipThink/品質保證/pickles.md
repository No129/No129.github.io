# VSTest.console

* 路徑：C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\TestWindow
* 指定結果路徑：
    ```
    vstest.console C:\Workspace\Framework\PwCTW\Client\Service\XBRL\_Tests\XBRL.UT\bin\Debug\XBRL.UT.dll /logger:trx;LogFileName=c:\_TOHU\TEST\TestResult.trx
    ```
    ```
    VSTest.console [測試專案函式庫] /logger:trx[;LogFileName=<Defatlt >]
    ```


* 參考：[使用 VSTest.console 執行 MSTest V2](https://blog.yowko.com/2018/04/vstest-console-mstest-v2.html)

* [醒醒吧少年，只用Cucumber不能帮助你BDD](http://insights.thoughtworkers.org/bdd/)
* [[搞搞就懂]-[BDD] 使用 SpecFlow 從需求起步進行開發](https://dotblogs.com.tw/wasichris/2016/09/30/233728)

# [Pickles](https://www.nuget.org/packages/Pickles/)

## Pickles - The Open Source Living Documentation Generator 

**Pickles** is an open source **living documentation** generator that works on feature files written in the *Gherkin* language, popularized in tools like *Cucumber* and *SpecFlow*.

**Pickles** 是一個開放源碼的 **living documentation** (活文件) 生成器，用於處理用 [Cucumber](https://github.com/cucumber/cucumber) 或 [SpecFlow](https://github.com/techtalk/SpecFlow) 等工具所建立，採用 [Gherkin](https://en.wikipedia.org/wiki/Cucumber_(software)) 語法編寫的 feature 檔。( 關於 Gherkin 語法可參考 [Cucumber 行為驅動開發指南](http://www.books.com.tw/products/CN11014775) 一書) 

*Pickles* can be incorporated into your build process to produce living documentation in a format that is more accessible to your clients. *Gherkin* language files are written in plain text and stored in your source folder. This can make them inaccessible to clients who may not know how to work with source control or who are not interested in seeing all of the source code, just the features.

*Pickles* 可以整合進建置程序，以更適合客戶存取的格式產生活文件。*Gherkin* 語言檔以純文本檔案編寫並與程式碼一同儲存。

*Pickles* can produce output in different formats:

- Static HTML: a set of HTML files with minimal JavaScript
- Dynamic HTML: a JavaScript-rich single page app with integrated search
- Word: Microsoft Word
- Excel: Microsoft Excel
- JSON: a custom JSON format

Optionally, *Pickles* can **integrate test results**, so that your stakeholders know which scenarios pass validation. *Pickles* supports these test formats:

- NUnit
- MSTest
- XUnit
- SpecRun
- Cucumber JSON
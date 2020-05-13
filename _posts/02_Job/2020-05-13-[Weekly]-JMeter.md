---
layout: post
title: "JMeter 起手式"
categories: QA
tag: 
date: 2020-05-13 22:23:51 UTC+8 
last_modified_at: 2020-05-13 22:23:51 UTC+8 
---
# JMeter
JMeter 是開源軟體 Apache 基金會下的一個負載測試工具，用來測試部署在伺服器端的應用程式的效能。

什麼是負載測試？舉個例子，你開了一個網路商店，興沖沖地準備雙十一大幹一把，沒想當天活動的時候大量用戶一訪問你的網店，你的網店就掛了，那怎麼辦？辦法就是在實際搞活動之前，先測試一下以確認系統能承受那麼多少用戶，當然測試的時候我們不需要請真正的這麼多實際用戶，否則得花多少錢啊！  

JMeter 能夠模擬大量用戶訪問的軟體，而且它是開源的，不花錢！

## 安裝
JMeter 的安裝非常簡單，從[JMeter 官方網站][JMeter] 下載壓縮檔後解壓即可使用。

* 下載
可以在 [JMeter 官方網站][JMeter] ( 如下圖 ) 後，再切換到 **[Download Releases][Ref001]** 頁面下載。

    ![JMeter](/assets/20200513/Image001.png)  

* 下載 .zip 檔案。
    ![JMeter Download](/assets/20200513/Image002.png)

* 解壓縮後執行 **bin\jmeter.bat** 批次檔就可以開啟 JMeter 的圖形介面
    ![JMeter Run Bat File](/assets/20200513/Image003.png)

* JMeter 的圖形介面
    ![JMeter Run Bat File](/assets/20200513/Image004.png)

### 未能正常開啟 JMeter 圖形介面
執行 **jmeter.bat** 後若未開啟 JMeter 的圖形介面，並且出現以下訊息:

    Not able to find Java executable or version. Please check your Java Installation.

這是因為 JMeter 是由 JAVA 撰寫開發，所以安裝 **JDK** 到電腦，可以自行到 **ORACLE** 下載安裝包。

## 開始使用
### 主要元件
* **測試計畫 ( Test Plan ):**  
所有的測試工作都基於測試計劃進行，個別專案中僅能具備單一測試計畫，也是其他 JMeter 元件的最上層容器。

* **執行緒組合 ( Threads(Users)\Thread Group ):**  
相當於許多執行緒的組合，在個別專案中有多個執行緒組合，對特定標的進行測試的各種不同呼叫的執行緒集合的概念，例如待測網站 A 及 網站 B 時，應建立兩個不同執行緒組合。  
代表一定數量的平行使用者，它可以用來模擬平行使用者傳送請求，實際的請求內容在 Sampler 中定義，被執行緒組合所包含。

* **監聽器 ( Listener ):**   
監聽器負責收集測試結果，同時也被告知結果顯示的方式。

* **邏輯控制器 ( Logic Controller):**  
可以自定義 JMeter 傳送請求的行為邏輯，它與 Sampler 結合使用可以模擬複雜的請求序列。
* **斷言 ( Assertions ):**  
可以用來判斷請求響應的結果是否如使用者所期望的。它可以用來隔離問題域，即在確保功能正確的前提下執行壓力測試。這個限制對於有效的測試是非常有用的。
* **配置文件 ( Config Element ):**  
維護 Sampler 需要的配置資訊，並根據實際的需要會修改請求的內容。
* **前置處理器 ( Pre Processors )／後置處理器 (  Post Processors ):**   
負責在生成請求之前和之後完成工作=方前置處理器常用來修改請求的設定，後置處理器則用來處理響應結果。
* **定時器 ( Timer ):**  
負責定義請求之間的延遲間隔。


### 1. 新增 Thread Group
![Add Thread Group](/assets/20200513/Image101.png)  
**Test Plan** 為所有項目的根節點，開啟新測試後預設會建立不用額外操作。 

* **設定測試數量**  
每次測試的數量，是透過 **執行緒數量 Number of Threads(users)** 及 **循環數量 Loop Count** 的乘數，在 JMeter 中執行緒數量配合的 **數量**，與 Visual Studio 中的 Web Loading 專案中指定一段 **時間** 不同。
![Run Times](/assets/20200513/Image103.png)  

### 2. 新增 HTTP Request
![Add Thread Group](/assets/20200513/Image102.png)

* 設定 HTTP Request  
![Add Thread Group](/assets/20200513/Image104.png)

完整設定可以參考 [使用手冊的 18.1.2 HTTP Request][Ref004] 的說明，簡單說明必要的參數如下：  
* **Basic**    
    * **Web Server**  
        * **Proptocol[http]:** 可以填入到 **HTTP** 及 **HTTPS** 兩種不同的協議。
        * **Server Name or IP:** 網頁的伺服器名稱或是 IP 位址。
        * **Port Number:** 埠號，預設 HTTP/HTTPS 的 80 埠號，可以設定自訂的不同埠號。
    * **HTTP Request**  
        * **Method:** 各個不同呼叫模式，例如 Get, Post 方法。
        * **Path:** 路徑，待測試的網址路徑。
        * **Redirect Automatically:** 勾選後，在網頁轉址時，將轉址與原請求視窗同一請求。
        * **Follow Redirects:** 勾選後，在網頁轉址時，將轉址視為個別不同請求。
        * **Use KeepAlive:** 設定 HTTP 呼叫的 Keep-Alive 設定。
    * **Parameters:** 提供設定網頁後綴參數。

### 3. 新增監聽器  
執行測試後，可以透過監聽器在執行過進行結果收集，以下列示兩種不同的監聽器，分別以樹狀結構及列表形式表示測試結果。
* View Results Tree
![Add Thread Group](/assets/20200513/Image105.png)
* View Results in Table
![Add Thread Group](/assets/20200513/Image106.png)

### 4. 執行與中斷
點擊綠色箭頭就會執行此 **測試計畫** 。  
![Run Test](/assets/20200513/Image107.png)

執行過程可以點撃 **STOP** 按鍵中斷執行。  
![Run Test](/assets/20200513/Image108.png)

清除測試結果則是利用 **掃帚** 按鍵。  
![Run Test](/assets/20200513/Image109.png)


## 參考文件  
* [官方使用手冊][JMeterManual]
* [JMeter 使用指南][Ref002]
* [JMeter multipart/form-data 請求自定義 body data 簡述][Ref003]
* [HTTP 協議詳解][Ref005]
* [JMeter 性能測試入門][Ref006]
* [JMeter 錄製腳本][Ref007]
* [Jmeter 教程 簡單的壓力測試][Ref008]
* [Apache JMeter™ : 負載測試與效能測量的好工具][Ref009]

[JMeter]:https://jmeter.apache.org/
[JMeterManual]:https://jmeter.apache.org/usermanual/index.html

[Ref001]:https://jmeter.apache.org/download_jmeter.cgi
[Ref002]:https://www.cnblogs.com/st-leslie/p/5185376.html
[Ref003]:https://www.itread01.com/content/1541152143.html
[Ref004]:http://svn.apache.org/repos/asf/jmeter/tags/v2_8/docs/usermanual/component_reference.html#HTTP_Request
[Ref005]:https://www.cnblogs.com/TankXiao/archive/2012/02/13/2342672.html
[Ref006]:https://www.cnblogs.com/TankXiao/p/4045439.html
[Ref007]:https://www.cnblogs.com/TankXiao/p/4064289.html
[Ref008]:https://www.cnblogs.com/TankXiao/p/4059378.html
[Ref009]:http://cloudchen.logdown.com/posts/247932/apache-jmeter-tool-for-load-test-and-measure-performance
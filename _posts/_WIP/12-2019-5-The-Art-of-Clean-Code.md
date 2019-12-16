

# Introduction (Why)

 Anyone can write code that a computer understands, but few programmers know how to write code that a **human can understand**. (Martin Fowler, Refactoring)


so COMMUNICATE, DON'T CODE.

乾淨 --> 易讀

花一份時間撰寫，要花十倍的時間在閱讀，節省了一次的時間，其實是浪費了往後維護時十倍的時間。

童子軍法則，每一次簽入都比你拿到時乾淨一些

當你停足重構時，程式就會變成遺留代碼( Legacy Code )

# Names (The power invested in you)


好的命名讓你更快速的了解程式

* 函式是**動作**，所以避免只給一個名詞

    product() vs searchProduct

* 類別是**物品**，所以透過擬人(角色或身份)或擬物(功能類比)
    Customer, orderDetails

* 避免無意義的名稱

    Order**Info**, Order**Data**, vs Order

* yes/no 問句就應該回傳布林值

    isGoldClient() --> Green

多花一些時間在命名上，對於整個程序的生命週期中，跨時期及跨部門的溝通都是有幫助的。

同時，一個好的名稱也可以看出對領域的理解。


* 如何理解一個函式？
    1. 閱讀**積了厚厚灰塵的**註解
    2. 被誰呼叫
    3. 解密函式的意函
    
為了避免往後維護如此麻煩，何不透過**名稱**讓函式**自我介紹**？

重新命名，讓函式有一個適當的名稱，目前的 IDE 可以非常方便的重新命名，可能只有在一些反射(reflection)或是 XML 設定檔之類的地方會有問題。

 There are only two hard things in Computer Science: cache invalidation and naming things.

 -- Phil Karlton

* Pronounceable: 要可以**發音** (不然口語溝通時會有困難)
    * Avoid abbreviations:避免縮寫，除非已是商業領域的共識。
* Consistent:維持一致
    find, fetch, get 

* Unique: 獨特
    Don't use buyer ro client to refer to a customer.
    對於同一事物採用相同名稱，避免同步混淆。



# Functions (SRP)
 
 A function **should do one thing**, it should do it well, and it should do it ONLY.
 - Uncle Bob

讓每個函式都保待**小巧**的尺寸。

多小？
* 5 行
* 一個螢幕

* 更小的函式帶給我們什麼？ 效能嗎? 不是

Measure, Don't Guess
-Kirk Pepperdine

Premature optimization is the root of all evil.
-Donald Kunth

* 會有一堆小函式，這樣好嗎? 害怕來自於以往不這麼做


* 傳入物件是否需要檢查其為空物件
    --> 僅在邊界(例如類別的公開方法)進行檢查（內部函式皆不檢查，因為公開方法會保證傳入物件的狀態)

* 避免回傳空物件
    * 擲出例外
    * 包裝在選擇性參數

* 程式永遠寫不完？一直都有更好的寫法?
* 所有的測試都通過後就是要重構程式，清理程式。

* 函式應在三層以內（three TABs)
* 避免在程式中間跳離

* GOD METHOD : 
    * 單一類別應該少於三百行
    * 如何解構**神函式**：27:00 ~ 29:00
        * Extract Method Object refactor:透過中介類別逐一分解
        

# Classes (The OOP Utopia 物件導向鳥托邦)

* OOP --> Allowing the implementation to evolve without breaking your clients
* 揭露**行為**而非資料  
    因為資料是依賴於細節而實做，是會異動的，例如啟動引擎的描述如果採用「car.engineStarted == True」或是「car.setEnginStarted(True)」就非常「程式」的語法，但如果是「car.startEngine()」就比較貼近一般文章的語法。
* 資訊隱藏  
    提供必要的資訊即可，例如確認目前的續航力描述，如果採用「car.getGasolineInLiters()」或是「car.getPercentageFuelLeft()」是取得當前的「燃料存量」資訊，相對來說「car.getEstimatedRemainingKm()」的描述就更加直接提供可續行的公里數
* Expose **Behavior**, not data
 Data is implementation detail:it will change
    * car.engineStarted == True (X)
    * car.setEnginStarted(True) (X)
    * car.startEngine()         (O)

* Infomation **Hiding**
 Tell as little as possible
    * car.getGasolineInLiters()
    * car.getPercentageFuelLeft()
    * car.getEstimatedRemainingKm()

* 其實，我們沒有採用物件導向開發，不是嗎? 都是「程序式」編碼
* 當系統的目的是在自動化某個商業**程序**，已存在的商業程序，所以自然發展出「程序程式」(Procedural code)
* 如何做到 **KISS** （Keep It Short and Simple)
    * 分配程序的邏輯（責任）到不同的類別，每個類別就像邏輯的容器

* 撰寫函式庫或（迷你)框架時，就容易落入版本地嶽，如何向前相容，如果你不採用物件導向。

# Commants (Incompetence)

* 你不是獨立作業，不是 Neo ，不是母體，你必須和其他人**合作**
* DON'T CODE! COMMUNICATE! 
* Respect your reader**s**, 10x more reading, remember?
* 永遠以最易懂的寫法，避免會造成混淆的寫法 --> Write **CHILDREN** Literature

* Tune your IDE （調整你的開發環境） 
* 快捷鍵／程式片斷 減少無效的操作時間
    * 盲打比語音輸入快，你會用語音輸入打程式嗎?
* 120 字元寬，10行高，單一函式不超過螢幕高度
* 註解與程式脫勾，應該壤程式自我說明
* 唯一正確的只有程式

* 註解不是提**什麼**而是應該說明**為什麼**
    * 規格（連結)/除錯說明
    * CLARIFICATIONS 例如說明調用特定 API 的原因
    * Warning of consequences 例如提醒該用法可能有執行緒安全的情形
    * DODOs 例如此次尚未處理，但可讓程式更具彈性或易讀的修改建議
    * Public API Documents 例如自行開發的函式庫或框架時，所撰寫的 API 說明文件
    * 

# Clean Lambdas (Handling a lightsaber)
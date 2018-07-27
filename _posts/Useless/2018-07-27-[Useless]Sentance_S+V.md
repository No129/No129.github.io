---
layout: post
title: "[useless]英文句型需求分析 - S+V"
categories: Useless
tag: 
date: 2018-07-27 00:00:00 UTC+8 
last_modified_at: 2018-07-27 00:00:00 UTC+8 
---

# 句型結構的需求分析
透過需求分析的手法來了解句型結構。首先要先了解老師口頭的「詞性」一辭其實有兩種不同的觀點：
* 個別單字所代表的詞性，例如，名詞 noun, 動詞 verb 
* 句子組成元素的詞性，例如，主詞 subject, 動詞 verb 

看看很多說法：
* 「名詞可以當主詞」：具備名詞特性的單字，可以放在句型中主詞的位置。
* 「動名詞可以代替名詞」：動詞只能放在句型中動詞的位置，但在轉換為動名詞後 ( V + ing )，可以代替名詞放在司型中主詞的位置。

# 程式開發的 [Hello World](https://zh.wikipedia.org/wiki/Hello_World)，數學界的[公理](https://zh.wikipedia.org/wiki/%E5%85%AC%E7%90%86) - 「S+V」


* 讓我們來分析這個句型的需求是什麼
```
Feature 主詞+動詞

Scenario 主詞為名詞，動詞為動詞
    Give 主詞為'Nothing' 
        And 動詞為'happens'
    When 呼叫句子
    Then 得到'Nothing happens.'    
```

建立處理函式如下：

```csharp
function sentence(string s, string v){
    console.writeline(string.form("{0} {1}.", s , v));
}
```

* 主詞不是名詞的案例
```
Scenario 主詞不是名詞時回傳 What?
    Give 主詞為'happens' 
        And 動詞為'happens'
    When 呼叫句子
    Then 得到'What?'    
```

修改處理函式如下：

```csharp
function sentence(string s, string v){
    if(string.IsNoun(s)){
        console.writeline(string.form("{0} {1}.", s , v));
    }else{
        console.writeline("What?");
    }
}
function static IsNoun(this string s){
    var bReturn = false;

    if(Noun.Contains(s){
        bReturn = true;
    }
    return bReturn;
}
```


* 需求異動：代名詞也可以為主詞，所以案例應該可以：
```
Scenario 主詞為代名詞，動詞為動詞
    Give 主詞為'It' 
        And 動詞為'happens'
    When 呼叫句子
    Then 得到'It happens.'    
```

修改處理函式如下：

```csharp
function sentence(string s, string v){
    if(string.IsNoun(s) || string.IsSynonym(s)){
        console.writeline(string.form("{0} {1}.", s , v));
    }else{
        console.writeline("What?");
    }
}
function static IsNoun(this string s){
    var bReturn = false;

    if(Noun.Contains(s){
        bReturn = true;
    }
    return bReturn;
}
function static IsSynonym(this string s){
    var bReturn = false;

    if(Synonym.Contains(s){
        bReturn = true;
    }
    return bReturn;
}
```

* 重構程式：其實需求是「代名詞可以取代名詞」所以將句型邏輯調整回「必須為名詞」然後調整「是否為名詞」的判斷，將「代名詞」視為「名詞」。

```csharp
function sentence(string s, string v){
    if(string.IsNoun(s)){
        console.writeline(string.form("{0} {1}.", s , v));
    }else{
        console.writeline("What?");
    }
}

function static IsNoun(this string s){
    var bReturn = false;

    if(Noun.Contains(s) || Synonym.Contains(s)){
        bReturn = true;
    }
    return bReturn;
}
```

* 需求異動：不是什麼動詞都可以，必須是「不及物動詞」( Intransitive Verb ) 才可以。
```
Scenario 動詞不是不及物動詞時，回傳 What?
    Give 主詞為'Nothing' 
        And 動詞為'like'
    When 呼叫句子
    Then 得到'What?'    
```

修改處理函式如下：

```csharp
function sentence(string s, string v){
    if(string.IsNoun(s) && string.IsIntransitiveVerb(v)){
        console.writeline(string.form("{0} {1}.", s , v));
    }else{
        console.writeline("What?");
    }
}

function static IsNoun(this string s){
    var bReturn = false;

    if(Noun.Contains(s) || Synonym.Contains(s)){
        bReturn = true;
    }
    return bReturn;
}

function static IsIntransitiveVerb(thie string v){
    var bReturn = false;

    if(IntransitiveVerb.Contains(v)){
        bReturn = true;
    }
    return bReturn;
}
```
# 句型 S+V 程式邏輯

* 規格書：

```
Feature 主詞+動詞

Scenario 主詞為名詞，動詞為動詞
    Give 主詞為'Nothing' 
        And 動詞為'happens'
    When 呼叫句子
    Then 得到'Nothing happens.'    

Scenario 主詞必須為名詞，否則回傳 What?
    Give 主詞為'happens' 
        And 動詞為'happens'
    When 呼叫句子
    Then 得到'What?'   

Scenario 代名詞可以視為名詞
    Give 主詞為'It' 
        And 動詞為'happens'
    When 呼叫句子
    Then 得到'It happens.'   

Scenario 動詞必須為不及物動詞，否則回傳 What?
    Give 主詞為'Nothing' 
        And 動詞為'like'
    When 呼叫句子
    Then 得到'What?'  
```

* 實做程式：
```csharp
function sentence(string s, string v){
    if(string.IsNoun(s) && string.IsIntransitiveVerb(v)){
        console.writeline(string.form("{0} {1}.", s , v));
    }else{
        console.writeline("What?");
    }
}

function static IsNoun(this string s){
    var bReturn = false;

    if(Noun.Contains(s) || Synonym.Contains(s)){
        bReturn = true;
    }
    return bReturn;
}

function static IsIntransitiveVerb(thie string v){
    var bReturn = false;

    if(IntransitiveVerb.Contains(v)){
        bReturn = true;
    }
    return bReturn;
}
```

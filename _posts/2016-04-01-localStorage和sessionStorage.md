---
layout: post
title:[【转】 localStorage和sessionStorage](http://blog.csdn.net/QDseashore/article/details/46799121)
categories:
- html5
tags:
- html5
---

 

說明

Html 5的Web Storage分兩種，一個是sessionStorage，另一個是localStorage，兩者差別就差在生命周期的不同而已，

只要會localStorage的使用方法，另一個sessionStorage寫法也差不多就會。

Web Storage特性:

1.儲存資料在Client端的瀏覽器，有點類似Cookie，不過Web Storage寫程式存取都是寫在Client端Javascript裡，Server端用不到

2.都是使用key / value pair的方式 給值或取值

3.儲存資料容量至少5MB以上，比Cookie大很多

4.不會像Cookie一樣，隨著Request發送給Server端，因為Web Storage只作用在Client端瀏覽器，不會占用頻寬，不影響網站效能，所以可以把size大一點&安全性低的資料儲存在Web Storage，提升網站效能。

5.只能儲存字串，想儲存物件的話，底下實作會說明

6.儲存在各瀏覽器中，所以在Chrome的Web Storage和IE的Web Storage是不會共用的，各自分開

7.Web Storage的值類似Cookie依網站區別，所以不同網站給相同的Web Storage值是不會共用的，是分開的

8.生命周期：

8-1:localStorage跨瀏覽器分頁、新視窗、甚至是關閉瀏覽器後再打開，localStorage仍然會存在，然後永久不逾期↓

When do items in HTML5 local storage expire?

8-2:sessionStorage生命周期只存在瀏覽囂的單一分頁，也就是另開新分頁的話，又是一個新的sessionStorage，預設無逾期時間，除非關閉該分頁、關閉瀏覽器等，sessionStorage就會消失。

9.支援瀏覽器：Internet Explorer 8+, Firefox, Opera, Chrome, Safari

 

 

待會底下會說明使用者如何用自己的瀏覽器自行清除Web Storage，或開發者寫程式來清除Web Storage

以上大概這樣，更詳細的說明請參考底下老師&專業級文章

[HTML5 Web Storage](http://huan-lin.blogspot.com/2012/06/html5-web-storage.html) by 蔡煥麟老師

 

用法

※通通都是寫在javascript裡

 

1.判斷瀏覽器是否支援Web Storage

    //此瀏覽器支援Web Storage
    if (typeof (Storage) !== "undefined") {
     
    } else {
    alert("此瀏覽器不支援Web Storage");
    }

↓以下列舉localStorage寫法當例子(sessionStorage寫法差不多)

 

2.localStorage給值寫法，挑一個自己想用的就好

    window.localStorage.setItem("Key名稱", "字串值");
    localStorage.setItem("Key名稱", "字串值");//前面的window. 可省略不寫
    localStorage["Key名稱"] = "字串值";//這寫法有cookie的fu
    localStorage.Key名稱 = "字串值";
    3.localStorage取值寫法，挑一個自己想用的就好
    
    var str = window.localStorage.getItem("Key名稱");
    var str = localStorage.getItem("Key名稱");
    var str = localStorage["Key名稱"]
    var str = localStorage.Key名稱;
    //↑以上注意取出來的值會是字串型別

4.判斷某localStorage是否存在

    if (localStorage.Key名稱)
   
    {//此localStorage有存在
   
    var str  =  localStorage.Key名稱; //把值取出來
   
     }

5.移除單個localStorage

localStorage.removeItem("Key名稱");
6.清除該網站所有的localStorage

localStorage.clear();
 



實作

以下是綜合範例程式碼，注意有引用到jQuery Library

※↓localStorage單純 給字串 取字串

    <script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>
    <script type="text/javascript">
    $(document).ready(init);
     
    function init() {
    //新增數字
    $("input#addCount").click(function () {
    //此瀏覽器支援Web Storage
    if (typeof (Storage) !== "undefined") {
    //注意Key有區分大小寫
    if (localStorage.clickcount) {//如果clickcount這個key裡有值的話
       
    localStorage.clickcount = Number(localStorage.clickcount) + 1;//把字串轉型成數字※Number()同時支援parseInt()和parseFloat()
    } else {//localStorage.clickcount 無值的話
    //localStorage只能儲存字串
    localStorage.clickcount = 1;//給預設1，此數字會自動轉型成字串，大概是js的特性？
    }
    $("div#result").html("目前localStorage的值為 " + (typeof (localStorage.clickcount) == "undefined" ? 0 : Number(localStorage.clickcount)));
     
    } else {
     
    alert("此瀏覽器不支援Web Storage");
    }
     
    });//end click 註冊事件
     
     
    $("input#removeOne").click(function () {
     
    //此瀏覽器支援Web Storage
    if (typeof (Storage) !== "undefined") {
    //注意Key有區分大小寫
    localStorage.removeItem("clickcount");
     
    $("div#result").html("目前localStorage的值為 " + (typeof (localStorage.clickcount) == "undefined" ? 0 : Number(localStorage.clickcount)));
     
    } else {
    alert("此瀏覽器不支援Web Storage");
    }
     
    });//end click 註冊事件
     
     
     
     
    $("input#clearAll").click(function () {
     
    //此瀏覽器支援Web Storage
    if (typeof (Storage) !== "undefined") {
     
    localStorage.clear();//清除所有localStorage
     
    $("div#result").html("目前localStorage的值為 " + (typeof (localStorage.clickcount) == "undefined" ? 0 : Number(localStorage.clickcount)));
     
    } else {
     
    alert("此瀏覽器不支援Web Storage");
    }
     
    });//end click 註冊事件
     
     
     
     
    }
     
     
     
     
    </script>
     
    <input type="button" value="加1"  id="addCount"/>
    <br />
      
    <input type="button" value="remove單個localStorage"  id="removeOne"/>
    <br />
      
    <input type="button" value="清除所有localStorage"  id="clearAll"/>
    <br />
      
    <!--呈現結果↓-->
    <div id="result">
     
    
     
     
    </div>

localStorage線上Demo，請使用IE開啟

[http://shadowjapan.blob.core.windows.net/dotblogsshare/StringSample.html](http://shadowjapan.blob.core.windows.net/dotblogsshare/StringSample.html)

 


※↓localStorage assign 物件寫法，要利用JSON.stringify(js物件)序列化成字串，再搭配JSON.parse(json字串)轉成JSON物件的方式處理

※此兩個js函式都是Javascript內建

 

    <script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>
    <script type="text/javascript">
    $(document).ready(init);
    //宣告js物件類別
    function Car() {
    //點擊次數
    this.clickcount = 0;
    }
    function init() {
     
    //新增數字
    $("input#addCount").click(function () {
    //此瀏覽器支援Web Storage
    if (typeof (Storage) !== "undefined") {
    //注意Key有區分大小寫
    if (localStorage.MyObj) {//如果localStorage.MyObj這個key裡有值的話
    //把json字串轉型成json物件
    var objCar = JSON.parse(localStorage.MyObj);//抓出json物件
    //assign value
    objCar.clickcount = Number(objCar.clickcount) + 1;//轉型成數字※Number()同時支援parseInt()和parseFloat()
    localStorage.MyObj = JSON.stringify(objCar);//重新把car物件序列化json字串 丟給 localStorage.MyObj
    } else {//localStorage.MyObj 無值的話
     
    var objCar = new Car();//new 一個物件
    objCar.clickcount = 1;//給預設1
    //localStorage只能儲存字串，如果想存js物件的話，就要把該js物件序列化成json字串存進去
    localStorage.MyObj = JSON.stringify(objCar);//序列化成json字串
     
    }
    //顯示結果↓
    var result = "";
    if ((typeof (localStorage.MyObj) == "undefined")) {
    result = 0;
    } else {
    //轉型成json物件
    var objCar = JSON.parse(localStorage.MyObj);
    result = objCar.clickcount;
    }
    $("div#result").html("目前localStorage的值為 " + result);
     
    } else {
     
    alert("此瀏覽器不支援Web Storage");
    }
     
    });//end click 註冊事件
     
     
    $("input#removeOne").click(function () {
     
    //此瀏覽器支援Web Storage
    if (typeof (Storage) !== "undefined") {
    //注意Key有區分大小寫
    localStorage.removeItem("MyObj");
     
    if (typeof (localStorage.MyObj) == "undefined") {
    $("div#result").html("目前localStorage的值為 " + 0);
    }
     
     
    } else {
    alert("此瀏覽器不支援Web Storage");
    }
     
    });//end click 註冊事件
     
     
     
     
    $("input#clearAll").click(function () {
     
    //此瀏覽器支援Web Storage
    if (typeof (Storage) !== "undefined") {
     
    localStorage.clear();//清除此網站所有localStorage
    if (typeof (localStorage.MyObj) == "undefined") {
    $("div#result").html("目前localStorage的值為 " + 0);
    }
     
     
    } else {
     
    alert("此瀏覽器不支援Web Storage");
    }
     
    });//end click 註冊事件
     
     
     
     
    }//end init
     
     
     
     
    </script>
     
    <input type="button" value="加1"  id="addCount"/>
    <br />
      
    <input type="button" value="remove單個localStorage"  id="removeOne"/>
    <br />
      
    <input type="button" value="清除所有localStorage"  id="clearAll"/>
    <br />
      
    <!--呈現結果↓-->
    <div id="result">
     
    
     
     
    </div>
localStorage線上Demo，請使用IE開啟

[http://shadowjapan.blob.core.windows.net/dotblogsshare/ObjSample.html](http://shadowjapan.blob.core.windows.net/dotblogsshare/StringSample.html)

 

sessionStorage線上Demo(出自w3schools網站)：

[http://www.w3schools.com/html/tryit.asp?filename=tryhtml5_webstorage_session](http://www.w3schools.com/html/tryit.asp?filename=tryhtml5_webstorage_session)

體驗生命周期方法↓

image

image

接下來再按鍵盤的Ctrl+N，另開瀏覽器新視窗，再去點擊，次數還是會從1開始算起

整個瀏覽器關閉再重開進入相同網址去點擊，次數也是從1算起

所以應該可以體會 **sessionStorage只存活在單一個分頁**

But，要注意一件事

如果使用**Chrome瀏覽器**的話，當關閉分頁，再按Ctrl+Shift+T鍵把分頁叫回來時

sessionStorage又會復活回來，在IE10不會。

 


最後，使用者Client端瀏覽器也可以自行刪除Web Storage

※我使用的是IE10

image

按「刪除」鈕

image

image

image

image

另外，提一下

image

 

※2014-07-16補充：

使用Google Chrome瀏覽器的人可以在使用到Web Storage的頁面按下F12鍵叫出開發者工具，查看localStorage或sessionStorage的狀況

chromeDemo

 
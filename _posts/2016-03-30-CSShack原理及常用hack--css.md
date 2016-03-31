---
layout: post
title: css hack原理及常用hack
categories:
- CSS
tags:
- CSS
---

css hack原理及常用hack

原理：利用不同浏览器对CSS的支持和解析结果不一样编写针对特定浏览器样式。

常见的hack有

- 属性前缀法(即类内部Hack)：例如 IE6能识别下划线"_"和星号" * "，IE7能识别星号" * "，但不能识别下划线"_"，IE6~IE10都认识"\9"，但firefox前述三个都不能认识。
- 选择器前缀法(即选择器Hack)：例如 IE6能识别*html .class{}，IE7能识别*+html .class{}或者*:first-child+html .class{}。
- IE条件注释法(即HTML条件注释Hack)：针对所有IE(注：IE10+已经不再支持条件注释)： <!--[if IE]>IE浏览器显示的内容 <![endif]-->，针对IE6及以下版本： <!--[if lt IE 6]>只在IE6-显示的内容 <![endif]-->。这类Hack不仅对CSS生效，对写在判断语句里面的所有代码都会生效。
 
CSS hack书写顺序，一般是将适用范围广、被识别能力强的CSS定义在前面。

css hack 并不是标准的css，所以应该尽量少使用hack。

浏览器识别字符标准对比表

![](http://i.imgur.com/38LdPSn.png)

1.大部分特殊字符IE浏览器支持，其他主流浏览器firefox，chrome，opera，safari不支持 (opera可识别除外)。

2.\9    ：所有IE浏览器都支持

3.\_和\-  ：仅IE6支持

4.\*     ：IE6、E7支持

5.\0    ：IE8、IE9支持，opera部分支持

6.\9\0  ：IE8部分支持、IE9支持

7.\0\9  ：IE8、IE9支持

###IE条件注释

说明

- lte：就是Less than or equal to的简写，也就是小于或等于的意思。
- lt ：就是Less than的简写，也就是小于的意思。
- gte：就是Greater than or equal to的简写，也就是大于或等于的意思。
- gt ：就是Greater than的简写，也就是大于的意思。
- ! ：就是不等于的意思，跟javascript里的不等于判断符相同
- 条件注释只能用于Explorer 5+ Windows(以下简称IE)(条件注释从IE5开始被支持)。如果你安装了多个IE，条件注释（Conditional comments）将会以最高版本的IE为标准（目前为IE 7）。
- 条件注释只能在windows Internet Explorer(以下简称IE)下使用，因此我们可以通过条件注释来为IE添加特别的指令。
- 条件注释的基本结构和HTML的注释(<!– –>)是一样的。因此IE以外的浏览器将会把它们看作是普通的注释而完全忽略它们。
- IE将会根据if条件来判断是否如解析普通的页面内容一样解析条件注释里的内容。
- 条件注释使用的是HTML的注释结构，因此他们只能使用在HTML文件里，而不能在CSS文件中使用。

example

    <!– 默认先调用css.css样式表 –>
    <link rel=”stylesheet” type=”text/css” href=”css.css” />
    
    <!–[if IE 7]>
    <!– 如果IE浏览器版是7,调用ie7.css样式表 –>
    <link rel=”stylesheet” type=”text/css” href=”ie7.css” />
    <![endif]–>
    
    <!–[if lte IE 6]>
    <!– 如果IE浏览器版本小于等于6,调用ie.css样式表 –>
    <link rel=”stylesheet” type=”text/css” href=”ie.css” />
    <![endif]–>

那如果当前的浏览器是IE，但版本比IE5还低，该怎么办呢，可以使用<!–[if ls IE 5]>，当然，根据条件注释只能在IE5+的环境之下，所以<!–[if ls IE 5]>根本不会被执行。

###选择器hack：不同浏览器对选择器的支持不一样

语法：
       `<hack> selector{ sRules }`
说明：
 选择不同的浏览器及版本
通常如未作特别说明，所有的代码和示例的默认运行环境都为标准模式。
一些CSS Hack由于浏览器存在交叉认识，所以需要通过层层覆盖的方式来实现对不同浏览器进行Hack的。

/***** Selector Hacks ******/

    /* IE6 and below */
    * html #uno  { color: red }
    
    /* IE7 */
    *:first-child+html #dos { color: red }
    
    /* IE7, FF, Saf, Opera  */
    html>body #tres { color: red }
    
    /* IE8, FF, Saf, Opera (Everything but IE 6,7) */
    html>/**/body #cuatro { color: red }
    
    /* Opera 9.27 and below, safari 2 */
    html:first-child #cinco { color: red }
    
    /* Safari 2-3 */
    html[xmlns*=""] body:last-child #seis { color: red }
    
    /* safari 3+, chrome 1+, opera9+, ff 3.5+ */
    body:nth-of-type(1) #siete { color: red }
    
    /* safari 3+, chrome 1+, opera9+, ff 3.5+ */
    body:first-of-type #ocho {  color: red }
    
    /* saf3+, chrome1+ */
    @media screen and (-webkit-min-device-pixel-ratio:0) {
     #diez  { color: red  }
    }
    
    /* iPhone / mobile webkit */
    @media screen and (max-device-width: 480px) {
     #veintiseis { color: red  }
    }
    
    /* Safari 2 - 3.1 */
    html[xmlns*=""]:root #trece  { color: red  }
    
    /* Safari 2 - 3.1, Opera 9.25 */
    *|html[xmlns*=""] #catorce { color: red  }
    
    /* Everything but IE6-8 */
    :root *> #quince { color: red  }
    
    /* IE7 */
    *+html #dieciocho {  color: red }
    
    /* Firefox only. 1+ */
    #veinticuatro,  x:-moz-any-link  { color: red }
    
    /* Firefox 3.0+ */
    #veinticinco,  x:-moz-any-link, x:default  { color: red  }


###属性hack：不同浏览器解析bug或方法

属性级：

语法：

` selector{<hack>property:value;}`

或者

`selector{property:value<hack>;}`

取值：

\_：选择IE6及以下。连接线（中划线）（-）亦可使用，为了避免与某些带中划线的属性混淆，所以使用下划线（_）更为合适。

\*：选择IE7及以下。诸如：（+）与（#）之类的均可使用，不过业界对（*）的认知度更高

\9：选择IE6+，可以区别所有IE和FireFox。

\0：选择IE8+和Opera

[;property:value;];：选择webkit核心浏览器（Chrome,Safari）。IE7及以下也能识别。中括号内外的3个分号必须保留，第一个分号前可以是任意规则或任意多个规则

[;color:#f00;]; 与 [color:#f00;color:#f00;]; 与 [margin:0;padding:0;color:#f00;]; 是等价的。生效的始终是中括号内的最后一条规则，所以通常选用第一种写法最为简洁。

注意：!important并不是一个hack手段，他是被用来改变css的优先级的，因为ie6是不识别!important,所以就被拿来当做css hack的一种，这是错误的。
　　　
说明：
　　　　
选择不同的浏览器及版本
浏览器优先级别:FF<IE9<IE8<IE7<IE6,CSS hack书写顺序一般为FF IE9 IE8 IE7 IE6
一些CSS Hack由于浏览器存在交叉认识，所以需要通过层层覆盖的方式来实现对不同浏览器进行Hack的。
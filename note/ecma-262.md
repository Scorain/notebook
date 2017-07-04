
# ECMAScript® 2016 语言规范

## 导论

## 1.适用范围

此标准定义ECMAScript 2016通用编程语言


## 2.一致性


一个符合标准的ECMAScript实现必须提供和支持此规范中对类型、值、对象、属性、函数和程序语法与语义的描述。

一个符合标准的ECMAScript实现必须将源文本输入解释为与Unicode,V8.0.0(及之后版本)和ISO/IEC 10646一致。

一个符合标准、提供应用程序接口（供需要适应不同语言和国家的语言和文化惯例的程序使用）的ECMAScript实现必须实现与此规范兼容的ECMA-402最近版本中定义的接口。

一个符合标准的ECMAScript实现可以提供此标准描述以外的类型、值、对象、属性、和函数。尤其，一个符合标准的ECMAScript实现可以为此规范中描述的对象提供此规范中未描述的属性，并且为那些属性赋值。

一个符合标准的ECMAScript实现可以支持此规范中未描述的指令和常规表达式语法。尤其，一个符合标准的ECMAScript实现可以支持使用了此规范11.6.2.2子条目中的‘将来保留字’列表中的保留字的程序语法。

一个符合标准的ECMAScript实现必须没有实现16.2子条目中被禁止的扩展。


## 3.引用标准


下面列出的参考文档对于此文档的应用是不可或缺的。对于已经过时的参考，只有锁定的版本适用。对于不知是否过时的参考，最近版本的参考文档（包含一些修正）适用。

ISO/IEC 10646:2003: Information Technology – Universal Multiple-Octet Coded Character Set (UCS) plus Amendment 1:2005, Amendment 2:2006, Amendment 3:2008, and Amendment 4:2008, plus additional amendments and corrigenda, or successor

ECMA-402, ECMAScript 2015 Internationalization API Specification. 
<http://www.ecma-international.org/publications/standards/Ecma-402.htm>

ECMA-404, The JSON Data Interchange Format. 
<http://www.ecma-international.org/publications/standards/Ecma-404.htm>


## 4.总览


此部分包含一个ECMAScript语言的不标准的概述。

ECMAScript是一种在宿主环境中执行计算和控制计算对象的面向对象程序语言。此处定义的ECMAScript并不是计算性自完备的；事实上，此规范中并不涉及外部数据输入和计算结果输出的规定。相反，我们期望ECMAScript程序的计算环境不仅提供本规范描述的对象和设备，还能提供某些特定环境下的宿主对象；除非为了说明宿主对象可能提供某些属性和方法以供ECMAScript程序访问，这些宿主对象的描述和行为都超出了本规范的范围。

ECMAScript最初被设计用于脚本语言，但已经变成了被广泛使用的通用编程语言。脚本语言是用于操作、定制和自动化已存在系统的设备的编程语言。在那些系统中，有用的功能可以通过用户接口获得，脚本语言是一种暴露程序控制功能的机制。这样，已存在系统提供对象和设备的宿主环境，完善脚本语言的能力。脚本语言意图被专业和非专业的程序员使用。

ECMAScript最早被设计为一种用于web的脚本语言，它提供一种机制，使浏览器中的网页更加活跃、为基于web的C/S架构提供服务器计算能力。ECMAScript现在为各种各样的宿主环境提供核心脚本能力。因此，不依赖于宿主环境的核心语言部分由本文档指明。

ECMAScript的使用已经超出简单脚本的范畴，它现在已经在不同的环境和领域用于全方位的编程任务。随着ECMAScript使用的扩展，它提供的特性和机能也在不断的扩展。ECMAScript现在已经是一种特性丰富的通用编程语言。

ECMAScript的一些机能与其他编程语言类似；如C、Java、Self和Scheme:

ISO/IEC 9899:1996, Programming Languages – C.

Gosling, James, Bill Joy and Guy Steele. The Java™ Language Specification. Addison Wesley Publishing Co., 1996.

Ungar, David, and Smith, Randall B. Self: The Power of Simplicity. OOPSLA '87 Conference Proceedings, pp. 227-241, Orlando, FL, October 1987.

IEEE Standard for the Scheme Programming Language. IEEE Std 1178-1990.


### 4.1 Web脚本

浏览器提供ECMAScript客户端计算宿主环境，包括代表如windows,menus,pop-ups,dialog boxes,text areas,anchors,frames,history,cookies,input/output等的对象。随后，这个宿主环境提供将脚本代码绑定到诸如焦点改变、页面图片加载卸载错误取消，选择框表单提交和鼠标动作等事件上的途径。


## 5.符号约定

## 6.数据类型和值

## 7.抽象操作

## 8.可执行代码和执行上下文

## 9.内在对象和引用对象的行为

## 10.源代码

## 11.词法语法

## 12.表达式

## 13.声明

## 14.函数和类




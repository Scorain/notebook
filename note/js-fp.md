
## 第一章 JavaScript函数式编程简介

本章是本书后续内容的基础。本章将介绍什么是underscore以及如何开始使用它；除此之外，也将对后续用到的术语和本书的目标进行解释。

#### 1.1 javascript案例

“为什么选择JavaScript”，这个问题的答案很简单：灵活。换句话说，或许除了Java，目前没有比JavaScript更加流行的语言了。所有的浏览器以及现有新兴技术的大范围支持，使得JavaScript成了满足可移植性的不错的选择，甚至是唯一的选择。
随着客户端服务和单页布局应用架构的再度出现，JavaScript越来越广泛地应用于附加在大量网络服务中的分离式应用当中（如单页布局）。比如所有的谷歌应用程序都由JavaScript编写，这也是单页布局应用的范例。
如果在学习JavaScript之前，你已对函数式编程有所研究，那么好消息是javascript“天然”支持函数式技术（例如：函数是javascript的一个核心概念）。举个例子：
```
[1,2,3].forEach(alert);
```
数组的forEach方法接收一个函数，并将数组中的每一个元素依次交给该函数执行。除此之外，javascript提供大量的能够以其他函数为参数的方法和函数。在本书的后续中，将进一步介绍。

javascript有坚实的语言原语基础。从函数、闭包、原型，到相当不错的动态核心，javascript提供了一系列非常好用的工具集。此外，javascript也提供了一种非常开放和灵活的执行模型。如：所有的javascript函数都有一个apply方法，使得我们可以用一个数组来调用函数，其中，数组的元素作为函数的参数。使用apply，可以创建一个名为splat的函数。它接收一个函数fun,并返回另一个函数，该函数接收一个数组并用apply来执行函数fun。这样一来，传入函数splat的数组的元素是函数fun的参数：
```
function splat(fun) {
	return function(array) {
		return fun.apply(null,array);
	}
}
var addArrayElements = splat(function(x,y){return x+y});
addArrayElements([1,2]);
```
这是我们函数式编程的初试-一个返回函数的函数-待会再来仔细的研究。
另外一个展现javascript灵活性的地方是，我们可以随时以任意多个任意类型的参数来调用任意一个函数。我们可以创建一个与splat功能相反的函数unsplat，它接受一个函数fun并返回另一个接受任意多个参数的函数，将参数转为数组传给fun并调用它：
```
function unsplat(fun){
	return function(){
		return fun.apply(null,arguments);
	};
}
var joinElements = unsplat(function(array){return array.join(' ')});
joinElements([1,2]);
```
每个函数都可以访问一个名叫arguments的局部对象，它以类似于数组的形式储存了调用本函数时的实际参数。arguments非常强大，并能够产生惊人的效果。另外，call可以看作apply的改变入参形式的语法糖。apply,call,arguments的同时存在只是javascript强大而灵活的一个小例子。
随着用javascript来创建各种规模应用的趋势，你可能会担心该语言本身发展及其运行时支持会停滞不前。但随意阅读一下ECMAScript会发现javascript在不断的发展中。

**javascript的一些局限**
从javascript的出现、演变、发展到普及来讲，javascript的局限性很小。但我们要承认javascript是一门存在缺陷的语言：语言古怪、不安全、第三方库相互竞争等。


#### 1.2 开始函数式编程

下面一句话可以直白的描述函数式编程：
>函数式编程通过使用函数来将值转换成抽象单元，接着用于构建软件系统

###### 1.2.1 为什么函数式编程很重要

如果你熟悉面向对象编程，那么你可能会同意它的主要目标是问题分解。相比较而言，用严格的函数式编程的方法来解决问题，也会将一个问题分成几部分来解决。与面向对象方法将问题分解成多组“名词”或对象不同，函数式方法将相同的问题分解成多组“动词”或函数。与面向对象编程类似的是，函数式编程也通过“黏接”或“组合”其他函数的方式来构建更大的函数，以实现更加抽象的行为。一种将函数式的部件组成一个完整的系统的方法是取一个值，逐渐的将它“改变”-通过一个原始的或组合的函数-成另一个值。
在一个面向对象系统的内部，对象间的交互会引起各个对象内部状态的变化，而整个系统的状态转变则是由许许多多小的、细微的状态变化混合而形成的。这些相互关联的状态变化形成了一个概念上的“变化网”，我们是不是会因为它而感到困惑。当需要了解其带来的微妙且广泛的状态变化时，这种困惑就会成为一个问题。
相比之下，函数式系统则努力减少可见的状态修改。因此，向一个遵循函数式原则的系统添加新功能就成了理解如何在存在局限的上下文环境中-无破坏性的数据转换-来实现新的函数。然而，我们并不愿意在函数式风格和面向对象风格之间画一条明显的界限，说它们应该是对立关系。一个系统中可以由这两种模式共同组成。

###### 1.2.2 以函数为抽象单元

抽象方法是指隐藏了实现细节的函数。事实上，函数是一种非常好的工作单元，它使得我们能够坚持如下说法：

>使之运行，使之正确，使之快速

>使之运行，再使之正确，再使之快速

例如，对于错误和警告的报告，我们可以写出如下代码：
```
function parseAge(age) {
	if(!_.isString(age)) throw new Error("expecting a string");
	var a;
	console.log("Attemting to parse an age");
	a = parseInt(age,10);
	if(_.isNaN(a)){
		console.log(["could not parse age:",age].join(" "));
		a = 0;
	}
	return a;
}
```
虽然这个函数并不能全面地解析年龄字符串，但确是一个好例子。我们可以用如下的方法来调用parseAge:
```
parseAge("42");
parseAge(42);
parseAge("frob");
```
parseAge函数工作正常，但如果我们想要修改输出错误、信息和警告呈现的方式，那么就需要修改相应的代码行，以及其他地方的类似输出模式。一个较好的方法是将错误、信息和警告的概念抽象成不同的函数：
```
function fail(thing){
	throw new Error(thing);
}
function warn(thing){
	console.log(["warning:",thing].join(" "));
}
function note(thing){
	console.log(["note:",thing].join(" "));
}
```
有了这些函数。我们就可将parseAge函数改写成：
```
function parseAge(age){
	if(!_.isString(age)) fail("expecting a string");
	var a;
	note("attempting to parse an age");
	a=parseInt(age,10);
	if(_.isNaN)(a){
		warn(["could not parse age:",age].join(" "));
		a=0;
	}
	return a;
}
```
调用新函数与调用旧函数相比结果一样，但新函数的提示呈现被抽象化了，更有利于后期的变化。

###### 1.2.3 封装和隐藏

多年来，我们一直被教导说封装是面向对象的基石。javascript提供了一个对象系统，它能够封装数据和操作。然而，有时封装被用来限制某些元素的可见性，称为数据的隐藏。在javascript的对象系统中，并没有提供直接隐藏数据的方式，因此使用一种叫做闭包的方式来隐藏数据。

###### 1.2.4 以函数为行为单位

隐藏数据和行为只是一种将函数作为抽象单元的方式。另外一种方式是提供一种简单的存储和传递基本行为的离散单元。举个例子，用javascript语法来索引数组中的一个值：
```
var letters=['a','b','c'];
letters[1];
```
虽然数组索引是javascript的一个核心行为，但并没有办法可以在不把它放到函数里的前提下，获取这个行为并根据需要来使用它。因此，举一个函数的简单例子就是抽象数组索引行为，我们称之为nth。其简单实现如下：
```
function(a,index){
	return a[index];
}
```
或许正如你所想，nth的主逻辑工作正常，然而，当传入意想不到的值时，就会报错。
另外一个javascript的基本行为单元是比较器。比较器是一个函数，他接收两个参数，如果第一个参数小于第二个参数值，则返回<1，大于返回>1,等于返回0.事实上，javascript本身似乎可以利用数字本身的性质，提供一个默认的sort方法：
```
[2,3,1,-4,87].sort();
```
但如下情况会出错：
```
[2,4,99,5,-1,9,-108].sort();
```
问题在于，在没有给定参数的情况下，数组的sort方法执行字符串的比较。如果换成如下的写法：
```
[2,4,99,5,-1,9,-108].sort(function(x,y){
	return x-y;
});
```
现在就可以正确的比较数值了。此时，sort方法可以根据其入参函数返回值的正负来判断是否交换x、y的位置。但是，这里做一个假设，假设sort方法的执行过程中无法识别正负，只能识别-1、0、1这三个值呢！就得对sort的入参函数进行进一步的处理：
```
function pred(x,y){
	return x-y;
}
function comparator(pred){
	return function(x,y){
		if(pred(x,y)>0){
			return 1;
		}else if(pred(x,y)<0){
			return -1;
		}else{
			return 0;
		}
	};
}

[2,4,99,5,-1,9,-108].sort(comparator(pred));
```
上例中pred、comparator分别为两个不同的行为单元，它们不仅可以用于sort方法，还可以单独使用。

###### 1.2.5 数据抽象


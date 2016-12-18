## underscore

### underscore源码结构

#### 整体架构

```
(function(){
	/*保存执行上下文*/
	var root = this;
	/*定义underscore变量*/
	var _ = function(obj){...};
	/*不同的模块加载方式输出underscore*/
	if (typeof exports !== 'undefined') {
		if (typeof module !== 'undefined' && module.exports) {
			exports = module.exports = _;
		}
		exports._ = _;
	} else {
		root._ = _;
	}
	if (typeof define === 'function' && define.amd) {
		define('underscore',[],function(){return _;});
	}
}.call(this))
```

#### 获取ECMA原生方法

```
var ArrayProto = Array.prototype,
	ObjProto = Object.prototype,	
	FuncProto = Function.prototype;	
var push = ArrayProto.push,
	slice = ArrayProto.slice,	
	toString = ObjProto.toString,
	hasOwnProperty = ObjProto.hasOwnProperty;
var nativeIsArray = Array.isArray,
	nativeKeys = Object.keys,
	nativeBind = FuncProto.bind,
	nativeCreate = Object.create;
```

数组push方法：
```
//@params pushItem 压栈项
//@return {Number} 新集合长度
collections[length] = pushItem;
return collection['length'] += 1;
```

数组slice方法
```
//@params begin 起始索引
//@params end 终止索引
//@return {Array} 新数组
var res = [];
for(var index = begin;index < end;index++) {
	res.push(collections[index]);
}
return res;
```

对象的toString方法
```
//@return {String} 对象的字符串描述
toString.call(new Object()); // '[object Object]'
toString.call(new Array()); // '[object Array]'
toString.call(new Function()); // '[object Function]'
toString.call(new RegExp()); // '[object RegExp]'
```

对象的hasOwnProperty方法
>判断对象是否含有属性，查找不可遍历属性，不查找原型链

对象的keys工具方法
>返回键数组，不包含不可遍历属性，不包含原型链

#### 创建裸函数
```
var Ctor = function(){};
```

#### Underscore定义
```
var _ = function(obj) {
	if (obj instanceof _) return obj;
	if (!(this instanceof _)) return new _(obj);
	this._wrapped = obj;
}
```

#### 改变函数的执行上下文
```
var optimizeCb = function(func,context,argCount) {
	//不改变函数的执行上下文
	if (context === viod 0) return func;
	//函数有1~4个入参
	switch (argCount == null ? 3 : argCount) {
		case 1: return function(value) {
			return func.call(context,value);
		};
		case 2: return function(value,index) {
			return func.call(context,value,index);
		};
		case 3: return function(value,index,collection) {
			return func.call(context,value,index,collection);
		};
		case 4: return function(accumulator,value,index,collection) {
			return func.call(context,accumulator,value,index,collection);
		};
	}
	//函数有不定个入参
	return function(){
		return func.apply(context,arguments);
	};
}
```

#### 回调函数生成
```
var cb = function(value,context,argCount) {
	if (value == null) return _.identity;
	if (_.isFunction(value)) return optimizeCb(value,context,argCount);
	if (_.isObject(value)) return _.matcher(value);
	return _.property(value);
}
```

#### 继承的原型实现
```
var baseCreate = function(prototype) {
	if (!_.isObject(prototype)) return {};
	if (nativeCreate) return nativeCreate(prototype);
	Ctor.prototype = prototype;
	var result = new Ctor();
	Ctor.prototype = null;
	return result;
}
```

#### 获取对象的属性的方法
```
var property = function(key) {
	return function(obj) {
		return obj == null ? void 0 : obj[key];
	}
}
```

#### 类数组对象的判断
```
var MAX_ARRAY_INDEX = Math.pow(2,53) - 1;
var getLength = property('length');
var isArrayLike = function(collection) {
	var length = getLength(collection);
	return typeof length == 'number' && length >=0 && length <= MAX_ARRAY_INDEX;
}
```
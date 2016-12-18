## underscore

### underscoreԴ��ṹ

#### ����ܹ�

```
(function(){
	/*����ִ��������*/
	var root = this;
	/*����underscore����*/
	var _ = function(obj){...};
	/*��ͬ��ģ����ط�ʽ���underscore*/
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

#### ��ȡECMAԭ������

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

����push������
```
//@params pushItem ѹջ��
//@return {Number} �¼��ϳ���
collections[length] = pushItem;
return collection['length'] += 1;
```

����slice����
```
//@params begin ��ʼ����
//@params end ��ֹ����
//@return {Array} ������
var res = [];
for(var index = begin;index < end;index++) {
	res.push(collections[index]);
}
return res;
```

�����toString����
```
//@return {String} ������ַ�������
toString.call(new Object()); // '[object Object]'
toString.call(new Array()); // '[object Array]'
toString.call(new Function()); // '[object Function]'
toString.call(new RegExp()); // '[object RegExp]'
```

�����hasOwnProperty����
>�ж϶����Ƿ������ԣ����Ҳ��ɱ������ԣ�������ԭ����

�����keys���߷���
>���ؼ����飬���������ɱ������ԣ�������ԭ����

#### �����㺯��
```
var Ctor = function(){};
```

#### Underscore����
```
var _ = function(obj) {
	if (obj instanceof _) return obj;
	if (!(this instanceof _)) return new _(obj);
	this._wrapped = obj;
}
```

#### �ı亯����ִ��������
```
var optimizeCb = function(func,context,argCount) {
	//���ı亯����ִ��������
	if (context === viod 0) return func;
	//������1~4�����
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
	//�����в��������
	return function(){
		return func.apply(context,arguments);
	};
}
```

#### �ص���������
```
var cb = function(value,context,argCount) {
	if (value == null) return _.identity;
	if (_.isFunction(value)) return optimizeCb(value,context,argCount);
	if (_.isObject(value)) return _.matcher(value);
	return _.property(value);
}
```

#### �̳е�ԭ��ʵ��
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

#### ��ȡ��������Եķ���
```
var property = function(key) {
	return function(obj) {
		return obj == null ? void 0 : obj[key];
	}
}
```

#### �����������ж�
```
var MAX_ARRAY_INDEX = Math.pow(2,53) - 1;
var getLength = property('length');
var isArrayLike = function(collection) {
	var length = getLength(collection);
	return typeof length == 'number' && length >=0 && length <= MAX_ARRAY_INDEX;
}
```
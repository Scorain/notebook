# js隐式类型转换

> &copy; suny 2017-03-29 18:00


### 相关操作

+ 算数运算符 `-` `*` `/` `%`

+ 比较运算符 `==`

+ 加法 （一元加号运算符 & 连字符） `+`

### 相关方法

+ ToPrimitive (内部方法，引擎调用 toPrimitive)

+ ToNumber (引用类型中为 valueOf)

+ ToString (引用类型中为 toString)

### 转化为原始值

在隐式类型转换中，[[toPrimitive]]方法将某个值转化为原始类型的值。此方法接受两个参数：`input` `preferredType`分别为 `需要转化的值` 和 `转化偏好`；可选参数`preferredType`只接受 `string` `number` 两个值且默认为 `number`。当某个`input`转化成原始值时有不同的选择时，`preferredType`将起到决定性作用：

1. `preferredType` 为 `number` ： 先对`input`调用 `valueOf`，若值不为原始值，则接着调用 `toString`，还不是的话则抛出错误

2. `preferredType` 为 `string` ： 先对`input`调用 `toString`，若值不为原始值，则接着调用 `valueOf`，还不是的话则抛出错误

> 用户可以自定义 `toPrimitive` 方法重写这个行为

### 算数运算符

对于算数运算符 `-` `*` `/` `%`，左右两边的云算子若不为数值，js会自动将其转化为数值，然后进行计算。

对于 `+` 运算符，由于其还可以表示连字符，这里先不讨论，后续单独分析。

### 比较运算符

比较运算符中，涉及到隐式类型转换的是 非严格相等比较符 `==`。

`x == y` 的结果由如下规则决定：

    1. 如果 Type(x) 与 Type(y) 相同，则返回 `x === y` 的结果
    2. 如果 x 为 null 且 y 为 undefined ，返回 true
    3. 如果 x 为 null 且 y 为 undefined ，返回 true
    4. 如果 Type(x) 为 Number 且 Type(y) 为 String，返回 `x === ToNumber(y)` 
    5. 如果 Type(x) 为 String 且 Type(y) 为 Number，返回 `ToNumber(x) === y` 
    6. 如果 Type(x) 为 Boolean，返回 `ToNumber(x) === y` 
    7. 如果 Type(y) 为 Boolean，返回 `x === ToNumber(y)`
    8. 如果 Type(x) 为 String，Number 或 Symbol 且 Type(y) 为 Object，返回 `x === ToPrimitive(y)` 
    9. 如果 Type(x) 为 Object 且 Type(y) 为 String，Number 或 Symbol，返回 `ToPrimitive(x) === y` 
    10. 返回 false

### 加号 & 连字符

终于到了 `+` ，js中在进行加法运算时，按如下步骤：

    1. 首先把加号左右两边进行求原值ToPrimitive()操作
    2. 若两个原值中存在String类型，则分别对其进行ToString()操作，此时为字符串拼接
    3. 否则对两个原值进行ToNumber()操作，此时为数字相加



**参考文献**

- [ECMAScript® 2016 Language Specification](https://www.ecma-international.org/ecma-262/7.0/#sec-unary-plus-operator)

- [js隐式装箱-ToPrimitive](https://sinaad.github.io/xfe/2016/04/15/ToPrimitive/)
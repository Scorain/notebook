## form & table

### 表单

>1.form

attribute:action、method、enctype

>2.label

attribute:for

>3.input

attribute:type、name、value、placeholder、readonly、disabled、required、multiple、maxlength

>4.select

attribute:name、multiple

>5.option

attribute:value、selected

>6.textarea

attribute:name、rows、cols、placeholder、readonly、required、disabled  
  
### 表格

>1.table

>2.tr

>3.th/td

### 页面框架

>1.iframe

attribute:src、frameborder、scrolling

### UI框架

>[EasyUI](http://www.jeasyui.com/)适用于**后台管理系统**的前端界面（表单、表格数据交互繁多）

#### datagrid布局 **EasyUI中最重要的组件**

```
<!--HTML文件-->
<table id="dg" style="width:100%;"></table>
```

```
/*js文件*/
$("#dg").datagrid(options)

$("#dg").datagrid(method,args)
```

###### 属性
|属性名   |值类型   |属性描述   |
|-----   |-----   |----------   |
|culumns   |Array   |二维数组，表字段集合   |
|url   |String   |从后台拉取数据的地址   |
|data   |Array   |列表中的数据[{field:value}]   |
|idField   |String   |指明哪一个字段是标识字段   |
|singleSelect   |Boolean   |是否只允许选择一行   |
|method   |String   |远程请求数据的方法   |
|queryParams   |Object   |远程请求数据时的入参   |
|loadFilder   |Function   |将远程数据处理为标准数据对象{total:100,rows:[{field:value}]}   |
|editors   |Object   |定义编辑时用的编辑器   |
|...   |...   |...   |

###### 事件
|事件名   |入参   |事件描述   |
|-----   |-----   |----------   |
|onClickRow   |rowIndex,rowData   |用户单击行时触发   |
|onClickCell   |rowIndex,field,value   |用户单击单元格时触发   |
|onSelect   |rowIndex,rowData   |用户选择一行时触发   |
|onUnselect   |rowIndex,rowData   |用户取消选择一行时触发   |
|...   |...   |...   |

###### 方法
|方法名   |入参   |方法描述   |
|-----   |-----   |----------   |
|beginEdit   |index   |开始编辑行   |
|endEdit   |index   |结束编辑行   |
|selectRow   |index   |选择一行   |
|unselectRow   |index   |取消选择一行   |
|...   |...   |...   |


###### 列属性
|列属性名   |值类型   |列属性描述   |
|-----   |-----   |----------   |
|field   |String   |列字段   |
|title   |String   |列标题   |
|editor   |String,Object   |指明编辑类型   |
|...   |...   |...   |


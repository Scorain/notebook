## form & table

### ��

>1.form

attribute:action��method��enctype

>2.label

attribute:for

>3.input

attribute:type��name��value��placeholder��readonly��disabled��required��multiple��maxlength

>4.select

attribute:name��multiple

>5.option

attribute:value��selected

>6.textarea

attribute:name��rows��cols��placeholder��readonly��required��disabled  
  
### ���

>1.table

>2.tr

>3.th/td

### ҳ����

>1.iframe

attribute:src��frameborder��scrolling

### UI���

>[EasyUI](http://www.jeasyui.com/)������**��̨����ϵͳ**��ǰ�˽��棨����������ݽ������ࣩ

#### datagrid���� **EasyUI������Ҫ�����**

```
<!--HTML�ļ�-->
<table id="dg" style="width:100%;"></table>
```

```
/*js�ļ�*/
$("#dg").datagrid(options)

$("#dg").datagrid(method,args)
```

###### ����
|������   |ֵ����   |��������   |
|-----   |-----   |----------   |
|culumns   |Array   |��ά���飬���ֶμ���   |
|url   |String   |�Ӻ�̨��ȡ���ݵĵ�ַ   |
|data   |Array   |�б��е�����[{field:value}]   |
|idField   |String   |ָ����һ���ֶ��Ǳ�ʶ�ֶ�   |
|singleSelect   |Boolean   |�Ƿ�ֻ����ѡ��һ��   |
|method   |String   |Զ���������ݵķ���   |
|queryParams   |Object   |Զ����������ʱ�����   |
|loadFilder   |Function   |��Զ�����ݴ���Ϊ��׼���ݶ���{total:100,rows:[{field:value}]}   |
|editors   |Object   |����༭ʱ�õı༭��   |
|...   |...   |...   |

###### �¼�
|�¼���   |���   |�¼�����   |
|-----   |-----   |----------   |
|onClickRow   |rowIndex,rowData   |�û�������ʱ����   |
|onClickCell   |rowIndex,field,value   |�û�������Ԫ��ʱ����   |
|onSelect   |rowIndex,rowData   |�û�ѡ��һ��ʱ����   |
|onUnselect   |rowIndex,rowData   |�û�ȡ��ѡ��һ��ʱ����   |
|...   |...   |...   |

###### ����
|������   |���   |��������   |
|-----   |-----   |----------   |
|beginEdit   |index   |��ʼ�༭��   |
|endEdit   |index   |�����༭��   |
|selectRow   |index   |ѡ��һ��   |
|unselectRow   |index   |ȡ��ѡ��һ��   |
|...   |...   |...   |


###### ������
|��������   |ֵ����   |����������   |
|-----   |-----   |----------   |
|field   |String   |���ֶ�   |
|title   |String   |�б���   |
|editor   |String,Object   |ָ���༭����   |
|...   |...   |...   |


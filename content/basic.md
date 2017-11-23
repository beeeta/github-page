Title: python read api doc note 1
Date: 2017-11-23
Category: python

### 基本数据类型的转换

- 数值 --> 字符串(将数值转为特定进制的字符串形式)  
```
bin()
oct()
hex()
```

- 字符串 --> 数字
```
int('[0b,0o,0x]xxx',[2,8,16])
```
	
- 集合类型之间的转换  
``` 
list  -->   [(1,2),(2,3),(3,4)]	
     enumerate()
	 zip()
dict -->   [(),(),()]
	list(dict.items())
	
[(),(),()]  --> dict
    {i:j for i,j in [(),(),()]}
```
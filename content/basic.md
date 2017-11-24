Title: python api阅读笔记1
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

---

### python中的时间

#### datetime
- 创建time对象，date对象和datetime对象
```
datetime.time(16,26,56)
datetime.date(2017,20,20)
datetime.datetime(2017,20,20)
```
- 当前时间
```
datetime.time.now()
datetime.date.today()
datetime.datetime.now()
```
- 时间单位的转化
```
datetime.date <- datetime.datetime.date()
datetime.time <- datetime.datetime.time()
datetime.datetime <- [datetime.datetime](object).combine(datetime.date(obj),datetime.time(obj))
```
- 时间的运算和平移
```
datetime2 = datetime +_ timedelta
timedelta = datetime _ datetime
```
- 字符时间的创建与打印  
创建：
```
datetime.datetime.strptime('2017-09-09','%Y-%m-%d')
```
打印：
```
[datetime.datetime](object).strftime()
```

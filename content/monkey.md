Title: monkey patch
Category: python
Date: 2017-12

### 基础
> python的一种编程技巧。之后引入的包可以改变之前引入包的方法，主要可用于对第三方包进行定制。例子可以参考[requests-cache](https://github.com/reclosedev/requests-cache.git)和[gevent](https://github.com/gevent/gevent.git)源码

- 一个简单的例子

test.py
```python
import test2
import test3

test2.abc()

```

test2.py
```
def abc():
    print('test2 abc')
```

test3.py
```
import test2

# old_abc = test2.abc

test2.abc = lambda :print('monkeyed abc')

```

结果打印为：

```
monkeyed abc
```

- 深入一些的技巧
> 借助python的内省和魔法方法做的更pythonic





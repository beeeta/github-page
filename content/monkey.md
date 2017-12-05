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

```python
monkeyed abc
```
- 实现的原理  

一个模块中导入的其他模块，内置模块及其他模块中依赖的模块，都通过这个模块的命名空间来维护，所有的模块实质上只会导入一次，
模块多次在不同地方导入时，操作的是同一个模块对象


- 深入一些的技巧
> 借助python的内省和魔法方法做的更pythonic





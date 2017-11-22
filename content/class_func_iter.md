Title: python使用类和函数创建迭代器的几种方法
Date: 2017-11
Category: python


```python
"""
将类和函数改造为迭代器的方法

"""

# 1.实现了__iter__,__next__方法的类
class Iter(object):
    def __init__(self):
        self.age = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.age >4 :
            raise StopIteration
        else :
            rs = self.age
            self.age += 1
            return rs


# 2.使用原生的迭代器
def iterer():
    for i in range(5):
        yield  i

# 3.将闭包函数改造为迭代器iter(为什么要是闭包函数，因为每次调用有状态变化)
def outer():
    a = 0
    def inner():
        nonlocal a
        if a>4:
            return None
        else:
            b = a
            a += 1
            return b
    return inner

out = iter(outer(),None)

# Test
if __name__ == '__main__':
    iter1 = Iter()
    iter2 = iterer()
    iter3 = out
    for i in iter1:
        print('iter1 print:{}'.format(i))

    print('---------')
    for j in iter2:
        print('iter2 print:{}'.format(j))

    print('---------')
    for k in iter3:
        print('iter3 print:{}'.format(k))

```

三种方式执行的结果相同：
---
![执行结果图]({filename}/images/result1.png)

Title: 多线程与多进程
Category: python
Date: 2017-12

### 多线程和多进程的创建

两者的创建方式类似的，导入的包不同，都可以通过继承和挂载线程方法来实现

```python
from threading import Thread
from multiprocessing import Process

class Worker(Thread)
    def __init__(self):
        pass
    def run(self):
        print('do worker job')

worker = Worker()
worker.start()

thread = Thread(target=jobfunc,args=None) # 这种方式更方便
thread.start()
	
```

### 调用命令行命令
```python
from subprocess import call,Popen
call('ls -al')
call(['ls','-al'],shell=True)


```



Title: 多线程与多进程
Category: python
Date: 2017-12

> 主要关注创建进程线程的方法，进程线程之间的通信同步方法，Queue,进程池线程池

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

ret = Popen(['ls','-al'],stdout=PIPE,stderr=PIPE)
out, err = ret.communicate()


```

### 线程之间的同步机制
- Lock
```python
from threading import Lock
lock = Lock()

lock.acquire()
# do something
lock.release()

with lock:
    # do something

```

- RLock
```python
from threading import RLock
lock = RLock()
# 对多个代码段加锁，防死锁的一种方式
lock.acquire()
# do something
lock.release()

with lock:
    # do something

```

- Semaphore
信号量，控制获取资源的线程数量
```python
sema = Semaphore(3)
with sema:
    # do something
    # 只能由三个线程同时进来
```

- Event
```
e = Event()
e.wait()

e.set() # 在e.set()方法未执行之前e.wait()方法会被阻塞

```

- 三种Queue
```python
Queue,deque

PriorityQueue

class PriorityQueue(object):
    def __init__(self):
        self._q = []
        self._count = 0
        self._cv = threading.Condition()

    def __str__(self):
        return str(self._q)

    def __repr__(self):
        return self._q

    def put(self, item, priority):
        with self._cv:
            heapq.heappush(self._q, (-priority,self._count,item))
            self._count += 1
            self._cv.notify()

    def pop(self):
        with self._cv:
            while len(self._q) == 0:
                print("wait...")
                self._cv.wait()
            ret = heapq.heappop(self._q)[-1]
        return ret

```

### 线程池进程池
```python
from concurrent.futures import ThreadPoolExecutor,ProcessPoolExecutor

with ThreadPoolExecutor(3) as e:
    # 单独提交任务
    fut = e.submit(fib, 30)
    res = fut.result()
    print(res)
    # 或使用map函数
    with futures.ProcessPoolExecutor(2) as e:
       res = e.map(fib, [35]*2)
       for _ in res:
           print(_)

```




cmdb

b站地址：https://www.bilibili.com/video/BV11Z4y1s79H?p=11&t=71

![image-20201108175826880](/Users/yutang/Library/Application Support/typora-user-images/image-20201108175826880.png)

cmdb主要是通过获取监测的服务器中的信息，上报给平台进行展示。

paramiko实现获取服务器信息



### 1.为什么要开发cmdb？

```
目的是想要搭建运维自动化平台，减少人工干预降低人员成本。构建自动化平台要以资产核心，目前的服务器资产信息都是保存在excel中，不便于管理（数据越来与不准确），希望开发一套自动化采集的系统。
```

### 2.如何实现cmdb？

```
cmdb项目由三大部分组成，其中包括：中控机、API平台、资产管控平台。

中控机：基于parammiko实现SSH远程连接服务器，并且可以对服务器进行远程操作。利用中控机批量采集资产信息，并将资产信息结构化处理之后，将数据通过requests调用API接口保存到数据库总。在开发插件的过程中，基于工厂模式实现插件可扩展性。

API：获取中控机提供的资产数据并进行资产变更处理，它还可以为其他第三方提供数据接口。

资产监控平台：为运维人员或运维主管提供资产管理及数据报表统计。
```

### 3.为什么不直接连接数据库？而使用API？

```
直接连接数据库导致数据不安全（数据库密码会暴露）
并且如果数据库密码更新，需要通过很多地方都要更新
搭建API的平台，专门提供API服务
```

### 4.使用类的继承实现约束子类中必须要实现某个方法

### 5.线程池

```python
import time
from concurrent.futures import ThreadPollExecutor

def task(i):
  time.sleep(1)
  print(i)
  
pool = ThreadPollExecutor(10)

for i in range(87):
  pool.submit(task, i)
```

### 6.什么是反射？

```
通过字符串的形式去操作对象中的成员。
		getattr
		setattr
		delattr
		hasattr
		
应用场景：
	cmdb插件的可扩展
	Django的中间件
```

### 7.可扩展插件如何实现

```
1.把所有插件都定义到类中并且通过基类+异常进行约束，必须包含process方法
2.将类的路径注册到配置文件中
3.根据字符串的形式导入模块（importlib），并且基于反射找到类，然后实例化并执行它的process方法。
工厂模式
```

### 8.工厂模式

```
简单工厂、工厂方法、抽象工厂
```

### 9.开发封闭原则

```
对修改原码封闭，对配置文件开放
```

### 10.paramiko模块

### 11.content-type请求头

```
get、post中没有值时，去request.body中获取数据
```

### 12.单例模式

```python
import threading


class Singleton(object):
    instance = None  # 静态字段，类变量
    # 记录是否执行过初始化动作
    init_flag = False
    lock = threading.RLock()

    def __init__(self, name):
        """
        初始化对象
        :param name:
        """
        # 单例初始化方法只能执行一次
        if Singleton.init_flag:
            return
        self.name = name
        # 修改类属性得标记
        Singleton.init_flag = True

    def __new__(cls, *args, **kwargs):
        """
        创建对象,分配空间
        :param args:
        :param kwargs:
        """
        if cls.instance:
            return cls.instance
        with cls.lock:
            if not cls.instance:
                cls.instance = super().__new__(cls)
            return cls.instance
```

通过模块导入的形式也可以实现单例模式

```python
# test1.py
class Foo:
  pass

site = Foo()
```

```python
from test1 import site

print(site) # 单例模式
txj1371357ty1009zhl
```






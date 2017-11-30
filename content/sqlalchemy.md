Title: Sqlalchemy笔记
Category: python_web
Date: 2017-11-30

> 主要参考sqlalchemy官方文档

### 初始化过程
- 创建engine,Base,session
分别对应的是数据库连接，对象映射，回话

```python
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import scoped_session, sessionmaker

Base = declarative_base() # orm metadata信息父类
engine = create_engine(cfg.SQLALCHEMY_DATABASE_URI, echo=True)
session = scoped_session(sessionmaker(autocommit=False,autoflush=False,bind=engine))
Base.query = session.query_property() #对象绑定query方法

```

- 初始化数据库表结构

```python
from .models import Pet,User,Relation # 引入的对象会在metadata中注册
Base.metadata.create_all(bind=engine)

```

### 查询
查询语句可以分为以下几节，几节链式操作拼成一个完整的sql:
```
from sqlalchemy import func,or_,and_,text
```

```python
查询 -- 过滤 -- 排序 -- 取值
session.query(User) |  .filter_by(name='ed') |  .order_by(User.id) | first()
```

- 查询节
```python
query(User);query(User.name)
query(func.count(User.name),User.name).group_by(User.name) # 计数与分组查询

```

- 过滤节
```python
filter_by(name='id');
filter(User.name.in_(['red','blue'])) # like(),and_,or_,==,!=
filter(text('name like :name')).params(name='abc',..)

```

- 排序节

```python
order_by(User.id)

```
- 取值节

```python
first();all();one();one_or_none();scalar()# scalar 操作为one操作的第一个结果集的第一个元素
count() # 获取结果集的个数
```

### 表关联
#### 定义关联表

- 多对一与一对多
```
class User(Base):
	__tablename__ = 'users'
	id = Column(Integer,primary_key=True)
	name = Column(String(32))
	#address_id = Column(Integer, ForeignKey('address.id')) 
	#不在这里定义外键，因为这里是一方，应在多方声明外键
	addresses = relationship('Address',back_populates='user') #back_populates指向另一个类中的属性
	
class Address(Base):
	__tablename__ = 'address'
	id = Column(Integer,primary_key=True)
	name = Column(String(32))
	user_id = Column(Integer,ForeignKey('users.id'))
	user = relationship('User',back_populates='addresses')
```

- 多对多

```
class Pet(Base,CommonEntity):
	users = relationship("Relation", back_populates="pet")

class User(Base,CommonEntity):
	pets = relationship("Relation", back_populates="user")

#中间表定义外键关系
class Relation(Base):
	user_id = Column(Integer, ForeignKey('users.id'), primary_key=True)
    pet_id = Column(Integer, ForeignKey('pets.id'), primary_key=True)
    pet = relationship("Pet", back_populates="users")
    user = relationship("User", back_populates="pets")
```

#### 关联表查询

1）联合查询
session.query(User,Address).filter(User.id==Address.user_id).filter(..)

2）join查询
session.query(User).join(Address).filter(..)
或者：
session.query(User).join(User.addresses) # 当不止一个外键时显式指明
外关联：
session.query(User).outjoin(User.addresses)

3）为表对象取别名
```
from sqlalchemy.orm import aliased
alis = aliased(Address)
```

4）定义子查询语句
```
stmt = session.query(..).subquery()
子查询的结果可以理解为一个视图
session.query(User,stmt.c).filter(stmt.c.name = 'aa')
```

### 杂项
- 为字段取别名
```
Address.user_id.label('userid')
```
- 在关系中指定级联关系
```
relationship('Address', back_populates='users',cascade='all,delete')

```








Title: Keras
Category: ML
Date: 2017-12-21

> keras简化神经网络模型构建的过程

## 用keras进行数据训练和验证的主要步骤  
### 搭结构  

```
model---layers
	  --layers
	  --layers
	  --layers
```

### 编译  
```
.compile(
	  optimizer=优化器,
	  loss=损失函数,
	  metrics=度量
)

```

### 数据训练
```
.fit(
	  [data=]训练输入,
	  [labels=]训练标记,
	  epochs=数据轮循次数,
	  batch_size=数据组大小
)

```

### 验证
.evaluate(
	  [data=]训练输入
	  [labels=]训练标记
	  batch_size=数据组大小
)

---

## 使用中的注意事项  
1.理解机器学习及深度学习中的各种概念。比如：有监督学习，无监督学习
分类，聚类，回归；神经元模型，多层感知器，BP算法；目标函数（损失函数），
激活函数，梯度下降发；全连接网络，卷积神经网络，递归神经网络；训练集，测试集，
交叉验证，欠拟合，过拟合；数据规范化等
2.理解深度学习中各种模型和操作的特点，作用。比如cnn,rnn,lstm,dropout,pool等

## 一些梳理  

### activation的分类  
```
relu
sigmoid
softmax

```

### optimizer的分类  
```
rmsprop
sdg

```

### loss的分类  
```
binary_crossentropy
categorical_crossentropy
mse

```

### metrics的分类
```
accuracy

```
# MLPRegressor 神经网络搭建

​    **多层感知器(MLP)**是一种监督学习算法，前馈人工神经网络模型，本质上是一个*全连接神经网络*。

​	在输入样本后，样本在MLP在网络中逐层前馈（从输入层到隐藏层到输出层，逐层计算结果，即所谓前馈），得到最终输出值。

```python
#所用到的库
import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.neural_network import MLPRegressor
from sklearn import preprocessing
import pandas as pd
import random
```

##### 1.数据准备

**随机**测试数据100组，每组有7个自变量1个因变量，并保存到“all_data.csv”文件下。

![截屏2021-03-22 下午4.46.21](https://i.loli.net/2021/04/03/r7NP3QoI8msXySF.png)

读取数据文件：

![](https://i.loli.net/2021/04/03/ROhYZrfDVstlKad.png)

##### 2.描述性统计

![截屏2021-03-22 下午4.39.36](https://i.loli.net/2021/04/03/Zod3AeT6P7bB8Vs.png)

##### 3.数据标准化与测试集训练集分割

随机划分80%的训练集（这里为80组数据）与20%的测试集（这里为20组）。

![](https://i.loli.net/2021/04/03/p9BsmPxH4oDGXJr.png)划分后数据规模：

![](https://i.loli.net/2021/04/03/RaEPtdxcWHkpFNJ.png)

##### 4.使用sklearn库搭建MLP神经网络

参照文献中神经网络的构建：

* 输出层（一层）：共7个神经元；
* 隐藏层（共两层）：第一层15个神经元，第二层共5个神经元；
* 输出层（一层）：共1个神经元；

![](https://i.loli.net/2021/03/25/XBlStUC98T15kaP.png)

采用全链接构建神经网络，网络结构如下：

![](https://i.loli.net/2021/03/25/OIeWLbmr4VyRYpq.png)

采用MLPRegressor函数构建神经网络用于回归。

![](https://i.loli.net/2021/04/03/QFMaXdf8eGA63Eo.png)

##### 5.模型评分

对训练后模型进行回归结果评分，共计算4个指标（RMSE、MAE、MSE、R<sup>2</sup>)

![截屏2021-03-22 下午5.33.49](https://i.loli.net/2021/04/03/2zyhOxIHJWfXQ79.png)

（对测试集测试的指标效果比较差的原因应该是随机生成数据集的问题，之后还可以调参优化）

##### 6.可视化部分（对测试集的可视化）

![截屏2021-03-22 下午5.39.17](https://i.loli.net/2021/04/03/vjMWStK31kZomHb.png)

![截屏2021-03-22 下午5.40.03](https://i.loli.net/2021/04/03/Yx1NLctXpnPIqf6.png)

##### 7.训练后神经网络连接权重

![截屏2021-03-22 下午5.41.14](https://i.loli.net/2021/04/03/NHL6etwxKIUcrTb.png)

![](https://i.loli.net/2021/04/03/DfQUcg9nyVAN3Wr.png)


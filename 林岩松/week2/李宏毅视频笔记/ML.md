# 机器学习任务攻略

![img2](..\pic\img_1.png)

1.（Model Bias）the model is too small >>>> 函数不在所设置的function可以覆盖的范围之内

2.（Optimization Issue）   >>>>  找到的参数带来的LOSS不够低

（Model Bias  >>  VS  >>  Optimization Issue）

![img1](..\pic\img.png)

  ---------训练一个浅层和深层网络，查看Optimization的问题
  

3.training data够小，但是testing loss够大，（Over Fitting过拟合）

   ------①增加训练资料，data augmentation（数据增强）

   ------②让模型没有那么大的弹性，Less parameters  or  sharing parameters（CNN比较没有弹性），

   ------③less features ，early stopping，regularization，dropout
   
## Bias-Complexxity Trade-off （过拟合和欠拟合）

为什么要有public set 和 private set

public随机，有可能一个很差的Function可以在public set上随机出取得很好成果，但实际上模型很差

training set  >>>>  分成training set 和 Validation set

N-ford Cross Validation

missmatch  >>>> 训练资料和测试资料分布不同

# 类神经网络训练不起来怎么办（一）：局部最小值（local minima）与鞍点（saddle point）

梯度为0  >>>>   local minima 和saddle point都有可能   >>>>   可以说卡在了Critical point（驻点）

---------可以有办法找到是在local minima还是saddle point（用数学）

![img3](..\pic\img_2.png)

-----------绿色方框为0的话，代表critical point的位置
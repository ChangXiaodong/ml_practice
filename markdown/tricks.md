# 笔记

1. sofmax是sigmoid的扩展。softmax可以用于多分类问题。与多个二分类器的区别是：

   softmax适用于相互独立的类别，多个二分类器如logistic regression实用于不相互独立的。

eg.将图像分到三个不同类别中。

(i) 假设这三个类别分别是：室内场景、户外城区场景、户外荒野场景。

(ii) 现在假设这三个类别分别是室内场景、黑白图片、包含人物的图片。
在第一个例子中，三个类别是互斥的，因此更适于选择softmax回归分类器 。而在第二个例子中，建立三个独立的 logistic回归分类器更加合适。

2.神经网络在输出一个结果向量后，比如数字识别[0,1,0,0,0,0,0,0,0,0],经过softmax变成[0.1,0.9,0.2,0.3,0.4...]，计算交叉熵

3.神经网络优化方法-减小过拟合

- 滑动平均模型：shadow_variable = decay * shadow_variable + (1 - decay) * variable   

  decay一般为比较接近1的数。Tensorflow中，ExponentialMovingAverage提供了num_updates来动态设定decay。decay = min(decay, (1+num_updates)/(10 + num_updates))

- 指数衰减学习率

- 加入正则化的损失函数

  一般情况下，最有效的是增加正则化损失函数

  ​
# K-Means Vs MiniBatch K-Means

## K-Means

1.k值得选择

- k的范围一般在2 - sqrt(N)之间

- k值不断增加，计算类内误差平方和，选择误差平方值最小的k值

- k值不断增加，计算类内误差平方和与类间误差平方和的比值，选择比值的拐点处的k值

- 将数据可视化，根据经验选择

- 交叉验证法选择

- Elbow方法

  sum{(ni * (Mi - GM)^2) }/ sum {(X - GM) ^2}

  ni 是第i类内样本点数量， Mi是第i类样本中心点，GM是所有样本的中心点， X是样本。

  k值不断增加，选择比值拐点处的k值

2.初始化

- 随机初始化

- Kmeans++，初始化时使中心店距离最远

- 从给定的集合中选取。集合的大小大于K

3.Elkan算法

利用三角不等式减少计算次数。加速算法。

定理1：x是样本点，c、c'是中心。存在以下不等式，若 d(c, c') >= 2d(x, c) 则 d(x, c') >= d(x, c)

这种情况下可以避免计算d(x, c')。若能够知道d(x, c)的上界u，并且u<=1/2 d(c, c'), 那么d(x, c)和d(x, c')都不必计算。

定理2：x是样本点，c、c'是中心。存在以下不等式，d(x, c) >= max{0, d(x, c') - d(c, c')}

假设x是一个样本点，b是一个中心，b'是上一次迭代的中心，l'是上次迭代的下限，即d(x, b') >= l'.可以退出本轮迭代的下限：

d(x, b) >= max{0, d(x, b') - d(b, b')}>=max(0, l' - d(b, b'))=l

在后期的迭代中，b和b'的距离很小，因此可以用l'近似的替代l

算法：

```python
def k_means_Elkan(samples, k):
    centroids = _init_centroid(samples, k)
	#用来存储中心点i到其他中心点j 的距离
	table = [[0 for _ in range(k)] for _ in range(k)]
	#用来存储中心点i到其他中心点最小距离的1/2
	min_dis = [0 for _ in range(k)]
    update(table)
    update(min_dis)
    x_centroid = {}
	for x in samples:
        d = float("inf")
        for c in centroids:
            if dis(x, c) < d:
                new_x = (x, c)
         x_centroid[x] = c
#对任意一个样本点x,若x到他目前中心点c的距离u小于c到其他中心点距离的1/2，则x的中心点不变
	for x in x_centroid:
    	if dis(x, c) <= min_dis[c]:
        	contine
        else:
            for c_ in centroids:
                if c_ != c:
                    if dis(x, c_) < dis(x, c):
                        x_centroid[x] = c_
   	c = means(c)


    
      

```






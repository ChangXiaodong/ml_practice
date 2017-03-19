```
class MiniBatchKMeans(KMeans):
	Parameters:
		n_clusters : int, optional, default: 8
			k值个数
		max_iter : int, optional
			最大迭代次数
		max_no_improvement : int, default: 10
			在收敛前结束迭代
		tol : float, default: 0.0
			收敛阈值
		batch_size : int, optional, default: 100
			mini batches大小
		init_size : int, optional, default: 3 * batch_size
			初始化中心点时使用的数据数量
		init : {'k-means++', 'random' or an ndarray}, default: 'k-means++'
			初始化中心点方法
		n_init : int, default=3
			初始化中心点尝试次数，使用最优的inertia
		compute_labels : boolean, default=True
			完成收敛后，计算每一个点的label
		random_state : integer or numpy.RandomState, optional
			随机种子
		reassignment_ratio : float, default: 0.01
			如果数给的大，会花费更长的时间收敛，但是瘦脸效果更好
		verbose:
			输出信息模式
	Attributes：
		cluster_centers_ : array, [n_clusters, n_features]
        	Coordinates of cluster centers

        labels_ :
            Labels of each point (if compute_labels is set to True).

        inertia_ : float
            The value of the inertia criterion associated with the chosen
            partition (if compute_labels is set to True). The inertia is
            defined as the sum of square distances of samples to their nearest
            neighbor.

```

计算步骤：

1.选取随机种子
2.检查X
3.计算每一行点的L2范数,用每个数与这一行的平均数求平方差。计算完成留着后面用
4.计算old_center_buffer， 用来检测何时收敛，什么时候可以提前结束迭代
5.首先进行簇中心的选择， 进行n_init此minibatch k-means计算，选出inertia最小的簇中心
6.然后进行n_iter此mini_batch_step
7.每次随机选择batch_size个数据，执行mini_batch_step步骤，执行完成后判断是否收敛，如果收敛则提前结束迭代
7.然后执行ministep步骤，
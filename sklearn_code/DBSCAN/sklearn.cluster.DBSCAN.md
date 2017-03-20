```
class DBSCAN(BaseEstimator, ClusterMixin):
	Parameters:
		eps : float, optional
			样本间的距离，小于这个距离认为密度可达
		min_samples : int, optional
			一个聚类内最小的节点数，大于这个数字才认为是一个有效聚类
		metric : string, or callable
			可以自定义计算距离的方法
		algorithm : {'auto', 'ball_tree', 'kd_tree', 'brute'}, optional
			knn模块用来计算最近邻居的方法
		leaf_size : int, optional (default = 30)
			传给ball_tree 或 kd_tree的参数，可以加快计算速度
		p : float, optional
			运用Minkowski矩阵计算点间距的参数
		n_jobs : int, optional (default = 1)
			并行选项
	Attributes:
		core_sample_indices_ : array, shape = [n_core_samples]
			聚类的中心点指数
		components_ : array, shape = [n_core_samples, n_features]
			训练找到的中心点
		labels_ : array, shape = [n_samples]
			每个样本的label
	
def dbscan(X, eps=0.5, min_samples=5, metric='minkowski',
           algorithm='auto', leaf_size=30, p=2, sample_weight=None, n_jobs=1):
     Parameters:
     	 : array or sparse (CSR) matrix of shape (n_samples, n_features), or \
            array of shape (n_samples, n_samples)
        A feature array, or array of distances between samples if
        ``metric='precomputed'``.

    eps : float, optional
        The maximum distance between two samples for them to be considered
        as in the same neighborhood.

    min_samples : int, optional
        The number of samples (or total weight) in a neighborhood for a point
        to be considered as a core point. This includes the point itself.

    metric : string, or callable
        The metric to use when calculating distance between instances in a
        feature array. If metric is a string or callable, it must be one of
        the options allowed by metrics.pairwise.pairwise_distances for its
        metric parameter.
        If metric is "precomputed", X is assumed to be a distance matrix and
        must be square. X may be a sparse matrix, in which case only "nonzero"
        elements may be considered neighbors for DBSCAN.

    algorithm : {'auto', 'ball_tree', 'kd_tree', 'brute'}, optional
        The algorithm to be used by the NearestNeighbors module
        to compute pointwise distances and find nearest neighbors.
        See NearestNeighbors module documentation for details.

    leaf_size : int, optional (default = 30)
        Leaf size passed to BallTree or cKDTree. This can affect the speed
        of the construction and query, as well as the memory required
        to store the tree. The optimal value depends
        on the nature of the problem.

    p : float, optional
        The power of the Minkowski metric to be used to calculate distance
        between points.

    sample_weight : array, shape (n_samples,), optional
    	节点的权重，如果权重大于min_samles，它本身就成为了一个core，如果为负数，则会拒绝他成为			core
        Weight of each sample, such that a sample with a weight of at least
        ``min_samples`` is by itself a core sample; a sample with negative
        weight may inhibit its eps-neighbor from being core.
        Note that weights are absolute, and default to 1.

    n_jobs : int, optional (default = 1)
        The number of parallel jobs to run for neighbors search.
        If ``-1``, then the number of jobs is set to the number of CPU cores.

    Returns
    -------
    core_samples : array [n_core_samples]
        Indices of core samples.

    labels : array [n_samples]
        Cluster labels for each point.  Noisy samples are given the label -1.
```
- 计算步骤

  ​
1.检查输入样本X，允许X是稀疏矩阵
2.检查样本权重和样本X的对应关系
3.如果是稀疏矩阵，则对稀疏矩阵进行处理，计算他的近邻
4.否则是正常矩阵，调用NearestNeighbors方法，用给定的algorithm生成kd_tree, Ball_tree or Brute force。
5.给定一个半径，用radius_neighbors找出近邻
6.如果neighbors数量大于min_samples,则样本点为core
5.
class KMeans(BaseEstimator, ClusterMixin, TransformerMixin):

Parameters:

```
n_clusters:k个数
max_iter：最大迭代次数
n_init： 用不同随机数初始化k，计算n_init次k-means，返回类内误差最小的中心点，类内误差和其他一些参数
init:初始化中心点的方式，k-means++, random 或 制定array
algorithm：计算means的算法，full或elkan
precompute_distances：可以加快速度，但是会占用内存
tol：收敛判断阈值
n_jobs：并行cpu数量
random_state：产生随机数的种子
verbose：输出训练过程信息
copy_x：precompute时是否能够修改原始数据
```

Attributes：

```
cluster_centers_ :中心点坐标
labels_ ：每个点的labels
inertia_ ：类内平方误差和
```
主要步骤：
类方法fit，调用函数k_means

```
def k_means(X, n_clusters, init='k-means++', precompute_distances='auto',
            n_init=10, max_iter=300, verbose=False,
            tol=1e-4, random_state=None, copy_x=True, n_jobs=1,
            algorithm="auto", return_n_iter=False):
```

1.k_means函数首先检查传入的random_state，产生对应的随机数种子。
2.将原始数据根据copy_x选项进行复制
3.计算一个和原始数据独立的tolerance，用矩阵的方差 * tol。如果数据是csr稀疏矩阵，则用稀疏矩阵的方法计算矩阵方差。
>csr稀疏矩阵: data存数据，row和col存对应数据的坐标
>row = np.array([0, 0, 1, 2, 2, 2])
>col = np.array([0, 2, 2, 0, 1, 2])
>data = np.array([1, 2, 3, 4, 5, 6])
>csr_matrix((data, (row, col)), shape=(3, 3)).toarray()
>array([
>[1, 0, 2],
>[0, 0, 3],
>[4, 5, 6]
>])
4.计算L2范数平方，即用欧式距离作为距离检测的标准
5.制定训练的算法，full或elkan
6.对并行处理，如果需要并行，调用sklearn自带的Parallel模块
7.返回best_centers, best_labels, best_inertia




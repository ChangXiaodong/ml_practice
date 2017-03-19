		class Parallel(Logger):

```
Parameters:
	n_jobs: int, default: 1
		使用cpu的数量，-1为全部使用
	backend: str or None, default: 'multiprocessing'
		并行方式，multiprocessing、threading或自定义
	verbose:int, optional
		打印处理信息频率
	timeout: float, optional
		超时
	pre_dispatch: {'all', integer, or expression, as in '3*n_jobs'}
		提前feed数据的数量
	batch_size: int or 'auto', default: 'auto'
		每次分发数据的大小
	temp_folder: str, optional
		临时路径
	max_nbytes int, str, or None, optional, 1M by default
		触发memory mapping in temp_folder的阈值，只在multiprocessing时有效
	mmap_mode: {None, 'r+', 'r', 'w+', 'c'}
	
处理方式默认为multiprocessing

	
		
	
```
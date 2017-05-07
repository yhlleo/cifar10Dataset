# cifar10Dataset
Creat your own dataset with the similar format with CIFAR10 in python version.

之前发布的[仿照CIFAR10数据集格式，制作自己的数据集](http://blog.csdn.net/yhl_leo/article/details/50801226) (C++版本)，得到一些网友的关注，并且不断有网友在评论区或者私信里询问，怎样制作python版本的。趁着下午有点闲时间，把制作方法整理发布在这里，希望对大家有所帮助。

源码地址GitHub:  [yhlleo/cifar10Dataset](https://github.com/yhlleo/cifar10Dataset)

关于python 版本的CIFAR10的数据格式，官网上已经介绍：

 > **data** -- a 10000x3072 numpy array of uint8s. Each row of the array stores a 32x32 colour image. The first 1024 entries contain the red channel values, the next 1024 the green, and the final 1024 the blue. The image is stored in row-major order, so that the first 32 entries of the array are the red channel values of the first row of the image.
 >  **labels** -- a list of 10000 numbers in the range 0-9. The number at index i indicates the label of the ith image in the array data.

因此，想要制作自己的数据集，只需要把`data`, `label`准备好就可以，另外，我们可以读取`cifar10`存储好的文件，查看其数据格式，以`data_batch_1`为例（可以通过`cifar10_read.py`读取）：

```
{'data': array([[ 59,  43,  50, ..., 140,  84,  72],
       [154, 126, 105, ..., 139, 142, 144],
       [255, 253, 253, ...,  83,  83,  84],
       ..., 
       [ 71,  60,  74, ...,  68,  69,  68],
       [250, 254, 211, ..., 215, 255, 254],
       [ 62,  61,  60, ..., 130, 130, 131]], dtype=uint8), 
'labels': [6, 9, 9, 4, 1, 1, 2, 7, 8, 3, 4, 7, 7, 2, 9, 9, 9, 3, 2, 6, 4, 3, 6, 6, 2, 6, 3, 5, 4, 0, 0, 9, 1, 3, 4, 0, 3, 7, 3, 3, 5, 2, 2, 7, 1, 1, 1, 2, 2, 0, 9, 5, 7, 9, 2, 2, 5, 2, 4, 3, 1, 1, 8, 2, 1, 1, 4, 9, 7, 8, 5, 9, 6, 7, 3, 1, 9, 0, 3, 1, 3, 5, 4, 5, 7, 7,  ... , 9, 8, 9, 4, 4, 7, 1, 0, 4, 3, 6, 3, 9, 8, 3, 6, 8, 3, 6, 6, 2, 6, 7, 3, 0, 0, 0, 2, 5, 1, 2, 9, 2, 2, 1, 6, 3, 9, 1, 1, 5],
'batch_label': 'training batch 1 of 5', 
'filenames': ['leptodactylus_pentadactylus_s_000004.png', 'camion_s_000148.png', 'tipper_truck_s_001250.png', ... , 'truck_s_000036.png', 'car_s_002296.png', 'estate_car_s_001433.png', 'cur_s_000170.png']}
```

很明显，python版本存储成了一个`dict`，其中`key`包括:
 
 - `data`, 存放图像数据文件，是一个`nx3072`的数组；
 - `labels`, 存放图像对应的`label`，是一个`nx1`的数组；
 -  `batch_label`, 说明信息；
 - `filenames`, 文件名列表。

详细的代码内容，可以查看实现代码，另外`demo.py`中提供了测试数据，这里把读取的文件结果输出：

```
{'data': array([[255, 255, 255, ..., 255, 255, 255],
       [255, 255, 255, ..., 255, 255, 255]], dtype=uint8), 
'label': array([0, 1], dtype=uint8), 
'batch_label': 'training batch 0 of 1', 
'filenames': ['a.png', 'b.png']}
```

跟官方数据的输出格式一致，虽然没有训练测试，但是理论上应该没问题，大家在测试的过程中，如果遇到问题，欢迎指出。

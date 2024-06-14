#  Numpy
## 什么是Numpy
Numpy是Python科学计算库，主要提供了高性能的数组对象，以及数学运算函数。简单的来说就是对数据进行预处理时不可或缺的一个`第三方库`，属于在大模型实践路上的`必备品`。
## Numpy安装
Numpy安装非常简单，直接使用pip安装即可。windows机器直接CMD输入pip install numpy即可。
## Numpy基础
numpy的操作对象是多维数组，或者说是矩阵。有朋友可能想问了，python自带的list和tuple可以做矩阵运算吗？答案是可以的，但要**依赖for循环**，这非常不高效。
```python
# Python原生的list
# 假设有1个list
a = [1, 2, 3, 4, 5]
# 完成如下计算
# 对a的每个元素 + 1
# a = a + 1 不能这么写，会报错
# a[:] = a[:] + 1 也不能这么写，也会报错
for i in range(5):
    a[i] = a[i] + 1
print(a)
```
运行结果是[2, 3, 4, 5, 6]
但如果使用numpy，则可以直接使用numpy的函数来完成上述操作。
```python
import numpy as np
a = np.array([1, 2, 3, 4, 5])
a = a + 1
print(a)
```
运行结果是[2, 3, 4, 5, 6]
## Numpy创建数组
提供4种创建数组的方法：
- np.array()：这个是直接赋值
- np.zeros()：创建全0数组
- np.ones()：创建全1数组
- np.arange()：创建等差数列数组
具体写法如下：
```python
import numpy as np
a = np.array([1, 2, 3, 4, 5])
b = np.zeros(5)
c = np.ones(5)
d = np.arange(1,6,1)
print(a)
print(b)
print(c)
print(d)
```
运行结果是：  
[1 2 3 4 5]  
[0. 0. 0. 0. 0.]  
[1. 1. 1. 1. 1.]  
[1 2 3 4 5]  
当然还有其他创建数值的方法，就不一一列举了。  
## 查看ndarray数组的属性
ndarray的属性包括shape、dtype、size和ndim等，通过如下代码可以查看ndarray数组的属性。
```python
import numpy as np
a = np.array([1, 2, 3, 4, 5])
print(a.shape)
print(a.dtype)
print(a.size)
print(a.ndim)
print(a)
```
运行结果是：  
(5,)  
int64  
5  
1  
[1 2 3 4 5]  
其中shape表示数组的`形状`，dtype表示数组元素的`数据类型`，size表示数组`元素个数`（是通过形状乘积得到的），ndim表示数组的`维度`。

## 改变ndarray数组的数据类型和形状
ndarray数组可以通过astype()函数来改变数据类型，通过reshape()函数来改变形状。
其中reshape需要注意，reshape前后的`size`必须一致，否则会报错。
```python
import numpy as np
a = np.array([1, 2, 3, 4, 5, 6])
b = a.reshape(2,3)
c = a.reshape(3,2)
d = a.reshape(1,5)
```
以上可以通过a.shape来变换形状，b和c都可以成功，但d是会报错的，因为1*5是一个完全不同的形状，原数据里有6个数字，而reshape后只能有5个数字。

## ndarray数组的基本运算
array可以像普通变量一样去做加减乘除，直接运算即可。
```python
import numpy as np
a = np.array([1, 2, 3, 4, 5])
b = np.array([1, 2, 3, 4, 5])
print(a + b)
print(a - b)
```
运行结果是：  
[2 4 6 8 10]  
[0 0 0 0 0]  
## ndarray数组的索引和切片
可以直接通过索引去切片，但数组切片产生的新数组，还是指向原来的内存区域，数据不会被复制，视图上的任何修改都会直接反映到源数组上。将一个标量值赋值给一个切片时，该值会自动传播到整个选区
```python
import numpy as np
a = np.arange(24)
b = a.reshape(4,6)
c = b[0]
print(c)
```
运行结果应该是[0 1 2 3 4 5]

## ndarray数组的统计方法
可以通过数组上的一组数学函数对整个数组或某个轴向的数据进行统计计算。主要包括如下统计方法：
- mean：求平均
- sum：求和
- min\max：求极值
- argmin\argmax：求极值索引
- std\var：求标准差和方差
- cumsum：求累加和
- cumprod：求累乘积
需要注意的是这里会需要区分维度的概念，如axis=0，则表示按列进行统计，axis=1，则表示按行进行统计。这只是一个简单粗暴的理解。  
合理的理解是axis的最大值是数组最里面的[]里的数字，最小值是数组最外面的[]里的数字。

## 随机数np.random
### 创建随机ndarray数组
两种方式，一种是每次运行随机数都不一样，另一种是每次运行随机数都是相同的。
- 随机数一样的方法：通过np.random.seed()去完成定义随机数种子  
> [!WARNING]
> 这里需要注意的是np.random.seed()的含义，其实我在这块的理解也不是很透彻，始终找不得一个合适的角度去理解的。只能机械到理解成np.random.seed(1)和np.random.seed(2)分别固定的随机数不一样
- 随机数不一样的方法：直接使用np.random.random()
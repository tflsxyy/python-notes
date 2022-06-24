## Numpy

NumPy是使用Python进行科学计算的基础软件包。除其他外，它包括：

- 功能强大的N维数组对象。
- 精密广播功能函数。
- 集成 C/C+和Fortran 代码的工具。
- 强大的线性代数、傅立叶变换和随机数功能。

### 安装使用Numpy

我们可以先通过下面的命令来安装`numpy`。

```bash
pip install numpy
```

按照[官方文档](https://www.numpy.org.cn)的介绍，我们可以很方便的使用Numpy来创建例子。

```python
from numpy import *
eye(4)

# 结果
# array([[1., 0., 0., 0.],
#        [0., 1., 0., 0.],
#        [0., 0., 1., 0.],
#        [0., 0., 0., 1.]])
```

NumPy的主要对象是同构多维数组。它是一个元素表（通常是数字），所有类型都相同，由非负整数元组索引。在NumPy维度中称为 *轴* 。

例如，3D空间中的点的坐标`[1, 2, 1]`具有一个轴。该轴有3个元素，所以我们说它的长度为3.在下图所示的例子中，数组有2个轴。第一轴的长度为2，第二轴的长度为3。

```python
[[ 1., 0., 0.],
 [ 0., 1., 2.]]
```

NumPy的数组类被调用`ndarray`。它也被别名所知 `array`。请注意，`numpy.array`这与标准Python库类不同`array.array`，后者只处理一维数组并提供较少的功能。`ndarray`对象更重要的属性是：

- **ndarray.ndim** - 数组的轴（维度）的个数。在Python世界中，维度的数量被称为rank。
- **ndarray.shape** - 数组的维度。这是一个整数的元组，表示每个维度中数组的大小。对于有 *n*行和 *m* 列的矩阵，`shape` 将是 `(n,m)`。因此，`shape` 元组的长度就是rank或维度的个数 `ndim`。
- **ndarray.size** - 数组元素的总数。这等于 `shape` 的元素的乘积。
- **ndarray.dtype** - 一个描述数组中元素类型的对象。可以使用标准的Python类型创建或指定dtype。另外NumPy提供它自己的类型。例如numpy.int32、numpy.int16和numpy.float64。
- **ndarray.itemsize** - 数组中每个元素的字节大小。例如，元素为 `float64` 类型的数组的 `itemsize` 为8（=64/8），而 `complex32` 类型的数组的 `itemsize` 为4（=32/8）。它等于 `ndarray.dtype.itemsize` 。
- **ndarray.data** - 该缓冲区包含数组的实际元素。通常，我们不需要使用此属性，因为我们将使用索引访问数组中的元素。

### 数组创建

有几种方法可以创建数组。

例如，你可以使用array函数从常规Python列表或元组中创建数组。得到的数组的类型是从Python列表中元素的类型推导出来的。

```python
>>> import numpy as np
>>> a = np.array([2,3,4])
>>> a
array([2, 3, 4])
>>> a.dtype
dtype('int64')
>>> b = np.array([1.2, 3.5, 5.1])
>>> b.dtype
dtype('float64')
```

一个常见的错误，就是调用`array`的时候传入多个数字参数，而不是提供单个数字的列表类型作为参数。

```python
>>> a = np.array(1,2,3,4)    # WRONG
>>> a = np.array([1,2,3,4])  # RIGHT
```

`array` 还可以将序列的序列转换成二维数组，将序列的序列的序列转换成三维数组，等等。

```python
>>> b = np.array([(1.5,2,3), (4,5,6)])
>>> b
array([[ 1.5,  2. ,  3. ],
       [ 4. ,  5. ,  6. ]])
```

也可以在创建时显式指定数组的类型：

```python
>>> c = np.array( [ [1,2], [3,4] ], dtype=complex )
>>> c
array([[ 1.+0.j,  2.+0.j],
       [ 3.+0.j,  4.+0.j]])
```

通常，数组的元素最初是未知的，但它的大小是已知的。因此，NumPy提供了几个函数来创建具有初始占位符内容的数组。这就减少了数组增长的必要，因为数组增长的操作花费很大。

函数`zeros`创建一个由0组成的数组，函数 `ones`创建一个完整的数组，函数`empty` 创建一个数组，其初始内容是随机的，取决于内存的状态。默认情况下，创建的数组的dtype是`float64` 类型的。

```python
>>> np.zeros( (3,4) )
array([[ 0.,  0.,  0.,  0.],
       [ 0.,  0.,  0.,  0.],
       [ 0.,  0.,  0.,  0.]])
>>> np.ones( (2,3,4), dtype=np.int16 )                # dtype can also be specified
array([[[ 1, 1, 1, 1],
        [ 1, 1, 1, 1],
        [ 1, 1, 1, 1]],
       [[ 1, 1, 1, 1],
        [ 1, 1, 1, 1],
        [ 1, 1, 1, 1]]], dtype=int16)
>>> np.empty( (2,3) )                                 # uninitialized, output may vary
array([[  3.73603959e-262,   6.02658058e-154,   6.55490914e-260],
       [  5.30498948e-313,   3.14673309e-307,   1.00000000e+000]])
```

为了创建数字组成的数组，NumPy提供了一个类似于`range`的函数，该函数返回数组而不是列表。

```python
>>> np.arange( 10, 30, 5 )
array([10, 15, 20, 25])
>>> np.arange( 0, 2, 0.3 )                 # it accepts float arguments
array([ 0. ,  0.3,  0.6,  0.9,  1.2,  1.5,  1.8])
```

当`arange`与浮点参数一起使用时，由于有限的浮点精度，通常不可能预测所获得的元素的数量。出于这个原因，通常最好使用`linspace`函数来接收我们想要的元素数量的函数，而不是步长（step）：

```python
>>> from numpy import pi
>>> np.linspace( 0, 2, 9 )                 # 9 numbers from 0 to 2
array([ 0.  ,  0.25,  0.5 ,  0.75,  1.  ,  1.25,  1.5 ,  1.75,  2.  ])
>>> x = np.linspace( 0, 2*pi, 100 )        # useful to evaluate function at lots of points
>>> f = np.sin(x)
```

当`arange`与浮点参数一起使用时，由于有限的浮点精度，通常不可能预测所获得的元素的数量。出于这个原因，通常最好使用`linspace`函数来接收我们想要的元素数量的函数，而不是步长（step）：

```python
>>> from numpy import pi
>>> np.linspace( 0, 2, 9 )                 # 9 numbers from 0 to 2
array([ 0.  ,  0.25,  0.5 ,  0.75,  1.  ,  1.25,  1.5 ,  1.75,  2.  ])
>>> x = np.linspace( 0, 2*pi, 100 )        # useful to evaluate function at lots of points
>>> f = np.sin(x)
```

另见这些API

[`array`](https://numpy.org/devdocs/reference/generated/numpy.array.html#numpy.array)， [`zeros`](https://numpy.org/devdocs/reference/generated/numpy.zeros.html#numpy.zeros)， [`zeros_like`](https://numpy.org/devdocs/reference/generated/numpy.zeros_like.html#numpy.zeros_like)， [`ones`](https://numpy.org/devdocs/reference/generated/numpy.ones.html#numpy.ones)， [`ones_like`](https://numpy.org/devdocs/reference/generated/numpy.ones_like.html#numpy.ones_like)， [`empty`](https://numpy.org/devdocs/reference/generated/numpy.empty.html#numpy.empty)， [`empty_like`](https://numpy.org/devdocs/reference/generated/numpy.empty_like.html#numpy.empty_like)， [`arange`](https://numpy.org/devdocs/reference/generated/numpy.arange.html#numpy.arange)， [`linspace`](https://numpy.org/devdocs/reference/generated/numpy.linspace.html#numpy.linspace)，[`numpy.random.mtrand.RandomState.rand`](https://numpy.org/devdocs/reference/random/generated/numpy.random.mtrand.RandomState.rand.html#numpy.random.mtrand.RandomState.rand)，[`numpy.random.mtrand.RandomState.randn`](https://numpy.org/devdocs/reference/random/generated/numpy.random.mtrand.RandomState.randn.html#numpy.random.mtrand.RandomState.randn)， [`fromfunction`](https://numpy.org/devdocs/reference/generated/numpy.fromfunction.html#numpy.fromfunction)， [`fromfile`](https://numpy.org/devdocs/reference/generated/numpy.fromfile.html#numpy.fromfile)

### 打印数组

打印数组时，NumPy以与嵌套列表类似的方式显示它，但具有以下布局：

- 最后一个轴从左到右打印，
- 倒数第二个从上到下打印，
- 其余部分也从上到下打印，每个切片用空行分隔。

然后将一维数组打印为行，将二维数据打印为矩阵，将三维数据打印为矩数组表。

然后将一维数组打印为行，将二维数据打印为矩阵，将三维数据打印为矩数组表。

```python
>>> a = np.arange(6)                         # 1d array
>>> print(a)
[0 1 2 3 4 5]
>>>
>>> b = np.arange(12).reshape(4,3)           # 2d array
>>> print(b)
[[ 0  1  2]
 [ 3  4  5]
 [ 6  7  8]
 [ 9 10 11]]
>>>
>>> c = np.arange(24).reshape(2,3,4)         # 3d array
>>> print(c)
[[[ 0  1  2  3]
  [ 4  5  6  7]
  [ 8  9 10 11]]
 [[12 13 14 15]
  [16 17 18 19]
  [20 21 22 23]]]
```

有关 `reshape` 的详情，请参阅下文。

如果数组太大而无法打印，NumPy会自动跳过数组的中心部分并仅打印角点：

```python
>>> print(np.arange(10000))
[   0    1    2 ..., 9997 9998 9999]
>>>
>>> print(np.arange(10000).reshape(100,100))
[[   0    1    2 ...,   97   98   99]
 [ 100  101  102 ...,  197  198  199]
 [ 200  201  202 ...,  297  298  299]
 ...,
 [9700 9701 9702 ..., 9797 9798 9799]
 [9800 9801 9802 ..., 9897 9898 9899]
 [9900 9901 9902 ..., 9997 9998 9999]]
```

要禁用此行为并强制NumPy打印整个数组，可以使用更改打印选项`set_printoptions`。

```python
>>> np.set_printoptions(threshold=sys.maxsize)       # sys module should be imported
```

### 基本操作

数组上的算术运算符会应用到 *元素* 级别。下面是创建一个新数组并填充结果的示例：

```python
>>> a = np.array( [20,30,40,50] )
>>> b = np.arange( 4 )
>>> b
array([0, 1, 2, 3])
>>> c = a-b
>>> c
array([20, 29, 38, 47])
>>> b**2
array([0, 1, 4, 9])
>>> 10*np.sin(a)
array([ 9.12945251, -9.88031624,  7.4511316 , -2.62374854])
>>> a<35
array([ True, True, False, False])
```

与许多矩阵语言不同，乘积运算符`*`在NumPy数组中按元素进行运算。矩阵乘积可以使用`@`运算符（在python> = 3.5中）或`dot`函数或方法执行：

```python
>>> A = np.array( [[1,1],
...             [0,1]] )
>>> B = np.array( [[2,0],
...             [3,4]] )
>>> A * B                       # elementwise product
array([[2, 0],
       [0, 4]])
>>> A @ B                       # matrix product
array([[5, 4],
       [3, 4]])
>>> A.dot(B)                    # another matrix product
array([[5, 4],
       [3, 4]])
```

某些操作（例如`+=`和 `*=`）会更直接更改被操作的矩阵数组而不会创建新矩阵数组。

```python
>>> a = np.ones((2,3), dtype=int)
>>> b = np.random.random((2,3))
>>> a *= 3
>>> a
array([[3, 3, 3],
       [3, 3, 3]])
>>> b += a
>>> b
array([[ 3.417022  ,  3.72032449,  3.00011437],
       [ 3.30233257,  3.14675589,  3.09233859]])
>>> a += b                  # b is not automatically converted to integer type
Traceback (most recent call last):
  ...
TypeError: Cannot cast ufunc add output from dtype('float64') to dtype('int64') with casting rule 'same_kind'
```

当使用不同类型的数组进行操作时，结果数组的类型对应于更一般或更精确的数组（称为向上转换的行为）。

```python
>>> a = np.ones(3, dtype=np.int32)
>>> b = np.linspace(0,pi,3)
>>> b.dtype.name
'float64'
>>> c = a+b
>>> c
array([ 1.        ,  2.57079633,  4.14159265])
>>> c.dtype.name
'float64'
>>> d = np.exp(c*1j)
>>> d
array([ 0.54030231+0.84147098j, -0.84147098+0.54030231j,
       -0.54030231-0.84147098j])
>>> d.dtype.name
'complex128'
```

许多一元操作，例如计算数组中所有元素的总和，都是作为`ndarray`类的方法实现的。

```python
>>> a = np.random.random((2,3))
>>> a
array([[ 0.18626021,  0.34556073,  0.39676747],
       [ 0.53881673,  0.41919451,  0.6852195 ]])
>>> a.sum()
2.5718191614547998
>>> a.min()
0.1862602113776709
>>> a.max()
0.6852195003967595
```

默认情况下，这些操作适用于数组，就像它是一个数字列表一样，无论其形状如何。但是，通过指定`axis` 参数，您可以沿数组的指定轴应用操作：

```python
>>> b = np.arange(12).reshape(3,4)
>>> b
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])
>>>
>>> b.sum(axis=0)                            # sum of each column
array([12, 15, 18, 21])
>>>
>>> b.min(axis=1)                            # min of each row
array([0, 4, 8])
>>>
>>> b.cumsum(axis=1)                         # cumulative sum along each row
array([[ 0,  1,  3,  6],
       [ 4,  9, 15, 22],
       [ 8, 17, 27, 38]])
```

### 通函数

NumPy提供熟悉的数学函数，例如sin，cos和exp。在NumPy中，这些被称为“通函数”（`ufunc`）。在NumPy中，这些函数在数组上按元素进行运算，产生一个数组作为输出。

```python
>>> B = np.arange(3)
>>> B
array([0, 1, 2])
>>> np.exp(B)
array([ 1.        ,  2.71828183,  7.3890561 ])
>>> np.sqrt(B)
array([ 0.        ,  1.        ,  1.41421356])
>>> C = np.array([2., -1., 4.])
>>> np.add(B, C)
array([ 2.,  0.,  6.])
```

另见这些通函数

[`all`](https://numpy.org/devdocs/reference/generated/numpy.all.html#numpy.all)， [`any`](https://numpy.org/devdocs/reference/generated/numpy.any.html#numpy.any)， [`apply_along_axis`](https://numpy.org/devdocs/reference/generated/numpy.apply_along_axis.html#numpy.apply_along_axis)， [`argmax`](https://numpy.org/devdocs/reference/generated/numpy.argmax.html#numpy.argmax)， [`argmin`](https://numpy.org/devdocs/reference/generated/numpy.argmin.html#numpy.argmin)， [`argsort`](https://numpy.org/devdocs/reference/generated/numpy.argsort.html#numpy.argsort)， [`average`](https://numpy.org/devdocs/reference/generated/numpy.average.html#numpy.average)， [`bincount`](https://numpy.org/devdocs/reference/generated/numpy.bincount.html#numpy.bincount)， [`ceil`](https://numpy.org/devdocs/reference/generated/numpy.ceil.html#numpy.ceil)， [`clip`](https://numpy.org/devdocs/reference/generated/numpy.clip.html#numpy.clip)， [`conj`](https://numpy.org/devdocs/reference/generated/numpy.conj.html#numpy.conj)， [`corrcoef`](https://numpy.org/devdocs/reference/generated/numpy.corrcoef.html#numpy.corrcoef)， [`cov`](https://numpy.org/devdocs/reference/generated/numpy.cov.html#numpy.cov)， [`cross`](https://numpy.org/devdocs/reference/generated/numpy.cross.html#numpy.cross)， [`cumprod`](https://numpy.org/devdocs/reference/generated/numpy.cumprod.html#numpy.cumprod)， [`cumsum`](https://numpy.org/devdocs/reference/generated/numpy.cumsum.html#numpy.cumsum)， [`diff`](https://numpy.org/devdocs/reference/generated/numpy.diff.html#numpy.diff)， [`dot`](https://numpy.org/devdocs/reference/generated/numpy.dot.html#numpy.dot)， [`floor`](https://numpy.org/devdocs/reference/generated/numpy.floor.html#numpy.floor)， [`inner`](https://numpy.org/devdocs/reference/generated/numpy.inner.html#numpy.inner)， *INV* ， [`lexsort`](https://numpy.org/devdocs/reference/generated/numpy.lexsort.html#numpy.lexsort)， [`max`](https://docs.python.org/dev/library/functions.html#max)， [`maximum`](https://numpy.org/devdocs/reference/generated/numpy.maximum.html#numpy.maximum)， [`mean`](https://numpy.org/devdocs/reference/generated/numpy.mean.html#numpy.mean)，[`median`](https://numpy.org/devdocs/reference/generated/numpy.median.html#numpy.median)， [`min`](https://docs.python.org/dev/library/functions.html#min)， [`minimum`](https://numpy.org/devdocs/reference/generated/numpy.minimum.html#numpy.minimum)， [`nonzero`](https://numpy.org/devdocs/reference/generated/numpy.nonzero.html#numpy.nonzero)， [`outer`](https://numpy.org/devdocs/reference/generated/numpy.outer.html#numpy.outer)， [`prod`](https://numpy.org/devdocs/reference/generated/numpy.prod.html#numpy.prod)， [`re`](https://docs.python.org/dev/library/re.html#module-re)， [`round`](https://docs.python.org/dev/library/functions.html#round)， [`sort`](https://numpy.org/devdocs/reference/generated/numpy.sort.html#numpy.sort)， [`std`](https://numpy.org/devdocs/reference/generated/numpy.std.html#numpy.std)， [`sum`](https://numpy.org/devdocs/reference/generated/numpy.sum.html#numpy.sum)， [`trace`](https://numpy.org/devdocs/reference/generated/numpy.trace.html#numpy.trace)， [`transpose`](https://numpy.org/devdocs/reference/generated/numpy.transpose.html#numpy.transpose)，[`var`](https://numpy.org/devdocs/reference/generated/numpy.var.html#numpy.var)， [`vdot`](https://numpy.org/devdocs/reference/generated/numpy.vdot.html#numpy.vdot)， [`vectorize`](https://numpy.org/devdocs/reference/generated/numpy.vectorize.html#numpy.vectorize)， [`where`](https://numpy.org/devdocs/reference/generated/numpy.where.html#numpy.where)

### 索引、切片和迭代

**一维**的数组可以进行索引、切片和迭代操作的，就像 [列表](https://docs.python.org/tutorial/introduction.html#lists) 和其他Python序列类型一样。

```python
>>> a = np.arange(10)**3
>>> a
array([  0,   1,   8,  27,  64, 125, 216, 343, 512, 729])
>>> a[2]
8
>>> a[2:5]
array([ 8, 27, 64])
>>> a[:6:2] = -1000    # equivalent to a[0:6:2] = -1000; from start to position 6, exclusive, set every 2nd element to -1000
>>> a
array([-1000,     1, -1000,    27, -1000,   125,   216,   343,   512,   729])
>>> a[ : :-1]                                 # reversed a
array([  729,   512,   343,   216,   125, -1000,    27, -1000,     1, -1000])
>>> for i in a:
...     print(i**(1/3.))
...
nan
1.0
nan
3.0
nan
5.0
6.0
7.0
8.0
9.0
```

**多维**的数组每个轴可以有一个索引。这些索引以逗号分隔的元组给出：

```python
>>> def f(x,y):
...     return 10*x+y
...
>>> b = np.fromfunction(f,(5,4),dtype=int)
>>> b
array([[ 0,  1,  2,  3],
       [10, 11, 12, 13],
       [20, 21, 22, 23],
       [30, 31, 32, 33],
       [40, 41, 42, 43]])
>>> b[2,3]
23
>>> b[0:5, 1]                       # each row in the second column of b
array([ 1, 11, 21, 31, 41])
>>> b[ : ,1]                        # equivalent to the previous example
array([ 1, 11, 21, 31, 41])
>>> b[1:3, : ]                      # each column in the second and third row of b
array([[10, 11, 12, 13],
       [20, 21, 22, 23]])
```

当提供的索引少于轴的数量时，缺失的索引被认为是完整的切片`:`

```python
>>> b[-1]                                  # the last row. Equivalent to b[-1,:]
array([40, 41, 42, 43])
```

`b[i]` 方括号中的表达式 `i` 被视为后面紧跟着 `:` 的多个实例，用于表示剩余轴。NumPy也允许你使用三个点写为 `b[i,...]`。

三个点（ `...` ）表示产生完整索引元组所需的冒号。例如，如果 `x` 是rank为5的数组（即，它具有5个轴），则：

- `x[1,2,...]` 相当于 `x[1,2,:,:,:]`，
- `x[...,3]` 等效于 `x[:,:,:,:,3]`
- `x[4,...,5,:]` 等效于 `x[4,:,:,5,:]`。

```python
>>> c = np.array( [[[  0,  1,  2],               # a 3D array (two stacked 2D arrays)
...                 [ 10, 12, 13]],
...                [[100,101,102],
...                 [110,112,113]]])
>>> c.shape
(2, 2, 3)
>>> c[1,...]                                   # same as c[1,:,:] or c[1]
array([[100, 101, 102],
       [110, 112, 113]])
>>> c[...,2]                                   # same as c[:,:,2]
array([[  2,  13],
       [102, 113]])
```

对多维数组进行 **迭代（Iterating）** 是相对于第一个轴完成的：

```python
>>> for row in b:
...     print(row)
...
[0 1 2 3]
[10 11 12 13]
[20 21 22 23]
[30 31 32 33]
[40 41 42 43]
```

但是，如果想要对数组中的每个元素执行操作，可以使用`flat`属性，该属性是数组的所有元素的[迭代器](https://docs.python.org/tutorial/classes.html#iterators)：

```python
>>> for element in b.flat:
...     print(element)
...
0
1
2
3
10
11
12
13
20
21
22
23
30
31
32
33
40
41
42
43
```

### 直方图

`histogram`应用于数组的NumPy 函数返回一对向量：数组的直方图和bin的向量。注意：`matplotlib`还有一个构建直方图的功能，与NumPy中的直方图不同。主要区别在于`pylab.hist`自动绘制直方图，而 `numpy.histogram`只生成数据。

```python
>>> import numpy as np
>>> import matplotlib.pyplot as plt
>>> # Build a vector of 10000 normal deviates with variance 0.5^2 and mean 2
>>> mu, sigma = 2, 0.5
>>> v = np.random.normal(mu,sigma,10000)
>>> # Plot a normalized histogram with 50 bins
>>> plt.hist(v, bins=50, density=1)       # matplotlib version (plot)
>>> plt.show()
```

![quickstart-2_00_00](https://www.numpy.org.cn/static/images/quickstart-2_00_00.png)

```python
>>> # Compute the histogram with numpy and then plot it
>>> (n, bins) = np.histogram(v, bins=50, density=True)  # NumPy version (no plot)
>>> plt.plot(.5*(bins[1:]+bins[:-1]), n)
>>> plt.show()
```

![quickstart-2_01_00](https://www.numpy.org.cn/static/images/quickstart-2_01_00.png)
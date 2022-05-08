## Functions

### 关键字参数

下面是一个判断传入的三条边长能否构成三角形的函数，在调用函数传入参数时，我们可以指定参数名，也可以不指定参数名，代码如下所示。

```Python
def is_triangle(a, b, c):
    print(f'a = {a}, b = {b}, c = {c}')
    return a + b > c and b + c > a and a + c > b


# 调用函数传入参数不指定参数名按位置对号入座
print(is_triangle(1, 2, 3))
# 调用函数通过“参数名=参数值”的形式按顺序传入参数
print(is_triangle(a=1, b=2, c=3))
# 调用函数通过“参数名=参数值”的形式不按顺序传入参数
print(is_triangle(c=3, a=1, b=2))
```

在没有特殊处理的情况下，函数的参数都是**位置参数**，也就意味着传入参数的时候对号入座即可，如上面代码的第7行所示，传入的参数值`1`、`2`、`3`会依次赋值给参数`a`、`b`、`c`。当然，也可以通过`参数名=参数值`的方式传入函数所需的参数，因为指定了参数名，传入参数的顺序可以进行调整，如上面代码的第9行和第11行所示。

调用函数时，如果希望函数的调用者必须以`参数名=参数值`的方式传参，可以用**命名关键字参数**（keyword-only argument）取代位置参数。所谓命名关键字参数，是在函数的参数列表中，写在`*`之后的参数，代码如下所示。

```Python
def is_triangle(*, a, b, c):
    print(f'a = {a}, b = {b}, c = {c}')
    return a + b > c and b + c > a and a + c > b


# TypeError: is_triangle() takes 0 positional arguments but 3 were given
# print(is_triangle(3, 4, 5))
# 传参时必须使用“参数名=参数值”的方式，位置不重要
print(is_triangle(a=3, b=4, c=5))
print(is_triangle(c=5, b=4, a=3))
```

> **注意**：上面的`is_triangle`函数，参数列表中的`*`是一个分隔符，`*`前面的参数都是位置参数，而`*`后面的参数就是命名关键字参数。

我们之前讲过在函数的参数列表中可以使用**可变参数**`*args`来接收任意数量的参数，但是我们需要看看，`*args`是否能够接收带参数名的参数。

```Python
def calc(*args):
    result = 0
    for arg in args:
        if type(arg) in (int, float):
            result += arg
    return result


print(calc(a=1, b=2, c=3))
```

执行上面的代码会引发`TypeError`错误，错误消息为`calc() got an unexpected keyword argument 'a'`，由此可见，`*args`并不能处理带参数名的参数。我们在设计函数时，如果既不知道调用者会传入的参数个数，也不知道调用者会不会指定参数名，那么同时使用可变参数和**关键字参数**。关键字参数会将传入的带参数名的参数组装成一个字典，参数名就是字典中键值对的键，而参数值就是字典中键值对的值，代码如下所示。

```Python
def calc(*args, **kwargs):
    result = 0
    for arg in args:
        if type(arg) in (int, float):
            result += arg
    for value in kwargs.values():
        if type(value) in (int, float):
            result += value
    return result


print(calc())                  # 0
print(calc(1, 2, 3))           # 6
print(calc(a=1, b=2, c=3))     # 6
print(calc(1, 2, c=3, d=4))    # 10
```

> **提示**：**不带参数名的参数（位置参数）必须出现在带参数名的参数（关键字参数）之前**，否则将会引发异常。例如，执行`calc(1, 2, c=3, d=4, 5)`将会引发`SyntaxError`错误，错误消息为`positional argument follows keyword argument`，翻译成中文意思是“位置参数出现在关键字参数之后”。

### 高阶函数的用法

在前面几节课中，我们讲到了面向对象程序设计，在面向对象的世界中，一切皆为对象，所以类和函数也是对象。函数的参数和返回值可以是任意类型的对象，这就意味着**函数本身也可以作为函数的参数或返回值**，这就是所谓的**高阶函数**。

如果我们希望上面的`calc`函数不仅仅可以做多个参数求和，还可以做多个参数求乘积甚至更多的二元运算，我们就可以使用高阶函数的方式来改写上面的代码，将加法运算从函数中移除掉，具体的做法如下所示。

```Python
def calc(*args, init_value, op, **kwargs):
    result = init_value
    for arg in args:
        if type(arg) in (int, float):
            result = op(result, arg)
    for value in kwargs.values():
        if type(value) in (int, float):
            result = op(result, value)
    return result
```

注意，上面的函数增加了两个参数，其中`init_value`代表运算的初始值，`op`代表二元运算函数。经过改造的`calc`函数不仅仅可以实现多个参数的累加求和，也可以实现多个参数的累乘运算，代码如下所示。

```Python
def add(x, y):
    return x + y


def mul(x, y):
    return x * y


print(calc(1, 2, 3, init_value=0, op=add, x=4, y=5))      # 15
print(calc(1, 2, x=3, y=4, z=5, init_value=1, op=mul))    # 120
```

通过对高阶函数的运用，`calc`函数不再和加法运算耦合，所以灵活性和通用性会变强，这是一种解耦合的编程技巧，但是最初学者来说可能会稍微有点难以理解。需要注意的是，将函数作为参数和调用函数是有显著的区别的，**调用函数需要在函数名后面跟上圆括号，而把函数作为参数时只需要函数名即可**。上面的代码也可以不用定义`add`和`mul`函数，因为Python标准库中的`operator`模块提供了代表加法运算的`add`和代表乘法运算的`mul`函数，我们直接使用即可，代码如下所示。

```Python
import operator

print(calc(1, 2, 3, init_value=0, op=operator.add, x=4, y=5))      # 15
print(calc(1, 2, x=3, y=4, z=5, init_value=1, op=operator.mul))    # 120
```

Python内置函数中有不少高阶函数，我们前面提到过的`filter`和`map`函数就是高阶函数，前者可以实现对序列中元素的过滤，后者可以实现对序列中元素的映射，例如我们要去掉一个整数列表中的奇数，并对所有的偶数求平方得到一个新的列表，就可以直接使用这两个函数来做到，具体的做法是如下所示。

```Python
def is_even(num):
    return num % 2 == 0


def square(num):
    return num ** 2


numbers1 = [35, 12, 8, 99, 60, 52]
numbers2 = list(map(square, filter(is_even, numbers1)))
print(numbers2)    # [144, 64, 3600, 2704]
```

当然，要完成上面代码的功能，也可以使用列表生成式，列表生成式的做法更为简单优雅。

```Python
numbers1 = [35, 12, 8, 99, 60, 52]
numbers2 = [num ** 2 for num in numbers1 if num % 2 == 0]
print(numbers2)    # [144, 64, 3600, 2704]
```

### Lambda函数

在使用高阶函数的时候，如果作为参数或者返回值的函数本身非常简单，一行代码就能够完成，那么我们可以使用**Lambda函数**来表示。Python中的Lambda函数是没有的名字函数，所以很多人也把它叫做**匿名函数**，调用Lambda函数就跟调用普通函数一样，python 使用 lambda 来创建匿名函数，也就是不再使用 def 语句这样标准的形式定义一个函数。

匿名函数主要有以下特点：

* lambda 只是一个表达式，函数体比 def 简单很多。
* lambda 的主体是一个表达式，而不是一个代码块。仅仅能在 lambda 表达式中封装有限的逻辑进去。
* lambda 函数拥有自己的命名空间，且不能访问自有参数列表之外或全局命名空间里的参数。

示例：

```python
sum = lambda num1, num2 : num1 + num2

print(sum(1, 2)) # 3
```

本质上匿名函数和正常定义函数是一样的：

```python
def sum(num1, num2):
    return num1 + num2

print(sum(1, 2)) # 3
```

> 注意：**尽管 lambda 表达式允许你定义简单函数，但是它的使用是有限制的。 你只能指定单个表达式，它的值就是最后的返回值。也就是说不能包含其他的语言特性了， 包括多个语句、条件表达式、迭代以及异常处理等等。**

###  简单的总结

Python中的函数可以使用可变参数`*args`和关键字参数`**kwargs`来接收任意数量的参数，而且传入参数时可以带上参数名也可以没有参数名，可变参数会被处理成一个元组，而关键字参数会被处理成一个字典。**Python中的函数是一等函数，可以赋值给变量，也可以作为函数的参数和返回值**，这也就意味着我们可以在Python中使用高阶函数。如果我们要定义的函数非常简单，只有一行代码且不需要函数名，可以使用Lambda函数（匿名函数）。
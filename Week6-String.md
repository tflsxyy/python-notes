## String 字符串

### 字符串的定义

所谓**字符串**，就是**由零个或多个字符组成的有限序列**，一般记为：
$$
s = a_1a_2 \cdots a_n \,\,\,\,\, (0 \le n \le \infty)
$$
在Python程序中，如果我们把单个或多个字符用单引号或者双引号包围起来，就可以表示一个字符串。字符串中的字符可以是特殊符号、英文字母、中文字符、日文的平假名或片假名、希腊字母、[Emoji字符](<http://www.ruanyifeng.com/blog/2017/04/emoji.html>)等。

```Python
s1 = 'hello, world!'
s2 = "你好，世界！"
print(s1, s2)
# 以三个双引号或单引号开头的字符串可以折行
s3 = '''
hello, 
world!
'''
print(s3, end='')
```

> **提示**：`print`函数中的`end=''`表示输出后不换行，即将默认的结束符`\n`（换行符）更换为`''`（空字符）。

### 转义字符和原始字符串

可以在字符串中使用`\`（反斜杠）来表示转义，也就是说`\`后面的字符不再是它原来的意义，例如：`\n`不是代表反斜杠和字符`n`，而是表示换行；`\t`也不是代表反斜杠和字符`t`，而是表示制表符。所以如果字符串本身又包含了`'`、`"`、`\`这些特殊的字符，必须要通过`\`进行转义处理。例如要输出一个带单引号或反斜杠的字符串，需要用如下所示的方法。

```Python
s1 = '\'hello, world!\''
print(s1)
s2 = '\\hello, world!\\'
print(s2)
```

Python中的字符串可以`r`或`R`开头，这种字符串被称为原始字符串，意思是字符串中的每个字符都是它本来的含义，没有所谓的转义字符。例如，在字符串`'hello\n'`中，`\n`表示换行；而在`r'hello\n'`中，`\n`不再表示换行，就是反斜杠和字符`n`。大家可以运行下面的代码，看看会输出什么。

```Python
# 字符串s1中\t是制表符，\n是换行符
s1 = '\time up \now'
print(s1)
# 字符串s2中没有转义字符，每个字符都是原始含义
s2 = r'\time up \now'
print(s2)
```

Python中还允许在`\`后面还可以跟一个八进制或者十六进制数来表示字符，例如`\141`和`\x61`都代表小写字母`a`，前者是八进制的表示法，后者是十六进制的表示法。另外一种表示字符的方式是在`\u`后面跟Unicode字符编码，例如`\u9a86\u660a`代表的是中文“骆昊”。运行下面的代码，看看输出了什么。

```Python
s1 = '\141\142\143\x61\x62\x63'
s2 = '\u9a86\u660a'
print(s1, s2)
```

### 字符串的运算

Python为字符串类型提供了非常丰富的运算符，我们可以使用`+`运算符来实现字符串的拼接，可以使用`*`运算符来重复一个字符串的内容，可以使用`in`和`not in`来判断一个字符串是否包含另外一个字符串，我们也可以用`[]`和`[:]`运算符从字符串取出某个字符或某些字符。

#### 拼接和重复

下面的例子演示了使用`+`和`*`运算符来实现字符串的拼接和重复操作。

```Python
s1 = 'hello' + ' ' + 'world'
print(s1)    # hello world
s2 = '!' * 3
print(s2)    # !!!
s1 += s2     # s1 = s1 + s2
print(s1)    # hello world!!!
s1 *= 2      # s1 = s1 * 2
print(s1)    # hello world!!!hello world!!!
```

用`*`实现字符串的重复是非常有意思的一个运算符，在很多编程语言中，要表示一个有10个`a`的字符串，你只能写成`"aaaaaaaaaa"`，但是在Python中，你可以写成`'a' * 10`。你可能觉得`"aaaaaaaaaa"`这种写法也没有什么不方便的，那么想一想，如果字符`a`要重复100次或者1000次又会如何呢？

#### 比较运算

对于两个字符串类型的变量，可以直接使用比较运算符比较两个字符串的相等性或大小。需要说明的是，因为字符串在计算机内存中也是以二进制形式存在的，那么字符串的大小比较比的是每个字符对应的编码的大小。例如`A`的编码是`65`， 而`a`的编码是`97`，所以`'A' < 'a'`的结果相当于就是`65 < 97`的结果，很显然是`True`；而`'boy' < 'bad'`，因为第一个字符都是`'b'`比不出大小，所以实际比较的是第二个字符的大小，显然`'o' < 'a'`的结果是`False`，所以`'boy' < 'bad'`的结果也是`False`。如果不清楚两个字符对应的编码到底是多少，可以使用`ord`函数来获得，例如`ord('A')`的值是`65`，而`ord('昊')`的值是`26122`。下面的代码为大家展示了字符串的比较运算。

```Python
s1 = 'a whole new world'
s2 = 'hello world'
print(s1 == s2, s1 < s2)      # False True
print(s2 == 'hello world')    # True
print(s2 == 'Hello world')    # False
print(s2 != 'Hello world')    # True
s3 = '骆昊'
print(ord('骆'), ord('昊'))               # 39558 26122
s4 = '王大锤'
print(ord('王'), ord('大'), ord('锤'))    # 29579 22823 38180
print(s3 > s4, s3 <= s4)      # True False
```

需要强调一下的是，字符串的比较运算比较的是字符串的内容，Python中还有一个`is`运算符（身份运算符），如果用`is`来比较两个字符串，它比较的是两个变量对应的字符串对象的内存地址（不理解先跳过），简单的说就是两个变量是否对应内存中的同一个字符串。看看下面的代码就比较清楚`is`运算符的作用了。

```Python
s1 = 'hello world'
s2 = 'hello world'
s3 = s2
# 比较字符串的内容
print(s1 == s2, s2 == s3)    # True True
# 比较字符串的内存地址
print(s1 is s2, s2 is s3)    # False True
```

#### 成员运算

Python中可以用`in`和`not in`判断一个字符串中是否存在另外一个字符或字符串，`in`和`not in`运算通常称为成员运算，会产生布尔值`True`或`False`，代码如下所示。

```Python
s1 = 'hello, world'
print('wo' in s1)    # True
s2 = 'goodbye'
print(s2 in s1)      # False
```

#### 获取字符串长度

获取字符串长度没有直接的运算符，而是使用内置函数`len`，我们在上节课的提到过这个内置函数，代码如下所示。

```Python
s = 'hello, world'
print(len(s))                   # 12
print(len('goodbye, world'))    # 14
```

#### 索引和切片

如果希望从字符串中取出某个字符，我们可以对字符串进行索引运算，运算符是`[n]`，其中`n`是一个整数，假设字符串的长度为`N`，那么`n`可以是从`0`到`N-1`的整数，其中`0`是字符串中第一个字符的索引，而`N-1`是字符串中最后一个字符的索引，通常称之为正向索引；在Python中，字符串的索引也可以是从`-1`到`-N`的整数，其中`-1`是最后一个字符的索引，而`-N`则是第一个字符的索引，通常称之为负向索引。注意，因为**字符串是不可变类型**，所以**不能通过索引运算修改字符串中的字符**。

```Python
s = 'abc123456'
N = len(s)

# 获取第一个字符
print(s[0], s[-N])    # a a

# 获取最后一个字符
print(s[N-1], s[-1])  # 6 6

# 获取索引为2或-7的字符
print(s[2], s[-7])    # c c

# 获取索引为5和-4的字符
print(s[5], s[-4])    # 3 3
```

需要提醒大家注意的是，在进行索引操作时，如果索引越界（正向索引不在`0`到`N-1`范围，负向索引不在`-1`到`-N`范围），会引发`IndexError`异常，错误提示信息为：`string index out of range`（字符串索引超出范围）。

如果要从字符串中取出多个字符，我们可以对字符串进行切片，运算符是`[i:j:k]`，其中`i`是开始索引，索引对应的字符可以取到；`j`是结束索引，索引对应的字符不能取到；`k`是步长，默认值为`1`，表示从前向后获取相邻字符的连续切片，所以`:k`部分可以省略。假设字符串的长度为`N`，当`k > 0`时表示正向切片（从前向后获取字符），如果没有给出`i`和`j`的值，则`i`的默认值是`0`，`j`的默认值是`N`；当`k < 0`时表示负向切片（从后向前获取字符），如果没有给出`i`和`j`的值，则`i`的默认值是`-1`，j的默认值是`-N - 1`。如果不理解，直接看下面的例子，记住第一个字符的索引是`0`或`-N`，最后一个字符的索引是`N-1`或`-1`就行了。

```Python
s = 'abc123456'

# i=2, j=5, k=1的正向切片操作
print(s[2:5])       # c12

# i=-7, j=-4, k=1的正向切片操作
print(s[-7:-4])     # c12

# i=2, j=9, k=1的正向切片操作
print(s[2:])        # c123456

# i=-7, j=9, k=1的正向切片操作
print(s[-7:])       # c123456

# i=2, j=9, k=2的正向切片操作
print(s[2::2])      # c246

# i=-7, j=9, k=2的正向切片操作
print(s[-7::2])     # c246

# i=0, j=9, k=2的正向切片操作
print(s[::2])       # ac246

# i=1, j=-1, k=2的正向切片操作
print(s[1:-1:2])    # b135

# i=7, j=1, k=-1的负向切片操作
print(s[7:1:-1])    # 54321c

# i=-2, j=-8, k=-1的负向切片操作
print(s[-2:-8:-1])  # 54321c

# i=7, j=-10, k=-1的负向切片操作
print(s[7::-1])     # 54321cba

# i=-1, j=1, k=-1的负向切片操作
print(s[:1:-1])     # 654321c

# i=0, j=9, k=1的正向切片
print(s[:])         # abc123456

# i=0, j=9, k=2的正向切片
print(s[::2])       # ac246

# i=-1, j=-10, k=-1的负向切片
print(s[::-1])      # 654321cba

# i=-1, j=-10, k=-2的负向切片
print(s[::-2])      # 642ca
```

#### 循环遍历每个字符

如果希望从字符串中取出每个字符，可以使用`for`循环对字符串进行遍历，有两种方式。

方式一：

```Python
s1 = 'hello'
for index in range(len(s1)):
    print(s1[index])
```

方式二：

```Python
s1 = 'hello'
for ch in s1:
    print(ch)
```

### 字符串的方法

在Python中，我们可以通过字符串类型自带的方法对字符串进行操作和处理，对于一个字符串类型的变量，我们可以用`变量名.方法名()`的方式来调用它的方法。所谓方法其实就是跟某个类型的变量绑定的函数，后面我们讲面向对象编程的时候还会对这一概念详加说明。

#### 大小写相关操作

下面的代码演示了和字符串大小写变换相关的方法。

```Python
s1 = 'hello, world!'

# 使用capitalize方法获得字符串首字母大写后的字符串
print(s1.capitalize())   # Hello, world!
# 使用title方法获得字符串每个单词首字母大写后的字符串
print(s1.title())        # Hello, World!
# 使用upper方法获得字符串大写后的字符串
print(s1.upper())        # HELLO, WORLD!

s2 = 'GOODBYE'
# 使用lower方法获得字符串小写后的字符串
print(s2.lower())        # goodbye
```

#### 查找操作

如果想在一个字符串中从前向后查找有没有另外一个字符串，可以使用字符串的`find`或`index`方法。

```Python
s = 'hello, world!'

# find方法从字符串中查找另一个字符串所在的位置
# 找到了返回字符串中另一个字符串首字符的索引
print(s.find('or'))        # 8
# 找不到返回-1
print(s.find('shit'))      # -1
# index方法与find方法类似
# 找到了返回字符串中另一个字符串首字符的索引
print(s.index('or'))       # 8
# 找不到引发异常
print(s.index('shit'))     # ValueError: substring not found
```

在使用`find`和`index`方法时还可以通过方法的参数来指定查找的范围，也就是查找不必从索引为`0`的位置开始。`find`和`index`方法还有逆向查找（从后向前查找）的版本，分别是`rfind`和`rindex`，代码如下所示。

```Python
s = 'hello good world!'

# 从前向后查找字符o出现的位置(相当于第一次出现)
print(s.find('o'))       # 4
# 从索引为5的位置开始查找字符o出现的位置
print(s.find('o', 5))    # 7
# 从后向前查找字符o出现的位置(相当于最后一次出现)
print(s.rfind('o'))      # 12
```

#### 性质判断

可以通过字符串的`startswith`、`endswith`来判断字符串是否以某个字符串开头和结尾；还可以用`is`开头的方法判断字符串的特征，这些方法都返回布尔值，代码如下所示。

```Python
s1 = 'hello, world!'

# startwith方法检查字符串是否以指定的字符串开头返回布尔值
print(s1.startswith('He'))    # False
print(s1.startswith('hel'))   # True
# endswith方法检查字符串是否以指定的字符串结尾返回布尔值
print(s1.endswith('!'))       # True

s2 = 'abc123456'

# isdigit方法检查字符串是否由数字构成返回布尔值
print(s2.isdigit())    # False
# isalpha方法检查字符串是否以字母构成返回布尔值
print(s2.isalpha())    # False
# isalnum方法检查字符串是否以数字和字母构成返回布尔值
print(s2.isalnum())    # True
```

#### 格式化字符串

在Python中，字符串类型可以通过`center`、`ljust`、`rjust`方法做居中、左对齐和右对齐的处理。如果要在字符串的左侧补零，也可以使用`zfill`方法。

```Python
s = 'hello, world'

# center方法以宽度20将字符串居中并在两侧填充*
print(s.center(20, '*'))  # ****hello, world****
# rjust方法以宽度20将字符串右对齐并在左侧填充空格
print(s.rjust(20))        #         hello, world
# ljust方法以宽度20将字符串左对齐并在右侧填充~
print(s.ljust(20, '~'))   # hello, world~~~~~~~~
# 在字符串的左侧补零
print('33'.zfill(5))      # 00033
print('-33'.zfill(5))     # -0033
```

我们之前讲过，在用`print`函数输出字符串时，可以用下面的方式对字符串进行格式化。

```Python
a = 321
b = 123
print('%d * %d = %d' % (a, b, a * b))
```

当然，我们也可以用字符串的方法来完成字符串的格式，代码如下所示。

```Python
a = 321
b = 123
print('{0} * {1} = {2}'.format(a, b, a * b))
```

从Python 3.6开始，格式化字符串还有更为简洁的书写方式，就是在字符串前加上`f`来格式化字符串，在这种以`f`打头的字符串中，`{变量名}`是一个占位符，会被变量对应的值将其替换掉，代码如下所示。

```Python
a = 321
b = 123
print(f'{a} * {b} = {a * b}')
```

如果需要进一步控制格式化语法中变量值的形式，可以参照下面的表格来进行字符串格式化操作。

| 变量值      | 占位符     | 格式化结果      | 说明                   |
| ----------- | ---------- | --------------- | ---------------------- |
| `3.1415926` | `{:.2f}`   | `'3.14'`        | 保留小数点后两位       |
| `3.1415926` | `{:+.2f}`  | `'+3.14'`       | 带符号保留小数点后两位 |
| `-1`        | `{:+.2f}`  | `'-1.00'`       | 带符号保留小数点后两位 |
| `3.1415926` | `{:.0f}`   | `'3'`           | 不带小数               |
| `123`       | `{:0>10d}` | `'0000000123'`  | 左边补`0`，补够10位    |
| `123`       | `{:x<10d}` | `'123xxxxxxx'`  | 右边补`x` ，补够10位   |
| `123`       | `{:>10d}`  | `'       123'`  | 左边补空格，补够10位   |
| `123`       | `{:<10d}`  | `'123       '`  | 右边补空格，补够10位   |
| `123456789` | `{:,}`     | `'123,456,789'` | 逗号分隔格式           |
| `0.123`     | `{:.2%}`   | `'12.30%'`      | 百分比格式             |
| `123456789` | `{:.2e}`   | `'1.23e+08'`    | 科学计数法格式         |

#### 修剪操作

字符串的`strip`方法可以帮我们获得将原字符串修剪掉左右两端空格之后的字符串。这个方法非常有实用价值，通常用来将用户输入中因为不小心键入的头尾空格去掉，`strip`方法还有`lstrip`和`rstrip`两个版本，相信从名字大家已经猜出来这两个方法是做什么用的。

```Python
s = '   jackfrued@126.com  \t\r\n'
# strip方法获得字符串修剪左右两侧空格之后的字符串
print(s.strip())    # jackfrued@126.com
```

#### 替换操作

如果希望用新的内容替换字符串中指定的内容，可以使用`replace`方法，代码如下所示。`replace`方法的第一个参数是被替换的内容，第二个参数是替换后的内容，还可以通过第三个参数指定替换的次数。

```Python
s = 'hello, world'
print(s.replace('o', '@'))     # hell@, w@rld
print(s.replace('o', '@', 1))  # hell@, world
```

#### 拆分/合并操作

可以使用字符串的`split`方法将一个字符串拆分为多个字符串（放在一个列表中），也可以使用字符串的`join`方法将列表中的多个字符串连接成一个字符串，代码如下所示。

```Python
s = 'I love you'
words = s.split()
print(words)            # ['I', 'love', 'you']
print('#'.join(words))  # I#love#you
```

需要说明的是，`split`方法默认使用空格进行拆分，我们也可以指定其他的字符来拆分字符串，而且还可以指定最大拆分次数来控制拆分的效果，代码如下所示。

```Python
s = 'I#love#you#so#much'
words = s.split('#')
print(words)  # ['I', 'love', 'you', 'so', 'much']
words = s.split('#', 3)
print(words)  # ['I', 'love', 'you', 'so#much']
```

#### 编码/解码操作

Python中除了字符串`str`类型外，还有一种表示二进制数据的字节串类型（`bytes`）。所谓字节串，就是**由零个或多个字节组成的有限序列**。通过字符串的`encode`方法，我们可以按照某种编码方式将字符串编码为字节串，我们也可以使用字节串的`decode`方法，将字节串解码为字符串，代码如下所示。

```Python
a = '骆昊'
b = a.encode('utf-8')
c = a.encode('gbk')
print(b, c)  # b'\xe9\xaa\x86\xe6\x98\x8a' b'\xc2\xe6\xea\xbb'
print(b.decode('utf-8'))
print(c.decode('gbk'))
```

注意，如果编码和解码的方式不一致，会导致乱码问题（无法再现原始的内容）或引发`UnicodeDecodeError`错误导致程序崩溃。

#### 其他方法

对于字符串类型来说，还有一个常用的操作是对字符串进行匹配检查，即检查字符串是否满足某种特定的模式。例如，一个网站对用户注册信息中用户名和邮箱的检查，就属于模式匹配检查。实现模式匹配检查的工具叫做正则表达式，Python语言通过标准库中的`re`模块提供了对正则表达式的支持，我们会在后续的课程中为大家讲解这个知识点。

### 简单的总结

知道如何表示和操作字符串对程序员来说是非常重要的，因为我们需要处理文本信息，Python中操作字符串可以用拼接、切片等运算符，也可以使用字符串类型的方法。
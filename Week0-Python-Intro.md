# Python Introduction

### 为什么要学习Python

其实不是说一定要学或者每个人都要学Python，我们只是需要学习一种解决问题的方法。经过实践，大部分人选择了Python

### 为什么要选Python

Python是由荷兰人吉多·范罗苏姆（Guido von Rossum）发明的一种编程语言，是目前世界上最受欢迎和拥有最多用户群体的编程语言。

<img src="https://imagepphcloud.thepaper.cn/pph/image/98/653/364.jpg" width="30%">

C++之父：丹麦计算机科学家本贾尼·斯特劳斯特卢普（Bjarne Stroustrup）

<img src="https://pic3.zhimg.com/80/v2-c438db13fbd993ae3a5de747c3cd6cce_1440w.jpg" width="30%">



Java之父：詹姆斯·高斯林（James Gosling），加拿大软件专家，Java编程语言的共同创始人之一

<img src="http://5b0988e595225.cdn.sohucs.com/images/20180502/d9ac6f28980647c5832fdfc23122bc81.jpeg" width="30%">

<img src="https://gitee.com/jackfrued/mypic/raw/master/20210816232538.png" width="85%">

### Python的历史

1. 1989年圣诞节：Guido开始写Python语言的编译器。
2. 1991年2月：第一个Python解释器诞生，它是用C语言实现的，可以调用C语言的库函数。
3. 1994年1月：Python 1.0正式发布。
4. 2000年10月：Python 2.0发布，Python的整个开发过程更加透明，生态圈开始慢慢形成。
5. 2008年12月：Python 3.0发布，引入了诸多现代编程语言的新特性，但并不完全兼容之前的Python代码。
6. 2020年1月：在Python 2和Python 3共存了11年之后，官方停止了对Python 2的更新和维护，希望用户尽快过渡到Python 3。

> **说明**：大多数软件的版本号一般分为三段，形如A.B.C，其中A表示大版本号，当软件整体重写升级或出现不向后兼容的改变时，才会增加A；B表示功能更新，出现新功能时增加B；C表示小的改动（例如：修复了某个Bug），只要有修改就增加C。

### Python的优缺点

Python的优点很多，简单列出几点。

1. 简单明确，跟其他很多语言相比，Python更容易上手。
2. 能用更少的代码做更多的事情，提升开发效率。
3. 开放源代码，拥有强大的社区和生态圈。
4. 能够做的事情非常多，有极强的适应性。
5. 能够在Windows、macOS、Linux等各种系统上运行。

Python最主要的缺点是执行效率低，但是当我们更看重产品的开发效率而不是执行效率的时候，Python就是很好的选择。

### Python的应用领域

目前Python在Web服务器应用开发、云基础设施开发、**网络数据采集**（爬虫）、**数据分析**、量化交易、**机器学习**、**深度学习**、自动化测试、自动化运维等领域都有用武之地。

### Mac安装Python环境

macOS自带了Python 2，为了使用Python 3，我们可以从Python官网上下载对应的版本，不过我建议使用[Anaconda](https://www.anaconda.com/products/individual)来安装和管理Python版本和Python模块，同时提供了Jupyter可以交互式地使用Python。

### 终端（Terminal）

<img src="https://help.apple.com/assets/6152754A4192845C4361C49A/6152754B4192845C4361C4A1/en_GB/d94aa1c4979b25e9ffbda97fcbae219a.png" width="10%">

| 指令Command | 功能Options |
| :---------: | :---------: |
| **Exit** | 退出 |
| exit|退出当前终端|
| **Change Directory**    | 更改在文件夹中的位置 |
| cd | 回到Home文件夹 |
| cd ~ | 回到Home文件夹 |
| cd .. | 进入上一层文件夹 |
| pwd | 显示当前工作目录 |
| **List Directory Content** | 展示文件夹中的内容 |
| ls | 展示当前文件夹下的文件和子文件夹 |
| ls -all | 展示当前文件夹下所有文件和子文件夹（包括隐藏文件）以及文件的大小和修改时间 |
| **File and Directory Management** | 文件与文件夹操作 |
| cp <file> <dir> | 拷贝文件到目录 |
| mv <file> <dir> | 移动文件到目录 |
| mkdir <dir> | 在当前文件夹下创建一个新的叫dir的文件夹 |

> 使用Tab键，可以在终端中让电脑自动补全当前命令或者文件名
>
> 在终端的偏好设置中还可以更换喜欢的颜色。

### 运行第一个Python程序

在终端中运行以下命令，就可以运行 Python 程序了：

```bash
python example.py
```

如果当前Mac中还未安装Python3，只有默认的Python2，请使用`example_py2.py`:

```bash
python example_py2.py
```

### 写自己第一个Python程序 Hello World

按照行业惯例，我们学习任何一门编程语言写的第一个程序都是输出`hello, world`，因为这段代码是伟大的丹尼斯·里奇（C语言之父，和肯·汤普森一起开发了Unix操作系统）和布莱恩·柯尼汉（awk语言的发明者）在他们的不朽著作*The C Programming Language*中写的第一段代码。以下代码为使用Python输出"Hello World!"：

```python
>>> print("Hello World!")
Hello World! 
```

恭喜你！你现在已经可以运行并写出自己的第一个Python程序了！请继续保持，加油，后面的内容也不会很难！




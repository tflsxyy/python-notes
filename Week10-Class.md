## Class

面向对象编程是一种非常流行的**编程范式**（programming paradigm），所谓编程范式就是**程序设计的方法论**，简单的说就是程序员对程序的认知和理解以及他们编写代码的方式。

在前面的课程中，我们说过“**程序是指令的集合**”，运行程序时，程序中的语句会变成一条或多条指令，然后由CPU（中央处理器）去执行。为了简化程序的设计，我们又讲到了函数，**把相对独立且经常重复使用的代码放置到函数中**，在需要使用这些代码的时候调用函数即可。如果一个函数的功能过于复杂和臃肿，我们又可以进一步**将函数进一步拆分为多个子函数**来降低系统的复杂性。

我们的编程工作其实是写程序的人按照计算机的工作方式通过代码控制机器完成任务。但是，计算机的工作方式与人类正常的思维模式是不同的，如果编程就必须抛弃人类正常的思维方式去迎合计算机，编程的乐趣就少了很多。随着软件复杂性的增加，编写正确可靠的代码会变成了一项极为艰巨的任务，如何用程序描述复杂系统和解决复杂问题，就成为了所有程序员必须要思考和直面的问题。诞生于上世纪70年代的Smalltalk语言引入了一种新的编程范式叫面向对象编程。在面向对象编程的世界里，程序中的**数据和操作数据的函数是一个逻辑上的整体**，我们称之为**对象**，**对象可以接收消息**，解决问题的方法就是**创建对象并向对象发出各种各样的消息**；通过消息传递，程序中的多个对象可以协同工作，这样就能构造出复杂的系统并解决现实中的问题。



### 类和对象

如果要用一句话来概括面向对象编程，下面的说法是相当精辟和准确的。

> **面向对象编程**：把一组数据和处理数据的方法组成**对象**，把行为相同的对象归纳为**类**，通过**封装**隐藏对象的内部细节，通过**继承**实现类的特化和泛化，通过**多态**实现基于对象类型的动态分派。

这句话对初学者来说可能不那么容易理解，但是我可以先为大家圈出几个关键词：**对象**（object）、**类**（class）、**封装**（encapsulation）、**继承**（inheritance）、**多态**（polymorphism）。

我们先说说类和对象这两个词。在面向对象编程中，**类是一个抽象的概念，对象是一个具体的概念**。我们把同一类对象的共同特征抽取出来就是一个类，比如我们经常说的人类，这是一个抽象概念，而我们每个人就是人类的这个抽象概念下的实实在在的存在，也就是一个对象。简而言之，**类是对象的蓝图和模板，对象是类的实例，是可以接受消息的实体**。

在面向对象编程的世界中，**一切皆为对象**，**对象都有属性和行为**，**每个对象都是独一无二的**，而且**对象一定属于某个类**。对象的属性是对象的静态特征，对象的行为是对象的动态特征。按照上面的说法，如果我们把拥有共同特征的对象的属性和行为都抽取出来，就可以定义出一个类。



### 定义类

在Python中，可以使用`class`关键字加上类名来定义类，通过缩进我们可以确定类的代码块，就如同定义函数那样。在类的代码块中，我们需要写一些函数，我们说过类是一个抽象概念，那么这些函数就是我们对一类对象共同的动态特征的提取。写在类里面的函数我们通常称之为**方法**，方法就是对象的行为，也就是对象可以接收的消息。方法的第一个参数通常都是`self`，它代表了接收这个消息的对象本身。

```python
class Student:

    def study(self, course_name):
        print(f'学生正在学习{course_name}.')

    def play(self):
        print(f'学生正在玩游戏.')
```

### 创建和使用对象

在我们定义好一个类之后，可以使用构造器语法来创建对象，代码如下所示。

```Python
stu1 = Student()
stu2 = Student()
print(stu1)    # <__main__.Student object at 0x10ad5ac50>
print(stu2)    # <__main__.Student object at 0x10ad5acd0> 
print(hex(id(stu1)), hex(id(stu2)))    # 0x10ad5ac50 0x10ad5acd0
```

在类的名字后跟上圆括号就是所谓的构造器语法，上面的代码创建了两个学生对象，一个赋值给变量`stu1`，一个复制给变量`stu2`。当我们用`print`函数打印`stu1`和`stu2`两个变量时，我们会看到输出了对象在内存中的地址（十六进制形式），跟我们用`id`函数查看对象标识获得的值是相同的。现在我们可以告诉大家，我们定义的变量其实保存的是一个对象在内存中的逻辑地址（位置），通过这个逻辑地址，我们就可以在内存中找到这个对象。所以`stu3 = stu2`这样的赋值语句并没有创建新的对象，只是用一个新的变量保存了已有对象的地址。

接下来，我们尝试给对象发消息，即调用对象的方法。刚才的`Student`类中我们定义了`study`和`play`两个方法，两个方法的第一个参数`self`代表了接收消息的学生对象，`study`方法的第二个参数是学习的课程名称。Python中，给对象发消息有两种方式，请看下面的代码。

```python
# 通过“类.方法”调用方法，第一个参数是接收消息的对象，第二个参数是学习的课程名称
Student.study(stu1, 'Python程序设计')    # 学生正在学习Python程序设计.
# 通过“对象.方法”调用方法，点前面的对象就是接收消息的对象，只需要传入第二个参数
stu1.study('Python程序设计')             # 学生正在学习Python程序设计.

Student.play(stu2)    # 学生正在玩游戏.
stu2.play()           # 学生正在玩游戏. 
```

### 初始化方法

大家可能已经注意到了，刚才我们创建的学生对象只有行为没有属性，如果要给学生对象定义属性，我们可以修改`Student`类，为其添加一个名为`__init__`的方法。在我们调用`Student`类的构造器创建对象时，首先会在内存中获得保存学生对象所需的内存空间，然后通过自动执行`__init__`方法，完成对内存的初始化操作，也就是把数据放到内存空间中。所以我们可以通过给`Student`类添加`__init__`方法的方式为学生对象指定属性，同时完成对属性赋初始值的操作，正因如此，`__init__`方法通常也被称为初始化方法。

我们对上面的`Student`类稍作修改，给学生对象添加`name`（姓名）和`age`（年龄）两个属性。

```python
class Student:
    """学生"""

    def __init__(self, name, age):
        """初始化方法"""
        self.name = name
        self.age = age

    def study(self, course_name):
        """学习"""
        print(f'{self.name}正在学习{course_name}.')

    def play(self):
        """玩耍"""
        print(f'{self.name}正在玩游戏.')
```

修改刚才创建对象和给对象发消息的代码，重新执行一次，看看程序的执行结果有什么变化。

```Python
# 由于初始化方法除了self之外还有两个参数
# 所以调用Student类的构造器创建对象时要传入这两个参数
stu1 = Student('骆昊', 40)
stu2 = Student('王大锤', 15)
stu1.study('Python程序设计')    # 骆昊正在学习Python程序设计.
stu2.play()                    # 王大锤正在玩游戏.
```

### 打印对象

上面我们通过`__init__`方法在创建对象时为对象绑定了属性并赋予了初始值。在Python中，以两个下划线`__`（读作“dunder”）开头和结尾的方法通常都是有特殊用途和意义的方法，我们一般称之为**魔术方法**或**魔法方法**。如果我们在打印对象的时候不希望看到对象的地址而是看到我们自定义的信息，可以通过在类中放置`__repr__`魔术方法来做到，该方法返回的字符串就是用`print`函数打印对象的时候会显示的内容，代码如下所示。

```python
class Student:
    """学生"""

    def __init__(self, name, age):
        """初始化方法"""
        self.name = name
        self.age = age

    def study(self, course_name):
        """学习"""
        print(f'{self.name}正在学习{course_name}.')

    def play(self):
        """玩耍"""
        print(f'{self.name}正在玩游戏.')
    
    def __repr__(self):
        return f'{self.name}: {self.age}'


stu1 = Student('骆昊', 40)
print(stu1)        # 骆昊: 40
students = [stu1, Student('李元芳', 36), Student('王大锤', 25)]
print(students)    # [骆昊: 40, 李元芳: 36, 王大锤: 25]
```


### 面向对象的支柱

面向对象编程有三大支柱，就是我们之前给大家划重点的时候圈出的三个词：**封装**、**继承**和**多态**。我们先说一下什么是封装，封装的理解是：**隐藏一切可以隐藏的实现细节，只向外界暴露简单的调用接口**。我们在类中定义的对象方法其实就是一种封装，这种封装可以让我们在创建对象之后，只需要给对象发送一个消息就可以执行方法中的代码，也就是说我们在只知道方法的名字和参数（方法的外部视图），不知道方法内部实现细节（方法的内部视图）的情况下就完成了对方法的使用。

### 继承和多态

面向对象的编程语言支持在已有类的基础上创建新类，从而减少重复代码的编写。提供继承信息的类叫做父类（超类、基类），得到继承信息的类叫做子类（派生类、衍生类）。例如，我们定义一个学生类和一个老师类，我们会发现他们有大量的重复代码，而这些重复代码都是老师和学生作为人的公共属性和行为，所以在这种情况下，我们应该先定义人类，再通过继承，从人类派生出老师类和学生类，代码如下所示。

```python
class Person:
    """人类"""

    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def eat(self):
        print(f'{self.name}正在吃饭.')
    
    def sleep(self):
        print(f'{self.name}正在睡觉.')


class Student(Person):
    """学生类"""
    
    def __init__(self, name, age):
        # super(Student, self).__init__(name, age)
        super().__init__(name, age)
    
    def study(self, course_name):
        print(f'{self.name}正在学习{course_name}.')


class Teacher(Person):
    """老师类"""

    def __init__(self, name, age, title):
        # super(Teacher, self).__init__(name, age)
        super().__init__(name, age)
        self.title = title
    
    def teach(self, course_name):
        print(f'{self.name}{self.title}正在讲授{course_name}.')



stu1 = Student('白元芳', 21)
stu2 = Student('狄仁杰', 22)
teacher = Teacher('武则天', 35, '副教授')
stu1.eat()
stu2.sleep()
teacher.teach('Python程序设计')
stu1.study('Python程序设计')
```

继承的语法是在定义类的时候，在类名后的圆括号中指定当前类的父类。如果定义一个类的时候没有指定它的父类是谁，那么默认的父类是`object`类。`object`类是Python中的顶级类，这也就意味着所有的类都是它的子类，要么直接继承它，要么间接继承它。Python语言允许多重继承，也就是说一个类可以有一个或多个父类，关于多重继承的问题我们在后面会有更为详细的讨论。在子类的初始化方法中，我们可以通过`super().__init__()`来调用父类初始化方法，`super`函数是Python内置函数中专门为获取当前对象的父类对象而设计的。从上面的代码可以看出，子类除了可以通过继承得到父类提供的属性和方法外，还可以定义自己特有的属性和方法，所以子类比父类拥有的更多的能力。在实际开发中，我们经常会用子类对象去替换掉一个父类对象，这是面向对象编程中一个常见的行为。

子类继承父类的方法后，还可以对方法进行重写（重新实现该方法），不同的子类可以对父类的同一个方法给出不同的实现版本，这样的方法在程序运行时就会表现出多态行为（调用相同的方法，做了不同的事情）。多态是面向对象编程中最精髓的部分，当然也是对初学者来说最难以理解和灵活运用的部分。


### 简单的总结

面向对象编程是一种非常流行的编程范式，除此之外还有**指令式编程**、**函数式编程**等编程范式。由于现实世界是由对象构成的，而对象是可以接收消息的实体，所以**面向对象编程更符合人类正常的思维习惯**。类是抽象的，对象是具体的，有了类就能创建对象，有了对象就可以接收消息，这就是面向对象编程的基础。定义类的过程是一个抽象的过程，找到对象公共的属性属于数据抽象，找到对象公共的方法属于行为抽象。抽象的过程是一个仁者见仁智者见智的过程，对同一类对象进行抽象可能会得到不同的结果，如下图所示。

<img src="https://gitee.com/jackfrued/mypic/raw/master/20210731182914.png" width="75%">

> **说明：** 本节课的插图来自于 Grady Booc 等撰写的《面向对象分析与设计》一书，该书是讲解面向对象编程的经典著作，有兴趣的读者可以购买和阅读这本书来了解更多的面向对象的相关知识。

Python是动态语言，Python中的对象可以动态的添加属性。在面向对象的世界中，**一切皆为对象**，我们定义的类也是对象，所以**类也可以接收消息**。通过继承，我们**可以从已有的类创建新类**，实现对已有类代码的复用。


### 例题:律所信息数据库


```python
class LawFirm(object):
    """律所信息
    数据来源 https://en.wikipedia.org/wiki/List_of_largest_China-based_law_firms_by_revenue
    """
    
    def __init__(self, name, founded, lawyers, revenue):
        self.name = name
        self.founded = founded
        self.lawyers = lawyers
        self.revenue = revenue # in millions
    
    def get_name(self):
        return self.name
    
    def get_age(self):
        import datetime
        founded = datetime.datetime.strptime(self.founded, "%Y-%m-%d")
        today = datetime.datetime.now()
        age = today - founded
        
        return age.days // 365, age.days - age.days // 365 * 365
    
    def get_lawyers(self):
        return self.lawyers
    
    def get_revenue(self):
        return self.revenue
        
    def revenue_diff(self, another):
        print(f"{self.name} 与 {another.name} 年收入差值为{abs(self.revenue - another.revenue)}百万元")
        
if __name__ == "__main__":
    
    law_firm = []
    law_firm.append(LawFirm("Dacheng", "1992-4-29", 8658, 2360))
    law_firm.append(LawFirm("King & Wood Mallesons", "2012-3-1", 2762, 1072))
    law_firm.append(LawFirm("Yingke Law Firm", "2001-8-14", 9000, 445))
    law_firm.append(LawFirm("Zhong Lun Law Firm", "1993-1-1", 1680, 443))

    for i in law_firm:
        print(i.get_name())
        print(f"创立年限: {i.get_age()[0]}年 {i.get_age()[1]}天")
        print(f"律师人数: {i.get_lawyers()}")
        print(f"年收入: {i.get_revenue()}百万元")
        print()
        
    law_firm[0].revenue_diff(law_firm[1])
```
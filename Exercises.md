* 题目1:求数据平均

你调查了某家律师事务所应届生的第一年的工资，想要知道这一家事务所的应届生平均工资是多少，要求使用函数

```python
salary = [25.3, 28.4, 30.5, 20.1, 34.2, 25.6, 27.9, 35.9]

def get_avg(salary):
    # 从这里开始写你的代码
    
    # 你的代码到这里结束

print(get_avg(salary))
```

<details>

<summary>
求平均代码
</summary>

```python
salary = [25.3, 28.4, 30.5, 20.1, 34.2, 25.6, 27.9, 35.9]

def get_avg(list1):
    return sum(list1) / len(list1)

print(get_avg(salary))
```

</details>


* 题目2：对数字进行排序。

程序分析：可以利用选择法，即从后9个比较过程中，选择一个最小的与第一个元素交换，下次类推，即用第二个元素与后8个进行比较，并进行交换。

```python
if __name__ == "__main__":
    N = 10
    # input data
    print ('请输入10个数字:\n')
    l = []
    for i in range(N):
        l.append(int(input('输入一个数字:\n')))
    print(l)

    # 排列10个数字
    # 从这里开始写你的代码
    
    # 你的代码到这里结束
    print ('排列之后：')
    print(l)
```



<details>

<summary>
排序代码
</summary>

```python
if __name__ == "__main__":
    N = 10
    # input data
    print ('请输入10个数字:\n')
    l = []
    for i in range(N):
        l.append(int(input('输入一个数字:\n')))
    print(l)

#     排列10个数字
    for i in range(N - 1):
        min = i
        for j in range(i + 1,N):
            if l[min] > l[j]:
                l[j], l[min] = l[min], l[j]
#     l.sort()
    print ('排列之后：')
    print(l)
```

</details>

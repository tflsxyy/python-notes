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

    # 排列10个数字
    for i in range(N - 1):
        min = i
        for j in range(i + 1,N):
            if l[min] > l[j]:
                l[j], l[min] = l[min], l[j]
    # l.sort()
    print ('排列之后：')
    print(l)
```

</details>


* 题目3：利用Excel表格里的信息创建律师函发送给不同公司

程序分析：利用openpyxl读取表格里每个公司的数据，并利用docx按顺序填入律师函模板中，替换的位置为每个“CYJ”出现的地方，生成的每份律师函用每个公司的名字保存。

<details>

<summary>
生成律师函代码
</summary>

```python
import re

import openpyxl
from docx import Document
from docx.oxml.ns import qn
from docx.shared import Pt


# 打开工作簿（Workbook）
wb = openpyxl.load_workbook('律师函.xlsx')
# 读取工作表（Worksheet）
sheet = wb.worksheets[0]

# 律师函模板文件
template_file = '律师函.docx'

for company in sheet.values:
    # 使用模板实例化Document对象
    document = Document(template_file)
    for info in company:
        # 遍历模板文件的每一个段落
        for y in document.paragraphs:
            # 利用正则表达式，检查当下段落是否含有"CYJ"
            check = re.search('CYJ', y.text, flags=re.M)
            if check is not None:
                # 如果含有"CYJ"，则将"CYJ"替换为当下的子列表元素，只能替换一次
                y.text = y.text.replace('CYJ', info, 1)
                y.style.font.size = Pt(12)
                break
    # 保存新文件
    new_name = '律师函(' + company[0] + ').docx'
    document.styles['Normal'].font.name = '楷体'    
    document.styles['Normal']._element.rPr.rFonts.set(qn('w:eastAsia'), '楷体')
    document.save(new_name)
```
</details>

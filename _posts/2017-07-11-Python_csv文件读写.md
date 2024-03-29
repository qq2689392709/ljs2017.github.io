---
title: csv 读取写入
date: 2017/07/11 17:15:53
categories: 
- 随记
tags: 
- xlsxwriter
- xlrd
- Python
---

### csv文件读写

> csv:Comma Separated Values ,逗号分隔值
>
> .csv是一种文件格式，其实是一种特殊的文本文件格式
>
> 特点;字符之间使用英文逗号或者tab键分隔，主要用来不同程序之间进行数据的交互
>
> 注意：在Windows下可以通过excel，文本文档，notepad++,Editplus等

#### 1.读取csv文件

> 代码演示：
>
> ```python
> #第一步：导入模块
> import  csv
> 
> #第二步：经典的三部曲
> def readCsv1(path):
>     #1.打开文件
>     csvFile = open(path,"r")
>     #2.将文件对象转换为可迭代对象【读取内容】
>     csvReader = csv.reader(csvFile)   #result = f.read(),result本身就是文件中的内容
>     #print(type(csvReader))
> 
>     #3.获取内容
>     infoList = []
>     for item in csvReader:
>         print(item)
>         infoList.append(item)
>     #print(infoList)
> 
>     #4.关闭文件
>     csvFile.close()
> 
>     return  infoList
> 
> #第三步：简写方式
> def readCsv2(path):
>     infoList = []
>     with open(path,"r") as csvFile:
>         csvReader = csv.reader(csvFile)
>         for item in csvReader:
>             infoList.append(item)
> 
>     return infoList
> 
> #第四步：采用普通的方式读取csv文件:可以读取，但是，最终将其中的内容只是当做普通的文本读取出来
> #注意：但凡涉及到csv文件的读取，尽量采用特有的方式
> def readCsv3(path):
>     csvFile = open(path,"r")
>     result = csvFile.read()
>     print(result)
>     csvFile.close()
> 
> 
> path = r"csvFile.csv"
> readCsv3(path)
> ```

#### 2.写入csv文件

> 代码演示：
>
> ```python
> import  csv
> 
> #一.从列表写入csv文件
> def writeCsv1(path):
>     #1.定义一个列表
>     list1 = [['username', 'password', 'age', 'address'], ['zhangsan', 'abc123', '534', 'china'], ['lisi', 'fhhf', '56', 'beijing']]
>     #2.打开文件
>     #注意：默认每写入一行，会出现一个空行,newline消除空行
>     csvFile1 = open(path,"w",newline="")
> 
>     #3.将文件对象转换为可迭代对象
>     csvWriter = csv.writer(csvFile1)
> 
>     #4.写入内容
>     for i in range(len(list1)):
>         csvWriter.writerow(list1[i])
> 
>     #5.关闭文件
>     csvFile1.close()
> 
> #二、从字典写入csv文件
> def writeCsv2(path):
>     dict1 = {"张三":10,"李四":36,"jack":6}
> 
>     csvFile2 = open(path,"w",newline="")
>     csvWriter2 = csv.writer(csvFile2)
> 
>     for key in dict1:
>         csvWriter2.writerow([key,dict1[key]])
> 
>     csvFile2.close()
> 
> 
> #三、简写形式
> def writeCsv3(path):
>     list1 = [['username', 'password', 'age', 'address'], ['zhangsan', 'abc123', '534', 'china'],
>              ['lisi', 'fhhf', '56', 'beijing']]
>     with open(path,"w") as csvFile3:
>         csvWriter3 = csv.writer(csvFile3)
> 
>         for i in range(len(list1)):
>             csvWriter3.writerow(list1[i])
> 
> 
> path = r"file2.csv"
> writeCsv2(path)
> ```

### 
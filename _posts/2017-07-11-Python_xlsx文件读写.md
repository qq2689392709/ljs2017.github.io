---
title: xlsx 读取写入
date: 2017/07/11 17:15:53
categories: 
- 随记
tags: 
- xlsxwriter
- xlrd
- Python
---

### 1.xlsx 写入

```Python
# 写入
import xlsxwriter

# 创建工作簿
file_name = "D:\\book.xlsx"
workbook = xlsxwriter.Workbook(file_name)

# 创建工作表
worksheet = workbook.add_worksheet('first_sheet')

# 写单元格
worksheet.write(0, 0, 'Hello')
worksheet.write('A2', 'wold')

# 写行
worksheet.write_row(2, 0, [1, 2, 3, 4, 5, 6])
# 写列,其中列F需要大写
worksheet.write_column('F2', ['a', 'b', 'c', 'd'])

# 关闭工作簿
workbook.close()

```

### 2.xlsx 读取

```python
# 读取
import xlrd

def fileload(filename = '待读取.xlsx'):
    dataset = []
    workbook = xlrd.open_workbook(filename)
    table = workbook.sheets()[0]
    for row in range(table.nrows):
        dataset.append(table.row_values(row))
    return dataset

print(fileload('D:\\book.xlsx'))
```


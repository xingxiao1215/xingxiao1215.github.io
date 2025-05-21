---
title: Python基础
date: 2025-05-21 18:29:49
tags:
categories: 代码 
---

---

# **Python编程入门指南**  

---

## **一、开发环境搭建**
### 1.1 Python解释器安装
- 官网下载地址：https://www.python.org/downloads/  
- 安装时务必勾选 **Add to PATH** 选项，确保命令行可直接调用  
- 验证安装：终端执行 `python --version` 查看版本号  

### 1.2 开发工具选择
- 新手推荐：Thonny（内置调试器与可视化执行功能）  
- 专业开发：VS Code + Python插件（支持虚拟环境管理）  
- 命令行交互：Jupyter Notebook（适合数据分析场景）  

---

## **二、核心语法基础**
### 2.1 第一个程序：Hello World
```python
print("Hello, World!")
```
- **说明**：`print()` 函数用于输出文本，字符串需使用单引号或双引号包裹  
- **扩展**：可在字符串中使用转义字符（如 `\n` 表示换行）

### 2.2 变量与数据类型
```python
# 变量赋值无需声明类型
age = 20                # 整型 int
height = 1.75           # 浮点型 float
name = "Alice"          # 字符串 str
is_student = True       # 布尔型 bool
```
- **类型转换**：  
  ```python
  int("123")        # 字符串转整数
  float(3)          # 整数转浮点数
  str(True)         # 其他类型转字符串
  ```

### 2.3 运算符与表达式
| 运算类型 | 运算符                  | 示例                      |
|----------|-------------------------|---------------------------|
| 算术运算 | `+ - * / // % **`       | `2 ** 3` → 8              |
| 比较运算 | `== != > < >= <=`       | `"abc" == "ABC"` → False  |
| 逻辑运算 | `and or not`            | `not (5 > 3)` → False     |

---

## **三、程序控制结构**
### 3.1 条件分支
```python
score = 85
if score >= 90:
    grade = "A"
elif score >= 80:     # elif 可链式判断
    grade = "B"
else:
    grade = "C"
print(f"Your grade is {grade}")
```
- **注意**：冒号 `:` 后的缩进（4空格为规范）定义代码块

### 3.2 循环结构
#### （1）确定次数循环
```python
# 计算1-100的和
total = 0
for i in range(1, 101):   # range(起始, 终止, 步长)
    total += i
print("Sum:", total)
```

#### （2）条件循环
```python
# 猜数字游戏
secret = 42
guess = int(input("Input a number: "))
while guess != secret:
    guess = int(input("Try again: "))
print("Correct!")
```

---

## **四、数据结构**
### 4.1 列表（List）
```python
fruits = ["apple", "banana", "cherry"]
fruits.append("orange")      # 添加元素
fruits.remove("banana")      # 删除指定元素
fruits[0] = "grape"          # 修改元素
```
- **切片操作**：`fruits[1:3]` → 获取索引1到2的元素

### 4.2 元组（Tuple）
```python
coordinates = (10, 20)
# coordinates[0] = 5  # 报错！元组不可变
```

### 4.3 字典（Dictionary）
```python
student = {
    "name": "Bob",
    "age": 20,
    "major": "Computer Science"
}
student["grade"] = "A"     # 动态添加键值对
```

### 4.4 集合（Set）
```python
unique_numbers = {1, 2, 2, 3}
print(unique_numbers)      # 输出 {1, 2, 3}
```

---

## **五、函数定义与使用**
```python
def calculate_area(radius):
    """计算圆的面积"""
    return 3.14159 * radius ** 2

def greet(name="User"):     # 默认参数
    print(f"Hello, {name}!")

# 调用函数
greet("Alice")
area = calculate_area(5)
print(f"Area: {area:.2f}")  # 格式化保留两位小数
```
- **文档字符串**：函数定义下的三引号注释可用于生成API文档

---

## **六、错误处理**
```python
try:
    num = int(input("Enter a number: "))
    result = 10 / num
except ValueError:
    print("请输入整数！")
except ZeroDivisionError:
    print("除数不能为零！")
else:
    print("结果是:", result)
finally:
    print("程序执行完毕")  # 无论是否异常都会执行
```

---

## **七、文件操作**
```python
# 写入文件
with open("example.txt", "w") as f:
    f.write("Hello\nWorld")  # 写入字符串并换行

# 读取文件
with open("example.txt", "r") as f:
    content = f.read()
    print(content)
```
- **模式参数**：  
  - `"r"` 读取  
  - `"w"` 写入（覆盖已有内容）  
  - `"a"` 追加写入

---

## **八、模块与包管理**
```python
# 导入内置模块
import math
print(math.sqrt(16))  # 输出4.0

# 安装第三方库
# 终端执行: pip install requests
import requests
response = requests.get("https://example.com")
```
- **虚拟环境**：使用 `venv` 创建独立依赖环境  
  ```bash
  python -m venv myenv
  source myenv/bin/activate  # Linux/macOS
  myenv\Scripts\activate     # Windows
  ```

---

## **九、学习路径建议**
 **学习资源**：  
   - 官方文档：https://docs.python.org/3/  
   - 书籍：《流畅的Python》《Python Cookbook》  
   - 在线评测：LeetCode、HackerRank  

---

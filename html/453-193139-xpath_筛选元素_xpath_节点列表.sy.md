---
show: step
version: 1.0
enable_checker: true
---

# 语法 html 生成

## 回忆

- 把前面的 requests 和最近的 etree 结合了
  - 通过 request 获得网页的 response
  - etree 通过 HTML 函数把他转化为一棵 etree 树

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669521450717)

- 流程跑起来了
- 但是元素筛选有点麻烦
- 有什么快速筛选元素的方法吗？🤔

### 搜索

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630547071875)

- 点击第一个开始研究

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630547145505)

- xpath 
	- 是 w3c 制定的标准
	- 是 xslt 标准的主要元素

### 路径表达式

| 表达式 | 描述 | 
|--- |--- |
| . | 选取当前节点 |
|  / | 从根节点选取 或 表示层级关系 |
| nodename | 在当前位置选择此类节点 | 
| // | 在任意曾记得子孙路径下 |
| .. | 选取当前节点的父节点 | 
| @ | 选取属性 |


![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630547289914)

- 这些东西怎么理解呢？
- 具体来看看

### 操作

- dom 树如下

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669525619191)

- 我们来试一下各种路径表达式

### nodename

```
import requests
from lxml import etree
response = requests.get("http://localhost")
b_html = response.content
et_html = etree.HTML(b_html)
et_element = et_html.xpath(".")
print(et_element)
```

- . 为当前节点
- 输出为html元素的列表
- html下面有什么呢？

### 输出

- 当前节点为html
	- 下面有head

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669526063986)

- 可以输出

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669526080303)

### 层级关系

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669526234839)

- 可以输出p元素列表

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669526259394)

###  再向下一层

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669526419016)

- 找到 a 元素列表

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669526455954)

### 任意层级下

- 任意层级下的em元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669526539230)

- 可以找到

### 当前节点

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669527130581)

- 当前节点
	- .

### 向上一层

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669526663256)

- 向上一层	
	- ..

- 什么都输出不出
- 具体实际是怎么用xpath的呢？

### 通过浏览器

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669527325250)

- 右键内容检查元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669527339987)

- 在元素查看界面右键复制-xpath
- 将该元素的xpath复制到剪贴板

### 使用xpath

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669527474403)

- /html/body/p[1]
	- /html
		- 根下的html下
	- /body
		- html下的body下
	- /p[1]
		- body 下的 第1个 p 元素
		- 注意这里并不是从0开始
		- 而是从1开始

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669527566939)

- 可以找到这个元素

## 总结

- 这次深入了 xpath
- xpath 可以用来筛选 xml 文件中的节点
- xpath 有一套自己的语法

| 符号 | 作用 |
|--- |--- |
| . | 选取当前节点 |
|  / | 从根节点选取 或 表示层级关系 |
| nodename | 在当前位置选择此类节点 | 
| // | 在任意层级路径下 |
| .. | 选取当前节点的父节点 | 
| @ | 选取属性 |

- 这个@选属性我们还没有试试
- 怎么用呢？🤔
- 下次再说👋

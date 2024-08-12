---
show: step
version: 1.0
enable_checker: true
---

# 语法 html 属性 attrib

## 回忆

- 上次了解元素的标签成员
  - tag
- etree.Element最重要的是
	- 构成一棵家族树
- 了解 树 中的元素关系
  - 父子 
	- isparent()
  - 哥哥
	- isprevious
  - 弟弟
	- isnext()

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668854537523)

- html元素的属性可以在程序里面找得到吗？🤔

### 查看文档

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630461037878)

- etree 元素的属性很像像一个字典 dict
- 我们来试试

### 构造环境

```bash
sudo service nginx start
cd /usr/share/html
vi food.html
```

- 首先找到nginx网站根目录位置
	- 然后在根目录下编辑food.html

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702174515259)

### food.html

- 网页文件如下

```html
<!DOCTYPE html>
<html lang="zh-cn">
	<head>
		<title>menu</title>
		<meta charset="utf-8">
	</head>
	<body width="700px" id="mybody">
		<h1>menu</h1>
		<ul id="ulist">
			<li>
				<span class="food">豆汁</span>
				<price>10</price>
			</li>
			<li>
				<span class="food">羊瘪汤</span>
				<price>15</price>
			</li>
			<li>
				<span class="food">折耳根</span>
				<price>20</price>
			</li>
		</ul>
	</body>
</html>
```

### 尝试保存文件

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702174703218)

- 由于权限问题	
	- 文件无法保存

```
:w !sudo tee %
```

- % 代表当前编辑的文件名
- :w !{cmd} 是一个vim命令
	- 会执行{cmd}命令
	- 并将当前编辑的文件内容作为标准输入传入
- 在这个例子中
	- {cmd}是"sudo tee %
	- 这意味着它会以超级用户的权限
		- 将当前编辑的文件内容保存到当前文件中

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702174820692)

### 写后结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702174838411)

- 写完之后强制退出

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702174909072)

- 观察写后的文件

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702174942403)

### 尝试在浏览器中访问

```
firefox http://localhost/food.html
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702175158890)

- 确认网页已经存在
	- <kbd>ctrl</kbd> + <kbd>c</kbd> 结束火狐进程

### 构造结构

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702175284199)

- 回到~
	- 编辑爬虫文件

```python
import requests
from lxml import etree
response = requests.get("http://localhost/food.html")
b_html = response.content
et_html = etree.HTML(b_html)
print(et_html.attrib)
for attribute in et_html.attrib:
    print(attribute,et_html.attrib[attribute])
```

- 运行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231022-1697978177395)

- 确实可以看到属性
- 可以用得到key和value吗？

### items

```python
import requests
from lxml import etree
response = requests.get("http://localhost/food.html")
b_html = response.content
et_html = etree.HTML(b_html)
for key,value in et_html.attrib.items():
    print(key,value,sep=":")
```

- 结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231022-1697978589180)


### 得到属性

- attrib 是节点元素的属性字典
  - 属性字典是节点元素的成员变量
  - 属性字典的类型是一个字典

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630461979008)

- 可以用 get 和索引的方式得到属性的值

### 操作属性

```
import requests
from lxml import etree
response = requests.get("http://localhost/food.html")
b_html = response.content
et_html = etree.HTML(b_html)
et_body = et_html.xpath("/html/body")[0]
for key,value in et_body.attrib.items():
    print(key,value,sep=":")
```
- 执行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231022-1697978975842)

### 属性操作

- 索引方式有报错风险
	- 还可以使用get的方法

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668857510613)

- 效果一样

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668857530187)

- 尤其是当你不确定属性是否存在的时候

### 避免索引报错

- 不存在的属性
	- get会返回None
	- []索引会报错

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668857699571)

- 使用 get 的操作相对更安全
	- 索引可能会爆出 key 不存在的 KeyError
	- 不过也可能呢找不到bug

## 总结

- 这次了解etree.Element的attrib
  - attrib
  - 属性对象本质是一个字典
  - 可以用 get 和索引的方式得到具体的值
  - 使用 get 的方式更安全

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668858225490)

- 除了标签和属性组成员之外
  - 元素类还有文本成员
- 这文本成员怎么理解呢？🤔
- 下次再说
  - 使用 get 的方式更安全


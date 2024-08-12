---
show: step
version: 1.0
enable_checker: true
---

# 语法 html 生成

## 回忆

- 上次深入了 xpath
- xpath 可以用来筛选 xml 文件中的节点
- xpath 有一套自己的语法


| 符号 | 作用 |
| --- | --- |
| . | 选取当前节点 |
|  / | 从根节点选取 或 表示层级关系 |
| nodename | 在当前位置选择此类节点 | 
| // | 在任意层级路径下 |
| .. | 选取当前节点的父节点 | 
| @ | 选取属性attribute |

- 这个@选属性我们还没有试试
- 怎么用呢？🤔

### 直接搜索元素

```python
import requests
from lxml import etree
response = requests.get("http://localhost")
b_html = response.content
print(b_html)
et_html = etree.HTML(b_html)
l_et_element = et_html.xpath("//a")
for element in l_et_element:
	print(element)
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670027535333)

- 任意路径下的a元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670027552580)

### 根据属性类型筛选

- //a[@href]
	- //a
		- 任意路径下的a元素
	- [@href]
		- 有@href属性的

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670027751966)

- 任意路径下有href属性的a元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670027759394)

- 这里中括号的方法叫什么呢？

### 根据属性值筛选

- 中括号叫做谓词

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670027868489)

- 任意路径下
	- 有href属性值为http://nginx.org/的
	- a元素
- 注意引用属性值单引号或者双引号都可以

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669542517451)

### 根据是否有属性谓词筛选

- //a[@*]
	- //a 
		- 任意路径下的a元素
	- [@*]
		- []是筛选谓词
		- @是attribute
		- *是任意的

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670027653580)

- 任意路径下 有任意属性的 a元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670027673635)

### 双重谓词

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670029048298)

- 任意层级下的
	- 位置小于2的
		- 有href的a元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670029184013)

- 可以成功得到元素
- 如何理解谓语呢？

### 谓语 predicates

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670028229949)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630552360248)


### 观察网页

```python
import requests
from lxml import etree
response = requests.get("http://localhost")
b_html = response.content
print(b_html)
et_html = etree.HTML(b_html)
l_attrib = et_html.xpath("//a/@href")
print(l_attrib)
```


![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669541813289)

- a 元素 有 href 属性

### xpath

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670027314021)

- 任意路径下a元素的
	- href属性

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669542041751)

- 遍历成功
- 如果不对a元素进行筛选呢？

### href

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669542128636)

- 任意路径下任意元素的
	- href属性

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669542166221)

- 目前可以筛选到属性
	- 可以根据属性值筛选元素吗？

### 尝试

- 这里面出现了索引运算符[]
- 找一下/html/body下	
	- 第 1 个 p

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669542698464)


### 最后一个

- /html/body/
	- 最后一个p元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669542854651)

- 在索引运算符中使用了 last()
	- 此时last() = 3


### 倒数第二

- 倒数第二个p

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669542974392)

- 关键还是对 li 使用索引运算符
  - last()是最后一个
  - last() - 1 是倒数第二个

### 前两名 position

- 前两个p

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669543060055)

- p[position()<3]
	- 可以找到前两项
- 如果我想找后两项呢？🤔

### 后两项 

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670028432090)

- p[position()>last()-2]
- 可以找到后两项

### 存在href属性的a元素

- 拥有href属性 的 a元素 🤪

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669546658719)


- 可以试试href属性是特定值吗？

### 属性内容

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221127-1669546941736)

- href属性是 http://nginx.org 的a元素

### 总结

- 这次深入了 xpath 的筛选
  - 可以用中括号索引的方式对于子元素的位置进行筛选
    - 第一个
      - xpath("//p[1]")
    - 最后一个
      - xpath("//p[last()]")
    - 正数前三个
      - xpath("//p[position()<=3]")
    - 倒数两个
      - xpath("//p[position()>last()-2"])
  - 可以在索引中对属性进行筛选
    - @ 俗称花 a
    - 对应@ttribute
    - 可以找出有这个属性的元素
      - et_html.xpath("//*[@href]")
    - 也能找到属性是特定值的元素
      - et_html.xpath("//*[@href=\\"http://nginx.org/\"]")
  - 位置、属性筛选还可以配合节点筛选
    - et_target = et_html.xpath("//a[last()][@href=\\"http://nginx.org/\"]")
- 还有什么好玩的呢？🤔
- 下次再说

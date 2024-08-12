---
show: step
version: 1.0
enable_checker: true
---

# 语法 html 遍历

## 回忆

- 上次已经在内存构建了一棵 etree 树了
- 树是由节点 Element 构成的
- Element 元素的成员有:
  - attrib 属性字典
  - text 具体文本
  - tail 后跟文本
  - tag 标签
  - iter() 迭代器函数
    - iter 是深度优先遍历
    - 可以对tag进行筛选
- 除了etree.Element之外
	- 网页中还有什么对象吗？🤔


### 实体和注释

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630463857945)

- 为 root 元素增加了两类对象
  - etree.Entity("#234") 实体
  - etree.Comment("some comment") 注释
  - 还有原来的etree.Element("h1")
- root 元素本身是 
	- etree.Element 对象
- Entity 和 Comment 是另外两类对象
  - 作为 root 元素的子对象
    - 可以遍历
  - 但是不属于 etree.Element 元素类的对象
- iter()函数中用参数 tag=etree.Element 可以进行筛选
- Entity 元素本身只包含
  - text 成员
- Comment 元素包含
  - 头尾的注释标记
  - 具体的注释内容

### 添加实体

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669457946281)

- 为body元素添加Entity("#234")

```python
from lxml import etree
et_html = etree.Element("html")
etree.SubElement(et_html,"head")
etree.SubElement(et_html[0],"title").text = "oeasy"
etree.SubElement(et_html,"body").text = "o2z"
et_html[1].append(etree.Entity("#234"))
print(etree.tostring(et_html,pretty_print=True).decode())
```

### 输出重定向

```
:w|!python3 % > 1.html
```

- 输出重定向到1.html

```
:!firefox 1.html
```

- 然后用火狐打开1.html

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458003513)

- 出现了ê这个字符
- 这个ê是什么呢？

### 观察字符

- ê的序号是234

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458085251)

- 查看源文件
	- 看到源文件中的 实体
	- Entity

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231017-1697546153712)

- 可以换个序号输出吗？
- 我们试试

### 汉字

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458203480)

- 得到序号

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458215941)

- 确实输出了指定序号的汉字

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458223383)

- 可以输出emoji符号吗？

### emoji

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458325252)

- 得到序号

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458345799)

- 生成实体

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458353714)

- Comment怎么玩呢？

### Comment

```python3
from lxml import etree
et_html = etree.Element("html")
etree.SubElement(et_html, "head")
etree.SubElement(et_html[0], "title").text = "oeasy"
etree.SubElement(et_html, "body").text = "o2z"
et_html[1].append(etree.Comment("i am comment"))
print(etree.tostring(et_html,pretty_print=True).decode())
```

- 生成comment

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458780584)

### 浏览

```
firefox 1.html
```

- 浏览网页时
	- 右键检查源文件

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669458819057)

- 可以看到源文件中的注释
- 所谓注释Comment
	- 就是网页里面看不到
	- 但是源文件里面可以看到的
	- 对源文件的解释
	- 用`<!--` 和 `-->` 包裹起来的
- etree.Comment和etree.Entity很像
- 我们这样就可以将内存中的etree输出到html文件了
- 可以控制输出时候的缩进吗？

### 控制缩进

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630505528348)

- 根据文档

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669460191258)

- 输出缩进

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669460207547)

- 可以把缩进改为4空格吗？

### 调整缩进

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669460280148)

- 可以调整吗？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669460300493)

- 确实是有效的 
- Entity 和 Comment 可以被遍历出来吗？

### 遍历实体和注释

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669459173609)

- 结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669459637978)

- 遍历的时候可以筛选Entity和Comment吗？

### 筛选

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669459779067)

- iter()函数的参数
  - tag=etree.Entity - 筛选出 Entity 实体对象
  - tag=etree.Element - 筛选出 Element 元素对象
  - tag=etree.Comment - 筛选出 Comment 注释对象

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669459724547)

- 现在可以在内存里生成操作这颗 etree 树了
- 可是怎么将字符串快速转化成 元素树呢？

## 总结

- 已经在内存构建了一棵 etree 树了
	- 树是由节点 Element 构成的
	- 除了 etree.Element 节点之外，还有

| 对象名 | 对象类型 |
| --- | --- |
| etree.Entity | 实体 | 
| etree.Comment | 注释|

- Element 元素最重要，他的成员有:
  - attrib 属性字典
  - text 具体文本
  - tail 后跟文本
  - tag 标签
  - iter() 迭代器函数
    - 可以用 for 遍历迭代器函数
    - 参数 tag=etee.Element 可以类型进行筛选
- etee.indent()函数
	- 可以控制 etree.Element 输出的缩进
    - etree.indent(root, space="\t")
- etree.tostring()函数
	- 可以输出网页文件
    - `etree.tostring(et_html,pretty_look=True)`
- 能否 通过字符串
	- 比如 "\<html>\<head>\<title>o\</title>..."
		- 直接生成一棵etree树呢？ 🤔
- 下次再说

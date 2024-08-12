---
show: step
version: 1.0
enable_checker: true
---

# 语法 html 生成 etree

## 回忆

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

### 从字符串生成

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630503765091)

```python
from lxml import etree
some_xml_data = "<root>data</root>"
root = etree.fromstring(some_xml_data)
print(root.tag)
print(etree.tostring(root,pretty_print=True).decode())
```

- 确实可以生成etree元素树
- 虽然这棵树只有一个节点

### 生成

- 可以看到
  - 可以根据字符串生成 etree 元素节点(Element)
	- 你给他一个字符串
	- 他给你一个 etree 根节点
	- 里面的text属性会自动设置好

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669466951252)

- 节点的根目录标签
	- 取决于字符串最外层的标签
- 能否用一个网页文本
	- 来生成一棵etree树呢？

### 生成 etree

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630466004301)

```python
from lxml import etree
root = etree.fromstring("<html><head/><body><p>Hello<br/>World</p></body></html>")
etree.indent(root,space="\t")
print(etree.tostring(root,pretty_print=True).decode())
```

### 运行结果

- 这样确实
	- 可以通过字符串来生成一棵 etree

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231017-1697548063264)

- 我们就把 
	- 从网页得到的字符串 和 etree 
	- 关联起来了
- 不过我们 要的
	- 不是 xml
	- 而是 html

### 生成 html

- 首先查询文档
	- 找到 HTML 
		- parsers 语法分析器
- HTML Parser
	- 可以将 不那么标准的HTML
	- 生成 etree

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211017-1634436427443)

- Parsing HTML
  - HTML 就是网页
  - Parsing 就是把纯文本的 html 变成 html 语法树型结构
  - 也就是生成我们的 etree

### 动手

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669467418516)

- 将 XML方法
	- 更换为 HTML方法

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669467386432)


- 如果只有部分元素
- 也可以生成一棵 html 树么？

### 部分元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630504602875)

- 这次应该是可以生成 html 元素

```python
from lxml import etree
root = etree.HTML("<p>data</p>")
etree.indent(root,space="\t")
print(etree.tostring(root,pretty_print=True).decode())
```

- 而且可以自动补全整个的结构

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231017-1697548271033)

- 语法分析器
	- 会分析出目前的标签情况
	- 自动补全这棵树
		- 把`<p>`相关内容
			- 放在 html 的根下的 
			- body 节点的下面
	- 就像浏览器那样健壮
- 如果 html 是错乱的标签还能生成树么？

### 错乱标签

- 仔细观察
  - 发现 broken_html
	- 其实是混乱的 html 源代码
  - 缺少一些结束标签
  - 这也可以生成一棵完成的 etree 吗？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211017-1634436427443)

- 浏览器也经常面对这类情况
  - 它能够容错
- 这个事情就是 libxml2.6.21 以上的库帮助我们完成的
  - 包括补充头尾标签

### 动手试试

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220712-1657599575592)

- 绝大多数情况下
	- 会补全结束标签
	- 消除不相关的结束标签
- 不过世事无绝对

### 特殊情况

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220712-1657599630558)

- p元素应该是属于body元素的
- 不过这里让隶属于head元素
- 这种情况很少
- 错的实在太离谱
- 连个body都没有
- 毕竟巧妇难为无米之炊

### 移除空格

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630504914540)

- 照猫画虎


```python
from lxml import etree
parser = etree.HTMLParser(remove_blank_text=True)
root = etree.HTML("   <p>  data    <b> strong   </b>    </p>    ", parser)
print(etree.tostring(root))
etree.indent(root,space="\t")
print(etree.tostring(root))
print(etree.tostring(root,pretty_print=True).decode())
```


![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630505103633)

- 标签之间没有意义的空格被删除掉了
- 注意删除的是标签之间的
  - 而不是标签内部的

### 编码问题

- 例子代码

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630466274184)

- 我们简化这个代码

### 操作

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669469486700)

- 本身没有什么问题

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669469500993)

- 甚至可以看到输出重定向的网页

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669469552082)

- 问题出现在tostring函数中
	- 当method = "text" 时

### 转化为纯文本

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669469710572)

- 问题是

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669469760718)

- b"\xf6" 
	- 无法用默认的ascii 进行解码
- 那是为什么？

### 字符集与编码格式

- unicode是字符集
	- 只提供字符对应序号
	- 不能编码进入字节
- utf-8是编码方式
	- 可以编码进入字节

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669469907656)

- b"\xf6" 是1个字节
	- 里面存储的是
		- ö 序号的16进制字节形态
- b"\xc3\xb6" 是2个字节
	- 里面存储的
		- ö 在utf-8编码下的字节形态
- 这个默认的utf-8解码解不出来b"\xf6"怎么办呢？
	- 观察tostring的细节

### 设置编码

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669471415277)

- 先把默认编码设置为utf-8

### utf-8

- 这个字符的 unicode 编码是`\xf6`
	- 传输的时候需要使用 utf-8
	- 编码为 utf-8 方式后
	- 占据两个字节
		- 为`\xc3\xb6`

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630466672155)

- 然后再用utf-8解码就可以了

### 修改代码

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669471466342)

- 执行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221126-1669471507544)

### 过程

- text属性的类型是string
	- tostring默认得到的是 unicode 编码的字节流 bytes
	- 传输时需要把他变成 utf-8 编码的字节流
	- 输出的时候还需要把他从 utf-8 解码为具体的字符串

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211016-1634393857739)

- 进行输出

## 总结

- 终于可以通过字符串构建一棵 etree 的节点树了
	- 通过 etree.HTML()函数将网页源文件进行 parse(语法分析)生成一棵 etree
	- 通过 etree.HTMLParser()函数设置 parser 空格情况
		- `parser = etree.HTMLParser(remove_blank_text=True)`
    - 这个 parser 的作用是去除标签间不相关的空格
    - 用 parser 作为生成树的时候的参数
         - `root = etree.HTML("<root> <a/> <b> </b> </root>", parser)`
- 我能用本章最初的 requests 爬到的字节序列
	- 生成 etree 元素么？
- 把一切串联起来
  - 将request 得到的 response 的 content
	- 当做 etree.HTML()需要的参数
- 直接将爬到的内容生成节点树？🤔
  - 这可能吗？
- 下次再说👋

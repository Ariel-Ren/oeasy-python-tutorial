---
show: step
version: 1.0
enable_checker: true
---

# lxml 元素 树形结构

## 回忆

- 导入了 requests 模块
- request可以帮我们发送http请求	
	- 这样我们就可以假装自己是一个浏览器
	- 完成了 http get 的过程
	  - 发出了 request
	  - 得到了 response
	  - 状态码 200
- 但是读到的内容是
  - r.content 字节序列
  - r.text 字符串序列
- 如何解析 html 语言呢？🤔

### 分析

- 想要解析 html
	- 那首先就要了解 html 语言的结构
- `html`全称`h`yper-`t`ext `m`arkup `l`anguage
  - 是一门 markup(标记性) 的语言
  - `markup` 是靠 `html` 元素 实现的

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630451887662)

- 元素 使用的 `标签(tag)` 包括
  - 开始标签
  - 结束标签
- 标签是成对儿出现的

### 实例

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630452159874)

- F12 可以检查元素
	- 也可以右键全部展开
	- 这就是一棵树
- 一棵什么树？

### Dom树

- 一棵 Dom 树

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668823401607)

- 什么是 Dom 树呢？

### Dom 树

- Document Object Model
  - 文档对象模型

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630453123602)

- 根节点在 html元素
	- html元素 长出两个分支
	  - head元素
	  - body元素
- 然后各自底下
	- 还有子分支

### 渲染过程

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668824125270)

- response 到达浏览器后
  - 首先需要分词 parse
  - 然后根据语义 semantic
  - 尝试生成一棵 dom 语义树
  - 然后再根据 css 样式表
  - 一步步地进行渲染成一个好看的页面

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668824141134)

- 爬虫也需要渲染吗？

### 爬虫

- 爬虫只看内容
	- 不需要渲染
  - 但也需要先生成 dom 树

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668824279118)

- 怎么生成呢？
  - 尝试引入一个包

### lxml

- 这是目前分析 html 最好的包
  - lxml
  - 是第三方的包

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630453359293)


- 第三方的包哪里查询帮助呢？

### 搜索

- 在百度搜索lxml

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630453447141)


- 这是一个开源的项目 lxml
  - http://lxml.de
	 - github 的地址也指向这里
  - l 的意思是 library
  - xml 的意思就是 e`x`tensible `m`arkup `l`anguage
- 整体的意思就是一个能够简单地处理 xml 的 python 库

### 打开lxml.de

- 他的特点是
  - 用 c 语言写了
	- 高效的 libxml2 和 libxslt 两个类库
	- 并封装成的 api
  - 使用 python 的简洁语法调用
  - 生成著名的 ElementTree

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630453454445)


- 他可以解析 xml
  - 也可以解析 html
- 其实 html 是 xml 的一个子集
  - 毕竟都是 ml(Markup Language)
  - 树型结构

### tutorial

- 进入教程

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630453747733)

- 本来想着是 
	- 读取一个网页文件
	- 然后再生成树
- 但是 目前看起来的思路是
	- 在内存里直接 通过调用函数 生成树
	- 然后 再处理这棵树
- 树嘛
	- 首先要有树根节点

### 扎根

- etree 的意思是
  - element tree
	- 元素树
  - 元素树树是由元素节点构成的

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668824641142)

- 哪个元素是整棵树的根呢？

### html元素

- 获得节点的方式是
  - etree.Element("html")
- 我们知道 html 元素 
	- 是网页文档的根
    - 所有其他元素的根
    - 也是 从无到有生成这棵树的根

```
from lxml import etree
et_html = etree.Element("html")
print("et_html", et_html)
print("et_html.tag", et_html.tag)
```

- 变量名是 et_html
  - et 代表他是 element_tree节点 类型的
  - html 代表他是 html 根节点

### 运行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668824985944)

- 运行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668824997169)

- 先把根扎下之后
  - 需要开枝散叶

### 开枝

```
from lxml import etree
et_html = etree.Element("html")
et_body = etree.Element("body")
print("et_html:", et_html)
print("et_html.tag:", et_html.tag)
print("et_body:", et_body)
print("et_body.tag:", et_body.tag)
```

### 运行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668825103811)

- 结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221119-1668825158114)

- 但是html节点和body节点的关系是什么呢？
## 总结

- 了解了 html 中的 dom 树
- 树是由节点元素组成的
  - 节点元素可以用 etree.Element()得到
  - 最根本的元素是根元素
  - dom-tree 的根就是 html 元素
- html 里面包括子节元素点
  - head
  - body

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630453123602)

- 如何建立节点之间的父子关系呢？🤔
- 下次再说

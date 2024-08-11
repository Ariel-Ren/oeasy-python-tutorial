---
show: step
version: 1.0
enable_checker: true
---

# xpath 路径表达式

## 回忆

- 上次深入了 xpath 的筛选
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

### 构造环境

- 首先在用户宿主文件夹
	- 建立一个网页

```bash
vi food.html
```

- 网页文件如下

```html
<!DOCTYPE html>
<html lang="zh-cn">
	<head>
		<title>menu</title>
		<meta charset="utf-8">
	</head>
	<body width="700px">
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

- 复制到剪贴板后
	- 在插入模式下进行粘贴
	- 用<kbd>g</kbd><kbd>g</kbd><kbd>=</kbd><kbd>G</kbd>调整缩进

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670030602904)

- 然后保存并退出

### 启动web服务器

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670030012452)

- 将网页文件拷贝至web服务器根下
- 并启动web服务
- 用火狐访问到网页

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670030659782)

### 尝试访问

```python
import requests
from lxml import etree
response = requests.get("http://localhost/food.html")
b_html = response.content
print(b_html)
et_html = etree.HTML(b_html)
l_element = et_html.xpath("//li")
for element in l_element:
	print(l_element)
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670030822973)

- 访问任意元素下的li元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670030848235)

- 访问成功
- 尝试使用谓词

### 属性比较

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630566795961)

- 参考上面的例子

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630568001180)

- 根据网页的结构
	- 尝试修改xpath
- et_target = et_html.xpath("//li[price>=20]")
  - 找到 1 条 li
- et_target = et_html.xpath("//li[price>=15]")
  - 找到 2 条 li
- et_target = et_html.xpath("//li[price>=10]")
  - 找到 3 条 li

### 继续研究

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630568371007)

- 根据上面的例子

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630568001180)

- et_target = et_html.xpath("//li[price<=10]/span")

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670031300427)

- 10 元以内(含10元)的食品名称

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670031314170)

- 注意获取的是节点的 text

### 通配符

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630568599049)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630568001180)

- 具体怎么用呢？

### 选中

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670031450673)

- et_target = et_html.xpath("\*")
  - 匹配当前节点(html)下的直接子节点

- 共两个 head、body	
- 要选出所有的元素节点应该如何呢？

### 所有元素节点


```python
import requests
from lxml import etree
response = requests.get("http://localhost/food.html")
b_html = response.content
et_html = etree.HTML(b_html)
l_et_element = et_html.xpath("//*")
for element in l_et_element:
	print(element)
```

- et_target = et_html.xpath("//\*")
  - 匹配任意路径下的任意节点
  - 相当多

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220701-1656645264113)

- 而且是深度优先的
- 如果我要筛选出所有有属性的元素节点呢？

### 有属性的所有节点

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670031564597)

- et_target = et_html.xpath("//\*[@\*]")
  - 匹配任意路径下的全部有属性的节点
  - 数量稍有减少

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670031591129)

- 还有什么可玩的？

### 尝试访问

```python
import requests
from lxml import etree
response = requests.get("http://localhost/food.html")
b_html = response.content
et_html = etree.HTML(b_html)
l_attributes = et_html.xpath("//@*")
for attrib in l_attributes:
	print(attrib)
```

- 查询结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231022-1697976158324)

### 路径并集

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630569224426)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630568001180)

- et_target = et_html.xpath("//h1|//price")
  - 符合前面//h1 或者符合后面//price 都可以

### 具体代码

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670031647049)

- 实现结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221203-1670031679443)

- 基本上 xpath 的用法我们了解了
- 这xpath怎么来的呢？

### xpath 的源头

- xpath 是谁定的？
- 为什么会有 xpath？
- 这还要从头说起

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630569561042)

- 早年间文本没有统一的交换格式
	- 为了交流的方便
	- 国际标准化组织 iso 制定了标准 SGML
		- Standard Generalized Markup Language 
		- SGML 是国际上定义电子文件结构和内容描述的标准
		- SGML 具有非常复杂的文档结构
		- 主要用于大量高度结构化数据的访问和其他各种工业领域
		- 在分类和索引数据中非常有用

### SGML

- SGML 是 描述数据的数据
	- 就是元数据
- 使用的方式 是 给文本添加标签
	- 标签本身 也是 文档的一部分

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630569551704)

- 后来 读写文件 
	- 开始依赖于 互联网浏览器
	- 一种新的标签标准 在实践中诞生

### html

- 在各种网络数据交换工具的试探实践中
	- html这种超文本语言出现了
	- 同时期浏览器出现了
	- 或者说对于html这种标签的渲染工具出现了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630570031771)

- 1989 年
	- HTML 诞生
		- Tim Berners-Lee
		- 最先在自己的 next 机器上建立了这种语言
	- HTML 抛弃了 SGML 复杂庞大的缺点
		- 继承了 SGML 的很多优点
		- HTML 最大的特点是简单性和跨平台性
- 浏览器各种兼容和试新的过程中进化

### 目前状态

- 我们看的网页都是html

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630569932502)

- 但是 html标签 毕竟是基于网页的
	- 不是基于 数据本身的
	- 随着 数据量的发展
	- xml 出现了

### xml

- HTML 描述的是网页渲染时候的结构
	- 但不描述数据类型和结构
	- 可读性差、搜索时间长
		- 1998 年 2 月 10 日
		- W3C(World Wide Web Consortium，万维网联盟)
		- 公布 XML 1.0 标准
- XML 诞生了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630570251257)

- 但是如何让xml渲染成人眼能够接受的页面呢？

### xslt

- 为了让 xml 看起来更好看
	- XSLT 规范出现了
	- 是渲染xml的规范

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220701-1656642715446)

- XSLT 对于 xml
	- 就像 css 对于 html
- xml、html
    - 楼房结构
    - 是语义
- xslt、css
	- 是具体的楼房装修风格
	- 是外观

- 除此之外
	- 还有对于xml的筛选工具

### xpath

- 其中的 xpath 是关于 xml 元素筛选的标准

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630570677195)

- https://www.w3.org/TR/2010/REC-xpath20-20101214/#context

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210902-1630570705394)

- `xpath` 的意思 就是 `x`ml `path` language

### 回到历史

- xml(e`X`tensible `M`arkup `L`anguage)
	- 是为了解决html标签太过面向渲染而不面向数据而产生的
	- 是html的升级
	- 本质上也是一种特殊的SGML(`S`tandard `G`eneralized `M`arkup `L`anguage)
- xslt(E`x`tensible `S`tylesheet `L`anguage `T`ransformations)
	- 是为了解决xml呈现能力而产生的
	- 是css的升级
	- 本质上也是一种特殊的SGML
- 说到底又回到了最初
	- SGML

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220701-1656643739364)

- 虽说回到了最初
- 但这个最初已经不是1986年那个纸质的最初了
- 纸张的东西放到了网页中

### 吞噬

- 就连1986年的纸质文档也数字化了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220701-1656643834774)

- 最初之前的更初呢

### 更初

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220701-1656643864383)

- sgml来自于gml
	- generic markup language


![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220701-1656643913342)


- gml是一种文档格式的脚本
	- gml是ibm用来描述文档标题格式用的
	- 定义了
		- 段落
		- 标题
		- 列表
		- 表格等
- 是为了当时渲染设备
	- 针式打字机服务的一种语言
- gml还可以往前倒么？

### ml

- markup language
	- markup 其实就是 make up
	- 起源就是用笔做笔记或者标记
	- 这是标签做标记的起点

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220712-1657603357016)

- 此后一路发展
	- ml标记方式的可能性很多
	- 所以要一种通用的generic
		- gml
	- gml需要规范化所以需要standard
	- 这就是sgml
- 当然再往前倒也可以
	- markup language来自于language
	- 语言和劳动创造了人本身
	- 这就有点太远了。。。
		- 我也知道。。。
- 所以我们打住
	- 去总结一下


### 总结

- 这次深入了 xpath 中的元素选择
  - 可以根据元素层级关系选择
  - 也可以根据元素位置选择
  - 还可以根据属性具体值选择
  - 而且可以根据文本的值进行选择
  - 甚至开始使用通配符
- xpath 是整个爬取的核心
  - 有什么东西可以练习么？🤔
- 下次再说

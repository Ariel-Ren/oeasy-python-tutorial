---
show: step
version: 1.0
enable_checker: true
---

# 语法 html 属性 attrib

## 回忆

- 了解了 html 中的 dom 树
- 树是由节点元素组成的
  - 节点元素可以用 etree.Element()得到
  - 最根源的元素是根元素
  - html 树的根就是 html 元素
  - 或者说 dom-tree 的根就是 html
- html 里面包括子节元素点
  - head
  - body
    - ul
- 重复类型的元素怎么追加呢？🤔

### 继续

- 直接添加列表
- 失败了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630458028665)

- 看来 etree.Element()元素的子节点
  - 不能是列表 list 对象
- etree元素 是递归的
	- etree元素 下面只能是 etree元素
- 聪明反被聪明误
	- 还是老老实实来逐个添加(append)

### 逐个添加(append)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630459987697)

- 这次仿佛成功了

### 索引(index)方式选择元素etree 节点

- etree元素 也可以用索引方式选择 子etree元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460162190)


- 可以用索引找到下级元素
	- 这一点有点像列表
	- etree元素 不是列表 

### 切片(slice)方式选择元素

- etree元素 也可以用索引方式选择子节点

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460277972)

- 切片选择的结果类型是列表
	- 列表中的列表项是 etree元素

### 判断是否是元素

- 判断是否是元素
- 如果是元素
  - 有几个子元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460368714)

- 可以用 len 得到元素的子元素数量

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460447051)

- 是否可以遍历etree中的所有子元素呢？


### 遍历元素

- 参照例子

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460561706)

- 遍历html元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460569619)

- body下面还有元素呢？
- 我还想往下遍历

### 继续遍历

- 循环遍历body元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220711-1657535747386)

- body里面有个ul元素
- 我希望body里面有两个元素h1和ul
- 而且h1是哥哥，ul是弟弟
- 可能么？

### 思考

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220711-1657535798685)

- 目前的结构是这样的
- 如果`et_html.append(et_h1)`会导致h1会被追加append
- h1一定是弟弟
- 除了append还有其他函数么？

### insert

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220711-1657535912265)

- 那怎么查到相关的帮助呢？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220711-1657535977679)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220711-1657535983720)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220711-1657536026555)

- 这个元素和列表为什么那么相像？
	- 函数名、遍历方法、索引切片
	- 都太像了


### 元素赋值

- 原来 Element 元素这个类最早是从 list 列表类派生出来的
- 所以继承了很多列表的特性
- Element 的 tag 属性对应标签的名字

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460612269)

- 不过有些地方和列表不同
  - 赋值的时候
  - 被替换元素会把原来位置的子元素替换掉
  - 被替换元素从原来的位置被删除
- 看完例子
- 我们去验证一下

### tag

- 验证一下 Element 元素的 tag 属性

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211106-1636192693875)

- 再验证一下子元素的替换

### 子元素替换

- 把一个子元素掰到别的地方

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211106-1636192792753)

- 元素替换之后
	- 旧的就没有了

### 深拷贝

- 如果想要新建一个类似的 etree 节点
- 可以考虑深拷贝

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460822360)

- 我们自己构建一个例子

### 构建

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220711-1657536298907)

- 然后尝试添加元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220912-1662974840012/wm)

- 第一个子元素和最后一个子元素真的不同么？

### 添加元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220711-1657536340606)

- 第3个元素标签是child1
- 但是并不是root[0]元素的那个child1标签元素

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220912-1662974911994/wm)

- 是新复制出来的child1
- 两个元素地址不同 

### 父子兄弟

- 判读是否是父亲

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460949130)

- 判断是否是哥哥或弟弟

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460957729)

### 动手尝试

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630460965035)

- 通过节点得到
  - 父亲
  - 哥哥
  - 弟弟

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630453123602)

- 伦理清晰

### 属性

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630461037878)

- etree 元素的属性很像像一个字典 dict
- 我们来试试

### 属性字典

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630461635127)

- 可以为元素设置属性和属性值

### 遍历属性

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630461726672)

- 这真的很像一个字典
- 这就是一个字典

### 属性对象

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630461979008)

- attrib 是节点元素的属性组
  - 属性组是节点元素的成员变量
  - 属性组的类型是一个字典
- 可以用 get 和索引的方式得到属性的值

### 属性操作

- 索引方式有报错风险

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210901-1630462069699)

- 使用 get 的操作相对更安全
	- 索引可能会爆出 key 不存在的 KeyError
	- 不过也可能呢找不到bug

## 总结

- 了解 etree 中的元素关系
  - 父子
  - 兄弟
- 了解元素的标签成员
  - tag
- 了解元素中的属性组成员
  - attrib
  - 属性对象本质是一个字典
  - 可以用 get 和索引的方式得到具体的值
  - 使用 get 的方式更安全
- 除了标签和属性组成员之外
  - 元素类还有文本成员
  - 这文本成员怎么理解？🤔
- 下次再说

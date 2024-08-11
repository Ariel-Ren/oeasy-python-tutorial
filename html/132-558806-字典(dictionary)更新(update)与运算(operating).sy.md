---
show: step
version: 1.0
enable_checker: true
---

# 字典类型

## 回忆

- 次学习了字典
  - 字典项可以增删改
  - 字典还可以赋值
  - 字典项也可以是复杂的数据的结构
- 字典可以运算么？🤔

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220830-1661863497865)

### 查询文档

- 我想手动给字典添加键值对(key-value pair)
	- 可以么？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220830-1661863573759)

- 好像有个update
	- 可以用一本字典更新另一本


### 字典更新

- 字典的合并使用 update
	- 两本字典放在一起
	- 合成一本字典

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210914-1631608478627)

- 这个函数名字是 update
  - 就和集合的并集是一样的
- 但是如果两个字典对于同一个 key = a 的值不一致
  - 怎么办？

### 字典更新

- 试试

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210914-1631608534953)

- 以后面的为准
- 用d2更新d1么
- 相当于
	- d1["a"] = 2
	- 一个key只能有一个值
	- 所以这个字典项被更新了
- 这其实也就是可以让字典添加元素了
- 还有其他方法么？

### 快速写法

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220830-1661863724891)

- 直接更新
- 这和update有什么不同么？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220830-1661863791017)

- update把更新后的字典赋给前面的d1
	- 这个时候d1改变了
- 而merge_dict = {**d1, **d2}是返回一个值
	- 结果交给新字典merge_dict
	- d1、d2都没有改变

### 添加

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210914-1631608626758)

- 这个dict(b=2)
	- 究竟是什么呢？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220919-1663544814817)

- 绕了一圈
	- 最初的问题还是解决了
	- 可以手动给字典添加键值对了
- 甚至可以把构造函数dict()省略

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220919-1663545049745)
 
- 从汇编角度如何理解？

### 汇编角度

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220801-1659325326659)

- 调用了函数update

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220801-1659325345342)

- 把key的元组中加上'z'
- d1["z"]的值设置为4
- 除了 update
	- 还有一个 setdefault 命令
	- 也可以添加字典项

### setdefault

- 设置默认值怎么理解呢
	- 查看帮助

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210914-1631609246349)

- 试试

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220919-1663545287800)

- 设置默认值首先是设置一个值
- 那怎么理解默认呢？

### 默认 default

- 如果以前这个 key 设置过默认值的话
	- 再想设置新的默认值是不行的
	- 就返回原来的默认值

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210914-1631609226776)


- 如果以前没有设置过这个key的默认值
	- 设置这个key的默认值
		- 就插入这个字典项
	- 并返回这个默认值
- 设置默认值之后不能再设置默认值(setdefault)
- 那我就想更新怎么办呢？

### 赋值

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220706-1657094255127)

- update和=赋值还是可以直接更新字典的
- 和setdefault不同
- setdefault是试着设置
- 那有没有试着获取呢？

### 问题

- 我们用传统的dict[key]获取

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220830-1661860499424)

- 如果我们用传统方法
- 就会出现KeyError😱
- 去查文档

### 查询

- help(dict)
	- 查询dict帮助手册
- /get
	- 查询手册中的get
- <kbd>n</kbd>
	- 下一个字符

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220830-1661860416357)

- 有这个字典项
	- 返回相应的值
- 没有的话
	- 返回default的值
	- default 默认值为None

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220920-1663641456898/wm)

- default参数如何理解？

### default

- default参数为默认返回值

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220920-1663641549832/wm)
 
- setdefault是试着添加字典项
- get是试着查字典
- 都是试着来
- 下面交给你一个例子

### 武将排名

- 一吕二赵三典韦

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220706-1657095124010)

- 需要添加
	- 4关5马6张飞

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220830-1661859872889)

- 如果我想把马超和张飞位置互换应该如何？
- 这个排名使用字典或者列表
	- 各自优劣是什么？
- 最后我们总结一下

### 新单词总结

- dictionary 字典
- key 键
- value 值
- item 项
- mapping 映射

### 总结

- 这次学习了字典
- 字典可以更新
	- update
	- {**d1,**d2}
- 可以试着来
	- 试着设值setdefault
- 试着取值get
  - 字典还可以赋值
  - 字典也可以合并
- 字典是非常常用的一种容器
- 还是总结一下各种容器吧😱
- 这还真是一个大总结呢😱
- 下次再说！👋🏻

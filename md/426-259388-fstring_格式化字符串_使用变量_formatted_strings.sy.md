---
show: step
version: 1.0
enable_checker: true
---

# fstring

## 会议

- 上次了解了 格式化输出函数
	- format
		- 可以设置各种格式
		- 也可以使用参数

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676603540471)

- 能否在字符串中 
	- 直接使用上下文中的变量呢？？🤔

### pep-498

- https://peps.python.org/pep-0498/

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676605955886)

- 与format函数不同

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676606267295)

- f-string可以
	- 直接访问上下文变量
- 可以控制
	- 宽度
	- 精度
	- 正负号
	- 这些吗？

### 格式控制

- 回顾format

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676607345144)

- f-string的格式语法
	- 完全一致

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676607376368)

- 整数语法也一致吗？

### 整数格式控制

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676607584480)

- 整数格式控制
	- 也与format一致

- 上下文的变量都能被找到吗？

### 例子

- 有的时候可能找不到
	- 比如下图中inner函数
		- 找不到x变量

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676612092848)

- 除非
	- 在子函数里面声明了x
		- x 引用outer中的 参数x
			- 于是就可以用了
- 如果就想在f-string里面
	- 使用大括号怎么办呢？

### 使用大括号

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676612886594)

- 两个大括号
	- 相当于一个大括号
	- 很像转义字符
- f-string 有什么用吗?

### 数字精确位数

- 以前研究过的
	- 0.1 + 0.2 == 0.3

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231210-1702181742797)

- 在二十位小数的情况下就清清楚楚了

### 处理函数

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676612941158)


- 具体效果如何呢？

### 具体效果

- 确实有这样的对应关系

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676613035896)

| !a | !s | !r |
| --- | --- | --- |
| ascii()| str() | repr() |

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676613106339)

### 总结

- 我们这次研究了f-string
	- f-string的意思是格式化后的字符串
	- 格式化的过程中
		- 可以引用上下文中的变量
		- 从而得到相应的最终值

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676613676557)

- 除了f-string之外
	- 好像还有一种r-string
- 这r-string怎么用呢？🤔
- 下次再说👋🏻
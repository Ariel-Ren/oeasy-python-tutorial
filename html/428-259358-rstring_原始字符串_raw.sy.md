---
show: step
version: 1.0
enable_checker: true
---

# r-string

## 回忆
- 上次研究了f-string
	- f-string的意思是格式化后的字符串
	- 格式化的过程中
		- 可以引用上下文中的变量
		- 从而得到相应的最终值

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676613676557)

- 除了f-string之外
	- 好像还有一种r-string
- 这r-string怎么用呢？🤔

### 回忆b-string

- 我们其实以前学过一种b-string

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676613927796)

- b-string 得到字符串的字节状态
	- 相当于得到字符串对应的编码
- f-string 是什么意思来着？

### f-string

- f的意思是
	- format
		- 按照格式来生成 字符串

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676626473294)

- 那么这个r-string是什么意思？

### r-string

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676628177744)

- 效果和三引号基本一样
- 既然有了三引号
	- 为什么还需要r-string呢？

### r-string的意义

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676613787235)

- r和f
	- 可以配合

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676628534371)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676629370565)

- 这和上次的!r
	- 有点像啊

### 回忆具体效果

- repr 效果 
	- 可以保留单引号

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676613035896)

| !a | !s | !r |
| --- | --- | --- |
| ascii()| str() | repr() |

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676613106339)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230217-1676598819617)

- r-string 还可以和 f-string一起配合
	- 构成格式字符串的基本方式

### 总结

- 这次研究是的r-string
	- 先回忆了
		- b-string
		- f-string
- r-string的作用是查看raw格式的文本
	- 反斜杠\
	- 单引号'
	- 双引号"
	- 都会保留
- 我们可以根据这些规则
	- 制作一个进度条呢？🤔
- 下次再说👋🏻

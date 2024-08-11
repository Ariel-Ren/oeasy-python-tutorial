---
show: step
version: 1.0
enable_checker: true
---

# 你好世界 🥊

## 回忆上次内容

- 这次我们，
  - 了解了 Python
  - 进入了 Python
  - 退出了 Python
- 这并不难
	- 这就是我们对于 Python 的初体验
- 恭喜您存活了下来！

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220830-1661829248204)

- python 还有什么好玩的呢？🤔

### 你好世界

```bash
#首先进入Python3
python3
```

- 我们想要来个`Hello World！`
- 然后直接输入

```Python
#貌似程序都是从hello world开始的
Hello World
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220919-1663582657256)

- 好像系统报告了错误 😡
- 这可怎么办？

### 不怕报错

- 不怕报错
	- 告诉你哪儿错了
	- 就知道怎么改了
	- 比不报错强

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210302-1614682783779)

- 及时的反馈有助于我们快速学习
- 这就是python学习环境的好处

### idle

- 这是一个集成的学习开发环境
	- Integrated Development and Learning Environment 
	- 也叫idle

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220919-1663563402647)

- 系统还挺友好
	- 告诉我错在哪了 😌
	- 那我错哪儿了？

### 加上引号

- 通过报错
	- 我们知道了这是一个 SyntaxError
	- 语法错误 
- 他不认识 Hello World

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210302-1614683021899)

- `hello world` 应该是字符串
- 需要给他两边加上双引号 `"hello world"` 引起来
- 这回真的输出了！！！
	- 但是好像输出也有引号
	- 加的是双引号
	- 输出的却是单引号？
- 如果两边都加单引号呢？

### 字符串

- 按方向键<kbd>↑</kbd>可以找到之前运行的命令
	- <kbd>↑</kbd>、<kbd>↓</kbd>可以进行命令切换
	- <kbd>ctrl</kbd>+<kbd>a</kbd>可以将光标跳转到开头
	- <kbd>ctrl</kbd>+<kbd>e</kbd>可以将光标跳转到结尾
- `hello world`两边都加单引号

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220909-1662706016968)

- 不管输入的是单引号还是双引号
	- 输出的都是单引号
	- 效果是一样的
- 这种被引号引用的内容叫做
	- `字符串`
	- 意思是一串字符
- 字符串可以有加减乘除么？

### 字符串加法

- 两个字符串加在一起就是拼合字符串

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220909-1662708938747)

- 中间可以有空格么？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220909-1662708964500)

- 前面或者后面的单词加上空格都可以
- 如果想要前后两个单词都是独立单词呢？

### 连加

- 中间加上一个空格就可以

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220909-1662709098823)

- 但是`hello world`两边总有引号
- 我想要的是直出 `hello world`
	- 两边没有引号

- 应该怎么样做呢？
- 先胡乱尝试一下🤪

### 直接输出

- 理论上来说应该有个输出函数
- 显示输出英文是什么？
  - `display`
  - 但是系统又报了错 ❌

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220909-1662706179627)

- 每次回车无论对错都会有反应
	- 这次的问题是什么？
- NameError
	- 游乐场根本不认识这个display
	- 输出函数的英文是什么呢？

### 输出

- 输出函数的英文是
  - `print`
- 这不是打印么？
  - 我们用的是显示器啊
  - 没有用打印机

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220919-1663583444022)

- 至少游乐场认识这个名字
	- 没有出现NameError
	- 游乐场认为print是一个内建(builtin)的函数(function)
	- 是游乐场里面的东西
- print 应该如何理解？

### print缘起

- Python 诞生于 1990s
  - 给他带来启发的语言诞生于 1960s、1970s
  - 当时的机器使用电传打字机进行输出
	 - 代码里的输出都使用 print 函数
	 - 就成了一个文化
- 我直接把 `print` 这个函数名放到游乐场里面
  - 系统告诉我 `print` 是一个内建函数 `built-in function`
- 我乱敲一个`asdf`到游乐场里
  - 报给我一个 `NameError` 
  - 说不认识

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210916-1631760771502)

- 这就是交互式编程环境的好处
	- 啥都告诉你
	- 有来有回的
- 这个过程就叫做 REPL
	- 什么是REPL呢？🤔

### REPL

- Read - Evaluate - Print - Loop
- 读取 - 执行 - 打印输出 - 循环这个过程

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210815-1628992142150)

- 循环起来 
- 无论对错
	- idle都会给我们一个反馈
	- 让我们不断试错
	- 直到找到正确的方式

### 加上括号

- `print` 是一个函数
	- 函数后面必须得加上一对小括号
	- 就像 `quit` 一样
	- 小括号里面放置参数
	- 如果什么都不放的话

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220909-1662707071926)

- 会输出一个空行
- 我们先放一个 `h`
  - 但是不行
  - 因为系统把 `h`当做一个变量名
  - 不认识 `h`

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210916-1631760875828)

- 那怎么办？

### 加上引号

- 必须给 `h` 加上双引号
  - `"h"` 成为一个字符串
  - 字符串就能当 `print` 函数的参数

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210815-1628992210954)

- 这次输出的h两边没有引号了！！！

- 我们了解一下为什么用🧐
  - 括号
  - 引号

### 括号含义

- ()括号
  - 意味 print 是一个函数
  - 正在调用这个函数

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220919-1663583645719)

- `print()`
    - 输出空行
- `print(h)`
    - 游乐场说不认识h
- `print("h")`	
	- 输出字符串"h" 

### 引号含义

- 引号引号
	- 引用字符串的符号
	- 引号把一些字符引用起来形成一个字符串
	- 就像引用名人名言一样
	- 所以引号叫做引号

```Python
#使用print函数
print("h")
```

- 输出"h"字符串
	- "h"就是 print 函数的参数

```
#输出oeasy
print("oeasy")
```

- 输出"oeasy"字符串
	- "oeasy"就是 print 函数的参数
- 参数放在小括号里
	- 回车输出～

### 拼写细节

- 如果一不小心拼写成 `pront` 的话

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210305-1614901655062)

- NameError
	- 拼写错一点儿都不行 😬
	- 叫错名字的话就找不到这个函数了
- 但如果单词没有拼错
	- 是大小写错了呢？🤔

### 大小写错误

- Print 的 P 是大写的

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220909-1662709209965)

- 报了NameError
- 这就是计算机愚蠢之处
	- 也是计算机可爱之处
	- 大写就是大写
	- 小写就是小写
	- 错一点都不行
	- 一就是一
	- 二就是二
- 我们去总结一下

## 总结

- 我们这次在解释器里玩耍
- 了解到字符串就是给一堆字符两边加引号
	- 可以是单引号
	- 也可以是双引号
	- 这样游乐场就知道
		- 这个不是一个名字
		- 而是一个字符串
- 字符串可以用print函数进行输出
	- 但是print千万不要打错
	- 就连大小写都不能错

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220919-1663563791305)

- 我们在游乐场玩了这么久
	- 能否写一个真正的python文件啊？🤔
- 我们下次再说！👋


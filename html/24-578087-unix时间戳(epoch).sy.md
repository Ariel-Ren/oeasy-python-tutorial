---
show: step
version: 1.0
enable_checker: true
---

# 输出时间

## 回忆上次内容

- 通过搜索
	- 我们学会 `import` 导入 `time` 了
- 完整写法为
  - asc_time = time.asctime( time.localtime( time.time()))

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221007-1665146302633/wm)

- 内部函数是在`__builtins__`这个包里面的自带的
  - 比如 quit()
- 这一大长串的函数究竟应该如何理解呢？？🤔

```python
import time
ascii_time = time.asctime(time.localtime(time.time()))
print (ascii_time)
```

### 嵌套的函数

- 这个一大串东西是有规律的
- 首先什么是 time

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220925-1664114987198)

- 这个包里面都有些什么呢？

### time包中

- time 是一个 module 模块包
  - 处理时间的包

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220925-1664115145674)

- 包里有各种函数
	- time.time()
	- time.localtime()
	- time.asctime()
	- 这三个都是time里面的函数

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210813-1628837673343)

- 例子是一行写成的
- 使用了函数嵌套调用
	- 我们试试把函数嵌套调用拆开
	- 不用嵌套
	- 分开写

### 分开写

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220318-1647597703048)

- 函数嵌套调用
	- 首先通过调用 time.time()函数 得到了ticks
	- 然后通过调用 localtime(ticks)函数 得到了localtime
	- 最后通过调用 asctime(localtime) 得到了asctime

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220318-1647598144662)

- 那么这些函数
	- time
	- localtime
	- asctime
	- 都是什么意思
- 分别help一下

### <span style="color:red">time</span>.<span style="color:green">time()</span>

- help(time.time)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210813-1628837778251)

- 这里有两个time有点乱
- 我们区分一下颜色
	- 前面的是红色的 <span style="color:red">time</span>
	- 后面的是绿色的 <span style="color:green">time()</span>
- <span style="color:red">time</span>.<span style="color:green">time()</span>
  - 红色的是 <span style="color:red">time</span> 这个包(module)
  -  <span style="color:red">time</span> 包(module)里面有很多函数(function)
  - 圆括号说明绿色的 <span style="color:green">time()</span> 是函数
  - 红色绿色之间的<kbd>.</kbd>的意思是 **里面的**
  - 从<span style="color:red">time</span> 包里调用 <kbd>.</kbd>(**里面的**) <span style="color:green">time()</span> 这个函数(function)
  - 这个 <span style="color:green">time()</span> 函数 就是  <span style="color:red">time</span> 包 **里面** 的函数
- 那么这个<span style="color:red">time</span>.<span style="color:green">time()</span>到底返回什么值呢？

### 调用

- 调用一下看看

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210813-1628837973195)

- 这一串长长的数字应该如何理解

### time.time()的意义

- 我们还是得返回来看帮助文件

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210813-1628837778251)

- 这个东西返回的是一个浮点型的数字
	- 浮点的浮是浮动的浮
	- 浮点的点是小数点的点
- 这个值是从Epoch到当前的时间总共过了多少秒
- 那什么又是Epoch呢？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220318-1647599035064)

### Epoch
- 发音是[ˈepək]
- Epoch 的意思是纪年方法或者说是年号
	- 公元2022年日本纪年法令和四年
	- 公元1587年是明朝万历十五年
	- 今年是耶稣纪年法2022年

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220925-1664115667284)

- 那python中的Epoch年号又是什么年号呢？

### unix纪年法

- unix纪年法(unix时间戳)
	- 从1970年1月1日开始的
	- 也就是1970-01-01T00:00:00Z
	- 格林威治时间 1970 年 1 月 1 日 00:00:00
	- 每过一秒这个数字就加1
	- 每过半秒这个数字就加0.5
	- 所以Epoch也叫做
		- seconds since the Epoch
- 为什么是1970-01-01呢？
	- 第一版unix的正式发布是在1971年
	- 编写c和unix工作是从1969年开始实施的
	- 大概率是`Kenneth Thompson`和`Dennis Ritchie`
	- 在1970年初一拍脑门定下来了这个起始时间点
- 最关键的是
	- 这个关于秒数的数据类型time_t也已然在后来成了标准c库的一部分
	- 因此被广泛运用在各种 类unix(Unix-like)的软件系统中
	- 比如我们用到的这个debian的变种ubuntu
- 所以 Epoch 也叫做
	- Unix Time
	- Posix Time
	- UNIX Epoch Time

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220127-1643289652075)

- time.time()得到的是一个浮点数
	- 但是我们要的是年份、月份、日期、时分秒这些具体的信息
	- 考虑到从闰年到闰秒的一系列难题
- 这个转化太麻烦了
	- 有什么办法么？

### time.localtime()

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210813-1628837796010)

- time.time()出来的浮点秒数交给 time.localtime()处理
  - time 还是包名
  - 这次的函数名变成了 localtime()
  - 输入是unix时间戳
  - 输出本地时间元组
	- 年份、月份、日期、时分秒这些具体的信息

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210813-1628838009501)

- 如果localtime函数的参数缺省
	- 默认使用time.time()作为参数
-  time.time()我们刚才研究过
	- time.time()就是当前时间的unix时间戳

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220311-1646960906335)

- 这两个结果是一样的

### time.asctime()

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210813-1628837821286)

- time.asctime 函数
	- 输入为time.localtime()输出的时间元组作为 
	- 输出为一个字符串
- asctime函数 接收时间元组产生 ascii 字符串
	- ascii 就是 ascii编码
	- asctime 就是 用ascii方式显示的 time

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220930-1664546111567)

- asctime函数也有缺省参数么？

### asctime的缺省参数

- 查询文档

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210813-1628837821286)

- 如果asctime函数的参数缺省
	- 默认使用time.localtime()作为参数
- 对的
	- time.localtime()就是当前时间的时间元组

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220311-1646961145760)

### 最后输出

- 我们都使用默认参数
	- 把函数嵌套大大简化了
- 把最后的结果交给 print()
	- 最终就能得到当前的时间！🤪

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220311-1646961221721)

- 我可以让时间刷新么？

### 手动延迟

- 我想要刷新这个东西怎么办？
	- 需要重新得到 `asc_time`
	- 然后重新输出 `asc_time`
- 这个过程可以手动来完成

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220317-1647499282065)

- 我想让他自动刷新起来
	- 先去编写一个py程序

### 编写程序

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220930-1664546772299)

- 运行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220311-1646961360615)

- 刷新完全靠手

## 总结

- time 是一个 `module`
	- import 他可以做和时间相关的事情
	- time.time() 
		- 得到当前时间戳
	- time.localtime() 
		- 得到本地时间元组
		- local为本地
	- time.asctime() 
		- 得到时间日期字符串
		- asc为ascii
- 简略的写法为
    - asc_time = time.asctime()
	- `time.asctime()`
	- asctime 是 time 这个 module 里面的函数
- 现在想要自动刷新时间，怎么办？🤔
- 我们下次再说！👋

---
show: step
version: 1.0
enable_checker: true
---

# 字符串类型_str_string_下标运算符_中括号

## 回忆上次内容

- 上次了解的是 
	- 转义字符 反斜杠
	- 转义转义 转化含义
	- 反斜杠和后面的字符 
		- 两个一起 构成转义序列
		- 转化了含义 

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231208-1702037778486)

- 字符串 变量 究竟是如何存储的呢？？🤔

### 类型和位置

- 先自省一下
	- 自省(introspection)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210817-1629166523239)

- 通过 type 函数获得 
	- 变量o 的类型
    - `str`
	- 就是 字符串 string

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210817-1629155102907)

- 通过 id 函数获得 
	- 变量o 的 唯一标志id
	- 也就是 在内存中的地址
	- 这个地址是一串数字

### 初始化过程

- 内存地址(`140547862959216`)
	- 存储了 "oeasy"字符串 
	- 地址 被赋给s_title变量名 

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210828-1630144191964)


- str 可以作为变量名吗？

### 注意事项

- str 是 字符串类名
	- 但是一旦被赋值 称为变量名
	- str就无法转化了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210828-1630144514499)

- 特别注意❗❗❗
	- 初学者要特别注意
	- 不要将str作为变量名！📢

- 可以 用字符串变量
	- 给 字符串赋值 吗？

### 用变量赋值
- s1 = "oeasy"
  - 这个字符串长度  5 个字节
	- oeasy
  - s1 位于 139633377299288
- s2 = "o2z"
  - 这个字符串长度 3 个字节
	- o2z
  - s2 位于 139633366623112

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210817-1629167725483)

- s2 = s1
  - 令s2 位于 id(s1) 
  - s2 和 s1 都指向 原来 s1 的地址
	- 会被系统垃圾回收

### 观察

- 去一个网站观察
	- https://pythontutor.com/visualize.html#mode=edit

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210829-1630203709851)

### 演示

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210829-1630208623942)

- 点击 Live Programming Mode
- 然后进入到实时编程模式

### 字符串运算

- 这种直接的计算
	- 并不能为内存中的变量赋值

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210829-1630209077502)

- 没有变量接收这些值
	- 这些值也就没有被任何变量引用
	- 这些值也就被垃圾回收了
- 在左边的帧(frames)的位置是空的
- 什么是frame呢？

### frame

- frame 也叫帧
	- 本意是画框

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231129-1701255743346)

- 现在尝试赋值
	- 把变量 画到画框里去

### 赋值

- 有两个变量
	- s1 
	- s2

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210829-1630209062770)

- 他俩 在 调用(call)栈(stack)的 帧(frame)上
	- 画出来了
	- 看得见了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220903-1662158505337)

- 可以用 prev 和 next 控制流程运行

### 之前的问题
```
s1 = "oeasy"
s2 = "o2z"
print(id(s1),id(s2))
s2 = s1
print(id(s1),id(s2))
```

- 运行效果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231129-1701256031127)


- 最终引用情况
  - 字符串"oeasy" 
	- 有两个变量引用(s1、s2)
  - 字符串 "o2z"
	- 原来 s2 所指向
	- 现在没有变量引用了

### 总结

- 这次了解的是 `字符串`
- 可以用str
	- 将整型数字 转化为 字符串
- 但是 不要让str成为变量名

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231129-1701256447307)

- 除了字符串
	- 还有什么变量类型？🤔
- 下次再说！👋

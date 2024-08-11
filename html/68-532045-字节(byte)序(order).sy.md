---
show: step
version: 1.0
enable_checker: true
---

# 进制转化

## 回忆上次内容

- 上次总结了四种进制的转化函数

- 数字 41 和字符串"41"的不同

| 函数名     | 前缀     | 目标字符串所用进制 |
| -------- | -------- | ----- |
| bin |   0b | 二进制 |
|  oct|   0o |八进制 |
| hex |  0x | 十六进制
|eval | 以上都有可能 |十进制|

- 字符串"41"
  - 两个字符
  - 字符转化为 ascii 序号
  - `\x34\x31`

- 数字 41
  - 转化为 二进制 0b101001
  - 两个字节前面补零
  - `\x00\x29`
  - 这就两个字节
- 但是这两个字节谁先谁后呢？

### 存储

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659269754647)

- 258 这个数字
- 如果用两个字节存储的话
- 字节状态是`\x01\x02`

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659269816826)

- 但是如何保证是两个字节呢？
- 我们借助一个包struct

### struct
- 导入struct包，并查看手册
	- import struct
	- help(struct)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659270621677)

- 2个字节有符号的整型数字
- 对应的符号应该是`h`

### 得到字节状态

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659270742329)

- 得到字节状态是`\x02\x01`
- 不是应该对应着 0x0102 么？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659269754647)

- 这数字可不能读错写错啊？

### 字节序


- 这涉及到一个东西叫做
  - 字节序

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211029-1635516032723)

- 这些可选的修饰字符暗示字节序
- 字节序有两种
	- `<`:little-endian
	- `>`:big-endian
	- 把这个修饰字节序的字符放在类型h(short)前面
		- `<h`:little-endian 2 bytes
		- `>h`:big-endian 2 bytes

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659271290044)

### 字节序对比

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211030-1635559712503)

- 这两个对应同一个数字
	- 0x12345678
- 但是字节序不同
	- BigEndian 
		- 从低地址开始
		- 在高地址结束
		- 也就是地址数值大的地方结束
		- 所以叫BigEndian
	- LittleEndian
		- 从高地址开始
		- 在低地址结束
		- 也就是地址数值小的地方结束
		- 所以叫LittleEndian

### little-endian $<h$   

- $<h$ 用的是小字节序
  - 编码模式属于 small-endian
  - 最低有效位（least significant byte）放在低地址 a

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211030-1635559260042)

- 这是目前常用的指令集架构 ($x86、x86-64$) 用的字节序
	- CISC(复杂指令集)
- 另一种字节序是大字节序
	- RISC(精简指令集)

### big-endian $>h$  

- $>h$  是按下图中的字节排序
  - 编码模式属于 big-endian
  - 最高有效位（most significant byte）落在低地址

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20211030-1635559602632)

- 这是目前 RISC 指令集架构 (RISC、MIPS) 用的字节序
- 这也是我们看起来比较顺的字节序
- python的字节码用的什么字节序呢？

### 汇编层面

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659271723024)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659271746661)

- 他用的是小端法
- 为什么呢？

### 查询cpu架构

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659272121830)

- x86-64属于复杂指令集CISC

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220731-1659270742329)

- 默认字节序为小端字节序

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220802-1659414621969/wm)

### 总结

- 这次我们研究了字节序
- 字节序有两种
	- big-endian $>h$  
	- little-endian $<h$   
- 这个可以用来明确整型存储的顺序
- 我们如果读写文件出了错
	- 可以考虑一下
	- 是否是因为字节序出的问题
- 变量可以声明、初始化了
- 但是又应该如何删除呢？🤔
- 下次再说👋

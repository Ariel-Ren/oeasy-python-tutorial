---
show: step
version: 1.0
enable_checker: true
---

# Hello World!

## 回忆上次内容

- 游乐场里面 已经装备了一些函数
	- help
	- dir
	- quit
	- print
	- chr
	- ord
	- 这些函数 位于 `__builtins__` 模块
	- 所以都是 内建函数
- 还是想把print函数删除掉
	- 可能吗?🤔

### 删除 print 函数

```
del __builtins__.print
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240521-1716298076398)

- NameError : name 'print' is not defined!😊
	- 这下啥都干不了啦!
- 如果我想要查询`__builtins__`模块
	- 更详细的信息 应该如何来着？
- 重启游乐场


### 详查模块

- 只查函数名目录

```
dir(__builtins__)
```

- 查询 函数 还有 对应的值

```
locals(__builtins__)
```

- 详细查看帮助

```
help(__builtins__)
```

- 可以 导入 
	- 外部模块 吗？

### 导入 外部模块

- 导入命令 是
	- import
		- port是港口 
		- import 是进口 、 导入
		- export 是出口 、 导出
	- import 后面`接空格`
- 被导入的模块 是
	- `__hello__`
	- 读作 `dunder hello`
	- 注意 hello 两边 
		- 都有dunder(双下划线)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230226-1677418325769)

- 把`__hello__`模块 导入到游乐场
	- 可以 输出那句程序员的浪漫

### 变化

- 注意！重进一次游乐场
	- 观察导入前后变化
- 导入 `__hello__`模块后
	- 游乐场中的模块 增加了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230226-1677418465935)

- 想要深入了解 `__hello__`
	- 应该怎么办呢？

### 什么不会就 help什么

```
help(__hello__)
```

- 使用help函数 查询手册

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220923-1663933594048)

- `__hello__` 是
	- 非常简单的 
	- 一个模块
	- 练手用的
- 各种 模块 	
	- 各自身怀绝技
	- 可以配合起来使用

- 有什么好玩的包吗？

### 反重力

- 在vim的正常模式下
	- 键入:!python3 
	- 进入游乐场
- 在游乐场中键入
	- import antigravity

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230528-1685281777708)

- 玩完了之后
	- <kbd>ctrl</kbd> + <kbd>d</kbd> 退出游乐场
	- 回到vim

### 观察LICENSE

```
cat /usr/lib/python3.8/LICENSE.txt
```

- 可以看到 python的 许可证

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240326-1711416359744)

- 除了中间几个版本 
	- 不兼容 gpl 协议
	- 原因是 Stallman 的律师 
	- 明确和 CNRI的律师说的 
- 我想把 许可证 
	- 做成 词云图 

### 代码

- 尝试 加载
	- 分词模块 jieba
	- 词云模块 WordCloud
	- 画图模块 matplotlib

```
import jieba
from wordcloud import WordCloud
import matplotlib.pyplot as plt

# 读取文件
with open('/usr/lib/python3.8/LICENSE.txt') as file:
    text = file.read()

# 使用jieba进行中文分词
words = ' '.join(jieba.cut(text))

# 生成词云
wordcloud = WordCloud(font_path='/usr/share/fonts/truetype/wqy/wqy-microhei.ttc', # 指定中文字体路径
                      width=800, height=600,
                      background_color='white').generate(words)

# 使用matplotlib展示词云
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.show()
```

- 执行结果
	- ModuleError
	- 找不到模块

### 安装模块

```
pip install wordcloud
pip install matplotlib
pip install jieba
```

- 安装后运行python
- 成功展示了 license的 图

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240326-1711417465440)

- 可以考虑修改
	- 高度
	- 宽度
	- 背景颜色

### dir()
 
- dir()可以得到
	- 当前作用域(scope)内所有的变量

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220727-1658883645478)

- 我们去试试

### 过程

- 下图就是变量a的一生

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220727-1658884446668)

- 让我们祈祷
	- a 往生 极乐世界

- 如果是下划线开头的变量呢？

### 下划线的含义

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230512-1683897803501)

- 所以 _a 可以作为
	- 模块内部的变量或者函数
	- from module import * 时 
	- 不被引用

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230215-1676466769187)

- 如何理解内部呢？

### 理解内部

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230512-1683897947284)

- 在random模块中有很多变量和函数
	- 有下划线 算是内部的
	- 没有下划线 不算是内部的
- from random import *
	- *代表所有的外部变量和函数 

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230512-1683898180552)

- 导入进来的
	- 都是没有下划线的
	- 也就是说内部的没有导入进来
- 如果就想要导入内部的变量呢？
## 总结

- 模块 就是 封装好功能的一个部件
	- 比如一个 wifi模块

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231122-1700645381698)

- 导入 `__hello__` module模块
	- 可以 输出`hello world!`

- 可以 做个 `自己的`模块吗？？🤔
- 我们下次再说！👋
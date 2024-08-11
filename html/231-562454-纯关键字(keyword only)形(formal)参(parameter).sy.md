---
show: step
version: 1.0
enable_checker: true
---

# 类型提示(type hint)

## 回忆

- 上次研究了纯位置(position)参数(parameter)
	- 纯位置参数在/之前
	- 纯位置参数只能用位置
	- 不能用关键字(keyword)
- 那和纯位置相对的
- 纯关键字(keyword only)
- 如何理解呢

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220829-1661783640535)

### 构造

```
import sys
def sentence(sub: str="I",\
             /,\
             pre: str = "love",\
             *,\
             obj: str = "you"):
    """
    a sentence is composed by 3 parts,
    sub is abbreviation of subject
    pre is abbreviation of predicate
    obj is abbreviation of object
    """
    frame = sys._getframe()
    code = frame.f_code
    print("co_argcount:",code.co_argcount)
    print("co_posonlyargcount:",code.co_posonlyargcount)
    print("co_kwonlyargcount:",code.co_kwonlyargcount)
    print(sub, pre, obj)

sentence(pre="like")
```

- sub 是纯位置形参
- pre 是两可形参
- obj 是纯关键字形参
- 我们先试试 pre 是否可以接受关键字实参

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662255788846/wm)

- 为什么参数总数是2呢？

### co_argcount

- 查看手册

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662255944361/wm)

- 纯关键字形参不计入co_argcount
- 这里面只记录纯位置形参和两可形参
- 谓语(pre)可以接受位置实参吗？

### 位置实参

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662256167644/wm)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662256180366/wm)

- 谓语(pre)是两可形参
	- 可以接受位置实参
- 宾语(obj)是纯关键字形参
	- 可以接受位置实参么？

### 纯关键字形参接受位置实参

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662256309818/wm)

- 报错了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662256327591/wm)

- 只能接受2个位置参数
	- 1个纯位置
	- 1个两可的
- 但是送过来3个位置实参
- 所以崩溃了
- 宾语改成关键字的

### 纯关键字形参接受关键字实参

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662256456861/wm)

- 没有问题

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662256473106/wm)

- 纯关键字形参当然能接受关键字实参

### 总结 

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662256639549/wm)

- 我们这次比较完整地了解了三种参数
	- 纯位置
		- / 之前
	- 两可
		- / 和 * 之间
	- 纯关键字
		- * 之后
- 顾名思义
	-  三类形参都有各自接受实参的方式
	-  不按方式来就报错
- 手册里还提到了`*` 和 `**args`

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220904-1662256698919/wm)

- 是什么意思？🤔
- 我们下次再说👋
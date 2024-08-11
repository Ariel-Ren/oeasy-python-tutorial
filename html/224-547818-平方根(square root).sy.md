---
show: step
version: 1.0
enable_checker: true
---

# 平方根(square root)

## 回忆

- 上次比较了两种做法
	- 两个函数
		- 先求因数集合
		- 再判断是否是质数
	- 一个函数
		- 求解出所有质因数
- 两种做法
	- 从算法上来说区别不大
	- 运行的结果是时间区别不大
- 实践证明函数调用的开销其实不大
- 功能最好拆分成高内聚、低耦合的函数
- 但是这个算法还可以优化么？

```
def get_factor_set(num):
    s = set()
    for i in range(2, num + 1):
        if num % i == 0:
            s.add(i)
    return s

def is_prime(num):
    for i in range(2,int(num / 2) + 1):
        if num % i == 0:
            return False
    return True

def get_prime_factor_set(num):
    s = set()
    for i in get_factor_set(num):
        if is_prime(i):
            s.add(i)
    return s


print(get_prime_factor_set(36))
```

### factor3.py

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661239368201)

- 复制文件之后
- 针对红框位置
- 想想是否可以优化

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220903-1662172060866/wm)

### 优化思路

- 开平方
	- 36的平方根是6
	- int(36/2)是18

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661239601961)

- 求97是否是质数
	- 判断range(1,10)就可以
	- 没有必要遍历range(1,48)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661239980837)

- 修改代码

### 优化后
```
import math
def get_factor_set(num):
    s = set()
    for i in range(2, num + 1):
        if num % i == 0:
            s.add(i)
    return s

def is_prime(num):
    sqrt = int(math.sqrt(num)) + 1
    for i in range(2,sqrt):
        if num % i == 0:
            return False
    return True

def get_prime_factor_set(num):
    s = set()
    for i in get_factor_set(num):
        if is_prime(i):
            s.add(i)
    return s

print(get_prime_factor_set(36))
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220903-1662172191192/wm)

-  想要和factor2.py比较

### 修改

- 先把factor3.py最后一句外层的print去掉

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661240420257)

- 然后比较factor2和factor3

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661240452517)

- 确实优化了
- 这个神奇的sqrt是怎么写的呢？

### 开平方根

- 作为一道相当出名的算法面试题
- 也有一些套路
	- 二分查找
	- 牛顿迭代
	- 卡马克法(雷神之锤III)
- python是怎么做的呢？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661259611055)

- 答案在mathmodule.c中

### 源码

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661259706265)

- 代码上面有注释
- 他说用的还是牛顿迭代
- 感谢写这个的大神！！！
- factor2可以用这个方式优化么？

### 修改

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661260415781)

- 在两个循环的range上都进行的优化
- 这次再来比较一下时间
- 注意最后一行去掉print
- 并且实参为36
- 和factor3保持一致

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661260680147)

- 速度提高3-5倍
- 如果把参数改为原来的1000000倍呢？

### 修改代码

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220823-1661261039062)

- 这时候差距就非常明显了
- factor3可以优化么？

### factor3

- 红框的位置理论上也可以先开根号的

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220903-1662179004838/wm)

- 但是如果那样
	- 就不是求所有因数的集合了
	- 比如36的因数包括9,12,18甚至36
	- 但是他们都大于sqrt(36) + 1
	- 改了就不是那个含义了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220824-1661313014831)

### 总结
- 函数的拆很容易
	- 但是不能为了拆而拆
	- 故意增加抽象层次
	- 还是要保持简洁
	- 保持高内聚低耦合
- 拆了之后也要能合上去
	- 必要时既有拆开的独立函数
	- 又有针对特定需求合起来的函数
	- 灵活应对
- 天下大势
	- 合久必分
	- 分久必合
- 代码效率和模块复用性不可兼得
	- 如何要找到其中的最大公约数
	- 什么是最大公约数？🤔
- 我们下次再说👋
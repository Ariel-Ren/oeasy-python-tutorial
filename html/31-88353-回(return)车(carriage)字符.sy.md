---
show: step
version: 1.0
enable_checker: true
---

# 回到开头

## 回忆上次内容

- 我们可以用 
	- <kbd>ctrl</kbd> + <kbd>z</kbd> 把当前进程切换到后台
	- 用 `fg` 可把进程再切回前台
	- `ps -lf` 查看进程信息
	- `kill -9 PID` 给进程发送死亡信号
	- `jobs` 查看所有作业
	- `fg %1` 可以把指定的进程切回前台
- 运行多个 `python3 sleep.py` 的话
	- 各个进程独立
	- `python3 sleep.py` 大概 7M
	- 各占内存
- 这个切进程很好用
	- 不过运行进程的时候总是满屏刷
	- 这个能解决吗？🤔

### 回到从头

- 我们从先去游乐场
- `\n`是我们熟悉的
- 我们先复习一下

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210221-1613905491259)

- 这次解锁的东西叫做`\r`
- `\r`的作用是回到输出头部的位置
- 如果原来的字符串比新的字符串长怎么办呢？

### return

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210923-1632387434289)

- `\r` 只负责回到头
- 其他的不管
- 不要翻篇，自己尝试修改`sleep.py`
- 让输出时间固定在一行

### 结合程序

- 这个程序和 sleep 的结合很简单
- 只需要把输出的字符串前面加上`\r`
- 并且把结尾默认的 end=`\n`换成 end=""

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220311-1646962549586)

- 试验成功
- 真的定在那儿刷新了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210221-1613906280764)

- 如果我把结束符设置为"\r"会如何呢？

### 突发奇想

```python3
#!usr/bin/python3
import time
while True:
    print('The time now is :',time.asctime(),end='\r')
    time.sleep(1)
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220824-1661330079255)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220326-1648306981989)

- 果然，不出所料
- 都给删除了
- 还有
	- 就是字有点小
	- 可以变大么？

### 字体变大

```bash
#安装figlet
sudo apt install figlet
#运行figlet
figlet "oeasy"
#利用管道使用figlet
echo "oeasy"|figlet
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210306-1614987482170)

### 变大原理

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220331-1648708095435)

- 把具体的ascii字符
- 映射到更大的字符组合上

### 管道原理

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210224-1614171987291)

- `管道运算符|` 就是水管子

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210306-1614987482170)

- 把 echo "oeasy"的输出结果
- 当做 figlet 的输入参数
- 再进行输出
- 我们尝试把时间输出当做 figlet 的输入

### 尝试整合

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210306-1614988251250)

- 运行失败了
- 我想先把那个`\r`去掉
- 但是还是不行
- 这里面只保留输出试试

```python
#!/usr/bin/python3
import time
print(time.asctime())
```

### 最终
```python
#!/usr/bin/python3
import time
print(time.asctime())
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220408-1649408434003)

- 保存并退出
- 在shell里运行
	- `python3 sleep.py`
- 在shell里面输出重定向
	- `python3 sleep.py | figlet`
- 输出是可以的
- 但是不会刷新
- 而且太大了
- 超过一行了

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220211-1644546361651)

- 不过至少可以出现一次时间了
- figlet 有别的字体么？

### figlet 字体列表

- f 控制字体
- r、c、l 控制左中右

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220211-1644546423440)

## 总结

- 用`\r`可以让输出位置回到最开头的地方
  - 重新输出时间
  - 我们可以让时间在固定位置刷新了
- 我想要的是大字符
  - 应该是 figlet
  - 但是希望同时还能刷新
- 可能吗？🤔
- 我们下次再说！👋

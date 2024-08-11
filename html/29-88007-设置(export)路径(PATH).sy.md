---
show: step
version: 1.0
enable_checker: true
---

# 放入路径

## 回忆上次内容

- 想要在任意路径下直接执行 `sleep.py`
  - 可以把 `sleep.py` 放入 `/usr/bin/` 下面
- 但是`/usr/bin`里面放的都是二进制文件
- 我想把 `sleep.py` 放在 `shiyanlou` 的宿主目录里面
- 然后把我的目录添加到系统变量 `$PATH` 中

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220930-1664549610079)

- 这样有可能吗？🤔
- 先回忆为什么无论ls在哪里都能执行

### 路径

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220324-1648105545833)

- ls所在的/usr/bin
	- 是在系统变量$PATH中的

### 修改 PATH

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210923-1632365852073)

```shell
#查看当前$PATH
echo $PATH
#设置$PATH，注意不要加空格
export PATH=~:$PATH
#查看更新后的$PATH
echo $PATH
```

- export PATH=~:$PATH
  - ~是当前用户 shiyanlou 的用户文件夹
  - 也就是/home/shiyanlou
  - :是分隔符号
  - 前面的 PATH 不需要$

### 具体效果

- 注意！！！
	- `PATH`必须大写
		- `$PATH`和`$path`是两回事
	- 输入的时候千万注意不能使用中文标点！！！
		- 包括<kbd>:</kbd><kbd>~</kbd><kbd>.</kbd>都必须是英文半角

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220324-1648116848920)

- 修改后主要是
	- 在老$PATH(黄色)之后
	- 增加了~(红色)
	  - 当前用户文件夹(~)
	  - 也就是shiyanlou的用户文件夹
	  - /home/shiyanlou 
  - 结果的新$PATH
	- 就在蓝色方框内
- /home/shiyanlou 下有 sleep.py
	- 能运行么

### 尝试运行

- 如果是新建的sleep.py需要修改权限

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220215-1644931164246)

- 虽然不能运行
- 但是是可以找到
- 只是权限不够
- 还是需要给当前用户执行权限

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220324-1648118284745)

- sudo chmod u+x sleep.py
	- sleep.py的owner是shiyanlou
	- 就是当前用户
- 然后在尝试运行python.py

### 成功运行

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210221-1613896287421)

- sleep.py确实直接运行了！
	- 换个路径也可以么？🤔

### 换个路径

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220324-1648118572438)

- 在当前路径(~/Code)运行`sleep.py`
  - 运行 `sleep.py第1行` 声明的解释器 `/usr/bin/python3`
  - 把 `/usr/bin/python3`从硬盘调用到内存
  - 成为一个进程
- 在内存中运行的python3
  - 解释执行 `sleep.py`
  - 每隔 1s 输出一次时间
  - <kbd>ctrl</kbd>+<kbd>c</kbd>结束进程
- 但是重新打开 `xfce终端` 
	- 这个新$PATH就失效了
	- 这可怎么办呢？

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220930-1664550005122)

### 重启终端过程

- 重启中断后
	- 登录shell
- $PATH 就回到了最初
	- 不包含/home/shiyanlou了
	- 找不到 sleep.py 了
- 我想每次新打开 `terminal` 就自动把 `$PATH` 设置好
	- 应该怎么办？


### 终端初始化

- 研究一下终端的初始化过程

- 当我们运行某个shell文件的时候	
	- 首先会运行shell的rc文件
	- rc也就是runcom配置文件
- shiyanlou的默认shell是zsh
	- 对应的rc文件就是~/.zshrc
	- 试着编辑他
	- vi ~/.zshrc
		- <kbd>G</kbd>到最后一行
		- <kbd>o</kbd> 在下方插入一个新行并进入编辑模式
		- 试着加一行输出

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220315-1647346246251)

- 然后重新打开一个xfce终端

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220310-1646914501998)

- 如果默认的shell不是zsh
- 而是bash
- 会如何呢？

### ~/.bashrc

- zsh对应的rc文件是~/.zshrc
- bash对应的 rc文件是~/.bashrc
	- 试着编辑他
	- vi ~/.bashrc
		- <kbd>G</kbd>到最后一行
		- <kbd>o</kbd> 在下方插入一个新行并进入编辑模式
		- 试着再加一行输出

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220313-1647175420184)

- 切换shell的时候会有相应的提示

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220310-1646914662083)

- 既然如此
- 我们可以把export PATH=$PATH:~这句话 
	- 放在默认的shell(zsh)的配置文件(~/.zshrc)中
- 这样新每次运行zsh终端的时候
	- 就自动完成路径配置
	- 把~加入到$PATH的路径列表中

### ~/.zshrc

```bash
# 编辑zsh的配置文件rc(run command)
vi ~/.zshrc
```

- 编辑这个配置文件
	- 在尾行下面加一句话
	- `export PATH=$PATH:~`
	- 可能不一定是124行
	- 只要是最后一行就行

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220313-1647175309737)

- 以后只要是进 zsh
	- $PATH 列表中就会包含用户文件夹~
- 可是
	- 这个 `~/.zshrc` 到底是啥意思

### 理解rc文件

- ~/.zshrc
  - ~ 指的是当前用户的用户文件夹
    - 此配置只对当前用户(shiyanlou)有效
  - 首字母 `.` 说明这是个隐藏文件
    - ls 看不见
    - ls -a 才能看见

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220318-1647611406002)

- zsh
	- 指定的 shell 是 zsh
    - 而不是 bash
    - bash 就得用 ~/.bashrc
- 这个rc是什么意思呢？

### rc
- rc 指的是 `run commands` 的缩写
    - 运行程序
    - 很多东西在配置 shell 的时候不用重复手动运行
    - 写到 rc 里面
    - 启动 shell 或者软件的时候就可以批量处理了
      - ~/.zshrc
      - ~/.vimrc
      - ~/.bashrc

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210812-1628740962094)

- 但是这个我还得重启一下zsh才能应用
	- 我就在当前的zsh下不重启
- 就把$PATH设置了可以么？

### 运行当前zsh的rc

- 运行~/.zshrc配置文件
	- source ~/.zshrc
	- 这就是手动执行执行~/.zshrc
- 或者直接运行zsh也可以

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220318-1647611729922)

- 执行之后
	- 路径就设置好了


### 总结

- 这次修改了 `$PATH`路径
    - 把当前用户文件夹 `~` 添加到 `$PATH`
    - 这样 `sleep.py` 就可以被找到
    - 于是就可以被执行了
- 还可以把配置`$PATH`的脚本
   - 放到`zsh`的配置文件(`~/.zshrc`)中
   - 配置 `~/.zshrc` 就可以配置 `zsh` 环境的 `$PATH`
- 在当前路径运行 sleep.py
  - 在 `python` 程序第 1 行声明打开方式为 python3
  - 把 `/usr/bin/python3` 从硬盘调用到内存
  - 成为一个进程不断输出时间
  - <kbd>ctrl</kbd>+<kbd>c</kbd>结束进程
- 我想看到 `python3` 这个进程
	- 可能吗？🤔
- 下次再说👋🏻
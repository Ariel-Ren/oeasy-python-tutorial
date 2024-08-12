---
show: step
version: 1.0
enable_checker: true
---

# 导入 request 包

## 新的开始

- 现在就要深入学习 python 爬虫了
	- 我们从哪里开始呢？
	- 首先访问一下本地主机

```
firefox http://localhost
```

- 连接失败
- 本地没有开启web服务

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231214-1702559995198)

- <kbd>ctrl<kbd> + <kbd>c<kbd>
	- 终止火狐

### nginx

- 要开启静态网页服务器
	- nginx
    - ngin 的意思是 engine x

```
sudo service nginx start
sudo service nginx status
```

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221118-1668769671876)

- 服务启动完成之后

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220912-1662949090031)

- 试着用浏览器访问 localhost

### 访问网页

```
firefox http://localhost
```

- 在地址栏里的是http://localhost
	- 注意是http
	- 而不是http`s`
		- 没有`s`

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20220912-1662949192013)

- 能访问自定义的网页么？

### 编辑网页

- 首先在用户宿主文件夹
	- 建立一个网页

```
vi oeasy.html
```

- 网页文件如下

```html
<!DOCTYPE html>
<html lang="zh-cn">
	<head>
		<title>menu</title>
		<meta charset="utf-8">
	</head>
	<body width="700px">
		<h1>menu</h1>
		<ul id="ulist">
			<li>
				<span class="food">豆汁</span>
				<price>10</price>
			</li>
			<li>
				<span class="food">羊瘪汤</span>
				<price>15</price>
			</li>
			<li>
				<span class="food">折耳根</span>
				<price>20</price>
			</li>
		</ul>
	</body>
</html>
```

### 保存网页

- 复制后粘贴

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231214-1702560722970)

- 然后保存并退出

### 网页的根目录

- 网页服务器根目录在哪呢？
    - `whereis nginx`
	- /usr/share/nginx/html/

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231015-1697365749304)


- sudo cp ./oeasy.html /usr/share/nginx/html
	- sudo 用管理员权限运行
	- cp 拷贝
	- 把food.html
	- 网站服务器根目录下


```
sudo cp ./oeasy.html /usr/share/nginx/html
```

### 浏览过程

```
firefox http://localhost/oeasy.html
```

- 浏览网页

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231215-1702609500691)

### 检查元素

- F12 检查元素
	- 选择网络 Networks

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231015-1697366142481)

- 如果<kbd>F12</kbd>没有用的话
	- 在键盘最下面一行找到<kbd>Fn</kbd>键
	- <kbd>Fn</kbd>+<kbd>F12</kbd>
- 实在不行右键
	- 检查元素也可以找到
- 然后刷新

### 刷新

- F5 也可以刷新
	- 刷新后会看到网络中的的
		- 请求 requests
		- 响应 response

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231015-1697366198856)

- 选中 oeasy.html 文件
	- 这个文件就是nginx  
		- 响应http的请求 得到的
- 请求就是 
	- request
- 响应就是 
	- response

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210831-1630412050376)

### 请求 request

- 首先从浏览器
	- 发出一个`http get`请求(request)
  - http
    - 超文本传输协议
		- hyper-text transmit protocol
    - 是网络传输中使用的协议
  - get
    - 是得到相应文件的方法
    - 除了get之外还有post等

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210831-1630406366911)

- 这是从火狐浏览器
	- 发往服务器的 请求
- 请求头里面 
	- 都包括一些什么呢？

### 请求头 request head

- 火狐浏览器会自动加上一些请求头
  - Accept-Language
    - 接受的语言
  - Host
    - 被请求的主机
  - User-Agent
    - 发请求的浏览器
- nginx 服务器接收到了请求之后
	- 就会进行处理
	- 就像跑堂的 会处理客人要求一样
	- 把客人需求 提给后台服务器
- 后台服务器根据客人要求得到一个回应页
	- nginx 就把这个 `回应页` 作为 `请求Request `的 `响应Response`
    - 然后这个回应页就返回到浏览器了

### 响应 Response

- 服务器根据接收到的东西处理
	- 将结果作为响应发回给浏览器

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210831-1630406600963)

- 浏览器会接到响应头
  - Content—Type
    - 接收文件类型
    	- html就在浏览器中渲染
    	- zip就直接下载
  - Content—Length
    - 内容字节长度
  - Date
    - 接收时间
  - Server
    - 服务器

### 完成

- 这个过程完成了
  - 整个 http get 会得到一个状态码(Status_Code)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20231015-1697366395464)

- Get 请求得到了响应
  - 状态码是 304
  - 意思是 Not Modified
- 什么是状态码呢？

## 总结

- 我们安装并启动了 
	- nginx 服务器
- 使用浏览器访问了服务器上的网页
	- 浏览器发送了请求
		- request
	- 服务器回应了响应
		- response
- 最终状态码
  - 304

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20210831-1630412050376)

- 什么是状态码呢？
- 还有其他状态码吗？🤣
- 下次再说👋

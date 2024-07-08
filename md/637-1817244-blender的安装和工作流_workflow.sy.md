---
show: step
version: 1.0 
enable_checker: true
---


# python_音频处理_midi制作

## 开始

- 我们首先要从零开始
- 安装3d软件

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240527-1716775021875)

- 装哪个呢?

### 选型

- 3dmax、maya先后争霸
- blender后来居上

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240527-1716775040740)

- 只有 blender是开源的
- 只能选blender

### 安装

```
sudo apt update
yes | sudo apt install blender

```

- 安装成功后
	- 可以在开始菜单找到
	- 图形 - Blender

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240108-1704718729508)

- 也可以在shell中
	- 直接运行

```
blender
```

- 在开机画面旁边 点一下
	- 进入界面

### 尝试控制3D视图面板

- 尝试控制默认镜头位置

|键鼠配合 | 操作| 效果 |
| --- |--- |---|
|<kbd>鼠标中键</kbd>| 滚动  | 镜头推拉 |
| <kbd> 鼠标中键</kbd>  |按住拖动 | 镜头旋转 |
| shift + <kbd> 鼠标中键</kbd> | 点击拖动 | 镜头平移 |


![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240108-1704721017891)

- 尝试控制默认摄像机

### 上下文菜单

- 右手 用鼠标 
	- 选中立方体
	- 选中后 会有橙色外轮廓
- 左手小拇指 先按下<kbd>shift</kbd>不松手 
	- 左手大拇指 再按下 <kbd>空格</kbd>
	- 同时放开 两个按键
	- 调出上下文菜单

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240108-1704720379817)

- 左手食指 按一下<kbd>g</kbd>
	- 出现 坐标轴 
- 键盘操作都由左手完成
- 如果不行的话
	- 就用鼠标点击侧面的移动工具

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240527-1716775290308)


### 调整坐标

- 坐标轴出现后
	- 鼠标放在 红色的坐标轴上 
	- 红色高亮之后 按下 右键
	- 立方体 外轮廓从 橙色 变成 白色
	- 出现 拖动光标 
	- 可以让立方体沿着 红色轴移动

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716354422213)

- 与此同时	
	- 属性调板中的Location.X变化

- 三个移动轴
	- 分别代表什么呢？

### 观察Tranform

- 在左上角面板中选中 立方体
	- 观察Tranform中
	- Location的变化
- 也可以 把鼠标放到数值上
	- 鼠标变化后 按下 鼠标
	- 上下移动 
	- 修改数值

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240229-1709169884300)

- 三个坐标轴
	- <span style="color:red">红</span><span style="color:green">绿</span><span style="color:blue">蓝</span> 三个颜色
	- 对应着 <span style="color:red">x</span><span style="color:green">y</span><span style="color:blue">z</span> 三个坐标轴

- 可以旋转立方体吗？

### 修改旋转


- 右手 用鼠标 
	- 选中立方体
	- 选中后 会有橙色外轮廓
- 左手小拇指 先按下<kbd>shift</kbd>不松手 
	- 左手 再按下 <kbd>空格</kbd>
	- 同时放开 两个按键
	- 调出上下文菜单
- 左手食指 按一下<kbd>r</kbd>
	- 出现 旋转轴 
- 鼠标放到 旋转轴上
	- 颜色高亮 后 
	- 可以旋转 
- 还是三种颜色 
	- 沿着 <span style="color:red">红</span><span style="color:green">绿</span><span style="color:blue">蓝</span> 三个坐标轴移动
	- 分别对应着 <span style="color:red">x</span><span style="color:green">y</span><span style="color:blue">z</span> 三个旋转轴


![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240129-1706526185664)

- 观察 Rotation 数值 
	- 确实变化了
- Scale可以修改吗？

### 修改Scale

- 右手 用鼠标 
	- 选中立方体
	- 选中后 会有橙色外轮廓
- 左手小拇指 先按下<kbd>shift</kbd>不松手 
	- 左手 再按下 <kbd>空格</kbd>
	- 同时放开 两个按键
	- 调出上下文菜单
- 左手食指 按一下<kbd>s</kbd>
	- 出现 旋转轴 
- 鼠标放到 旋转轴上
	- 颜色高亮 后 
	- 可以旋转 

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240129-1706526570671)

- 还是三种颜色 
	- 沿着 <span style="color:red">红</span><span style="color:green">绿</span><span style="color:blue">蓝</span> 三个坐标轴移动
	- 分别对应着 <span style="color:red">x</span><span style="color:green">y</span><span style="color:blue">z</span> 三个旋转轴
- 可以发现 右侧属性的 变化
- 目前 顶行 中部显示
	- 当前 处于布局(layout) 工作区(workspace)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240229-1709170696755)

- 可以 切换工作区 吗？

### blender

- 缩小左侧提示区宽度

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716355006846)

- 鼠标右键 选择
	- 脚本 Script 
	- 工作区 (Work Space)

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240108-1704718975933)

- 鼠标中键按下
	- 左右移动
	- 可以选择工作区

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240527-1716775396524)

- 选择
	- Script脚本
	- 工作区workspace

### 布局

- 如下

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240108-1704719043726)

### 移动边框

- 控制布局大小
	- 每个调板都可以调整大小

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240108-1704720180146)

- 控制台面板
	- 就是我们的 游乐场

### 观察脚本执行

- 在游乐场
	- 使用python

```
1 + 1
import bpy
bpy.data.version

```

- 查看版本信息

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240518-1716037232222)

### 执行python代码

- 将场景中的 Cube对象
	- 拖入 游乐场

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716355322837)

- 在 游乐场 得到
	- bpy.data.objects["Cube"]

```
bpy.data.objects["Cube"].
```

- 按下<kbd>.</kbd>
	- 按下<kbd>Tab</kbd>

### 提示效果

- 游乐场出现的对象为
	- Cube

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716381818979)

- Cube 基础的属性有
	- location
	- rotation_euler
	- scale

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716381999790)

- location是一个
	- 三维向量
	- 3d-vection

### 尝试访问

- 按方向键<kbd>⬆️ </kbd>
	- 尝试访问 向量的第0个分量

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716382314037)

- 继续按方向键<kbd>⬆️ </kbd>
	- 尝试设置 向量的第0个分量

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716382360773)

### 自增

```
bpy.data.objects["Cube"].location[0] += 1
```

- 每次执行
	- 立方体的location.x都会+1

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716382440550)

### 设置其他位置分量

```
bpy.data.objects["Cube"].location[1] += 3
bpy.data.objects["Cube"].location[2] += -2
```

- 尝试改变y、z

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716382597811)

- 观察属性调板

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240522-1716382583517)

### 尝试改变旋转

```
bpy.data.objects["Cube"].rotation[0] += 0.3
```

- Cube对象 没有rotation这个属性

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240523-1716433579180)

- 可以看到具体的属性名吗?

### 效果

- 点击
	- Edit - Preference
	- 编辑 - 设置

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240523-1716434097802)

- 勾选python提示

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240523-1716434190353)

### 效果

- 选中Cube
	- 找到属性调板

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240523-1716433987691)

- 可以看到 属性 
	- 对应的python代码

```
bpy.data.objects["Cube"].rotation_euler[2] 
```

- 后面加了_euler

### 尝试改变旋转

```
bpy.data.objects["Cube"].rotation_euler[0] += 0.3
bpy.data.objects["Cube"].rotation_euler[1] -= 0.3
bpy.data.objects["Cube"].rotation_euler[2] = 1.57
```

- 尝试修改物体的旋转属性

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240523-1716427369615)

- 属性调板中的旋转值
	- 是基于弧度制的

- 最后尝试 修改 缩放值

### 缩放

```
bpy.data.objects["Cube"].scale[0] = 1
bpy.data.objects["Cube"].scale[1] = 2
bpy.data.objects["Cube"].scale[2] = 3
```

- 直接设置 scale属性

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240523-1716427662996)


### 总结

- 这次从零开始
	- 安装了blender软件
	- 并且了解了界面
- 在界面上对物体进行了操作
	- 移动
	- 旋转
	- 缩放

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20240523-1716427822360)

- 还有什么可以玩的呢？🤔
- 我们下次再说！👋

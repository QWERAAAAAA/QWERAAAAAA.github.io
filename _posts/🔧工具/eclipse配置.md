## 确认是否安装了Java开发环境-JDK

打开iTerm或者mac自带的终端，输入 java -version

如果是下面这样返回了版本号就是已经安装过了

否则就先移步到我上一个博客安装并配置一下JDK

## 下载eclipse

进入官网 https://www.eclipse.org/downloads/
网站会自动检测你的设备并给出下载包，点左面这个下载


会进入一个新的界面，点击Download就行

## 安装eclipse

双击上步中下载的eclipse-inst-mac64.dmg文件
将图标拖进程序坞，并双击图标打开他
先看右上角有没有黄色感叹号，有的话千万千万要点进去更新一下
这里列出了多种下载安装包，根据需求来选择。例如我选择的Eclipse IDE for Java Developers

<img src="https://img-blog.csdnimg.cn/36e51e082a954970aa21e833eb4fcc16.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2hlbHMu,size_20,color_FFFFFF,t_70,g_se,x_16" alt="在这里插入图片描述" style="zoom: 33%;" />

修改第一个选项为2020-06年或者早于2020-06的版本
再点下面的那个文件夹形状的按钮，选择JDK所在的位置
（ 这步非常重要

点击INSTALL下载，下载完了以后是不会提示你将它放进程序坞的，所以你需要手动将它放进去，根据安装路径/Users/mac/eclipse/java-2020-06找到它的图标，将它拖到程序坞

## 为eclipse配置JDK

点击下面的这个偏好设置

点击下面的Add添加

点击Standard VM后点Next>

点击Directory

按照下面的红框的顺序找到自己JDK的Home的路径

点击Apply and Close

就配置成功了！！！

## 创建一个Java项目

**点击“Creat a new Java project”**


输入“Project name”，例如“softTest1”；JRE选择第三项“use default JRE（currently “Home”）”，也就是上述为eclipse配置的默认JRE；其他默认即可；最后点击“finish”创建project

随后的弹框直接点击“Create”即可

<img src="https://img-blog.csdnimg.cn/20200307132259320.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N6d195eA==,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述" style="zoom:33%;" />



**创建包：**

右键项目名softTest1->new->Package

<img src="https://img-blog.csdnimg.cn/20200307132332214.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N6d195eA==,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述" style="zoom:33%;" />

弹框中的包名默认或者修改都可



**创建class：**

右键新建的包名softTest1->new->class

<img src="https://img-blog.csdnimg.cn/20200307132352584.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N6d195eA==,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述" style="zoom:33%;" />

弹框中的“Name”可命名为“HelloWorld”，其他默认即可，点击“finish”。

写入代码、点击运行，即可在控制台中看到输出

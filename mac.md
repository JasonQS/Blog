# 当我换上了 Mac

### 快捷键

说几个我常用的，其他可以自己查

⌘ Q 关闭整个程序

⌘ W 关闭当前窗口

⌘ ⌃ F 全屏

⌘ H 隐藏当前窗口

⌘ ⇧ H 隐藏其他窗口

⌘ M 最小化窗口 ( 一般只用⌘ H )

⌘ ⇥ 切换窗口 (tab切换，↓↑←→)

⌘ N 新建窗口

⌘ T 新建

⌘ ⇧ T 恢复刚刚关闭的

⌘ R 刷新

⌘ ⇧ R 不带缓存的刷新

⌘ A 全选

⌘ S 保存

⌘ F 查找

⌘ Z 撤销

⌘ ⇧ Z 重做

fn ⌫ 往右删除

⌘ ⌫ 扔进废纸篓

⌥ ⌘ ⌫ 直接删除

⌘ ⇧ 3 截取全屏

⌘ ⇧ 4 自定义截取

⌘ ⇧ 4 ␣ 快速截取窗口

⌃ ⌘ ␣ 插入表情符号

### 给终端设置快捷键

Mac 本来没有设置打开Terminal的快捷键

需要在 Automator 里新建一个服务，然后绑定快捷键，这里不展开


### 输入法

系统输入法不能动态调频，于是装上搜狗并禁用默认的输入法

打开HIToolbox.plist，该文件需要安装xcode才能打开

`$ sudo open ~/Library/Preferences/com.apple.HIToolbox.plist`

在 *AppleEnabledInputSources* 找到要删除的输入法，删除整个以数字命名的文件就好了

 - - - - -

### JetBrains系列编辑器破解

[ilanyu](http://blog.lanyus.com/) 破解了他们家的编辑器

我们使用的方法有三种：

在(http://idea.lanyus.com/)获取注册码然后写到 Activation Code 里

在License Server里直接输入 `http://idea.iteblog.com/key.php`

在windows下用了一年多的我表示，每次启动的时候显示的是 `Licensed to ilanyu`
稍微有点不舒服，于是参考[License Server 搭建教程](http://blog.lanyus.com/archives/174.html)
，捐了20块抚慰良心

于是现在启动的时候显示的是 `Licensed to Jason` 了

该方法可以在本地搭建License Server，也可以把它部署到服务器上

### Microsoft Office for Mac 破解

[office 下载地址](http://officecdn.microsoft.com/pr/C1297A47-86C4-4C1F-97FA-950631F94777/OfficeMac/Microsoft_Office_2016_Installer.pkg)

破解工具：网上找 `FWMSO2016VL`

参考 [简单教程](http://www.jianshu.com/p/2172835cfb17)

### Adobe 破解

官网下载 [Creative Cloud](https://creative.adobe.com/zh-cn/products/download/creative-cloud)

注册账号然后在本地下载任何你想要的

破解工具：网上找 `adobe-zii-cc17`

### Yummy FTP Pro 破解

网上找找很多，这里放一个
[简答教程](http://www.web3.xin/soft/198.html)

发现了个博客，里面放了很多Mac破解软件 [web3.xin](http://www.web3.xin/soft)
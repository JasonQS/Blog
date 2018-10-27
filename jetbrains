[ilanyu](http://blog.lanyus.com/)做了一套jetbrains的[注册机](http://blog.lanyus.com/archives/326.html)

能以License Server的形式注册

用法是 ./licenseServer  -l 127.0.0.1 -p \[端口号\] -u \[注册名\]

#### 偷个小懒

以前我给这段命令加了个alias

`alias lic='/Users/jason/.licenseServer  -l 127.0.0.1 -p 1222 -u Jason'`

这样只要在需要用IDEA时terminal里输入 lic 即可注册

#### 更方便一些

后来觉得这样太麻烦, 就写了个sh脚本开机自动运行

`/Users/jason/.licenseServer  -l 127.0.0.1 -p 1222 -u Jason &`

& 表示后台运行

发现开机后 terminal会残留显示\[process completed\] 却不关闭

可以在Terminal的设置里 - shell - When the shell exits

把原来的 Don't close the window 改成 Close if the shell exits cleanly

#### 让别人也能用

在云服务器 /etc/rc.local 里加上

`/Users/jason/.licenseServer  -l 0.0.0.0 -p 1222 -u Jason &`

意思是开机时运行这条命令

这样就能让小白也能用上jetbrains注册机了

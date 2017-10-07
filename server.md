## 当我拿到一台服务器

###### Ubuntu 16.04   Mac   Yummy Ftp Pro

------------------

### 新建用户 *jason*

`$ adduser jason`  #新建用户 *jason*

`$ usermod -G sudo jason` #把*jason*加入到*sudo*组里

和useradd不同，adduser会帮你建好主目录,设置密码等

`$ deluser` #删除用户

*/etc/passwd* #用户信息

*/etc/group* #组信息

-----------------

### 优化ssh链接

1. Mac 终端防超时掉线

    每隔60秒给服务器发送一个心跳包
    在 *~/.ssh/config* 里加上

        ServerAliveInterval 60

2. 免密登录

    首先 `$ ssh-keygen -t rsa` 在当前目录下生成密钥对
    它会叫你取个名字，我做了两把， *ali_jason_rsa* 和 *ali_root_rsa*

    把public key放到服务器- `~/.ssh/authorized_keys` 文件中，如果没有就新建，
    不过注意：

    *该文件除自己以外不能有可写权限，所以 `$ chmod 600 authorized_keys`*

    再把private key放在自己的电脑上的 *~/.ssh* 里

    然后在 *~/.ssh/config* 里写入

        Host ali
            HostName 106.15.***.***
            User root
            IdentityFile /Users/jason/.ssh/ali_root_rsa

        Host j
            HostName 106.15.***.***
            User jason
            IdentityFile /Users/jason/.ssh/ali_jason_rsa

    配置完后，只需输入 `ssh ali` 或者 `ssh j` 就能连上服务器了

3. 服务器禁止密码登录 (可选)

    在 */etc/ssh/sshd_config* 里加上

        PasswordAuthentication no

        AllowUsers deploy@(your-ip) deploy@(another-ip-if-any) # 添加允许登录IP

    重启服务 `systemctl restart sshd.service`

--------------------

### 安装 Nginx 和 Tomcat

为了方便配置管理，我使用编译的方式安装这两个服务器

当然你也可以直接 `$ apt install nginx`

##### 安装依赖

一共需要装 zlib pcre ssl

`$ sudo apt update`

`$ sudo apt-get install zliblg-dev`

`$ sudo apt-get install libpcre3 libpcre3-dev `

##### 安装Nginx

`$ wget http://nginx.org/download/nginx-1.13.5.tar.gz`

`$ tar -xf nginx-1.13.5.tar.gz`

`$ cd nginx`

`$ ./configure`
<br>
`--prefix=/home/jason/qsboy/nginx` #生成的位置
<br>
`--with-http_ssl_module` #配上ssl

`$ make && make install`

##### 配置Nginx

为了编辑方便，我给 *nginx/conf/nginx.conf* 和 *nginx/sbin/nginx*做了个软连接到 *nginx* 下

`$ cd ~/qsboy`

`$ ln -s nginx/conf/nginx.conf nginx.conf`

`$ ln -s nginx/sbin/nginx nginx`

详细配置这边也说不完，就不写了

##### 安装Tomcat

Tomcat安装比较简单，解压了就能用

    这边注意Java和Tomcat的版本
    像我一开始装的 jdk9 和 Tomcat8.5 就报错了
    于是把 jdk9 换成jdk8
    或者装 Tomcat9

`$ apt install openjdk-8-jdk`

配置Java环境变量

可以修改/etc/profile #系统环境变量

    JAVA_HOME="/usr/lib/jvm/openjdk/"

也可以修改/etc/environment #用户环境变量

    export JAVA_HOME="/usr/lib/jvm/openjdk/"


#### 换上https

使用 [Let's Encrypt](https://letsencrypt.org/)

可以使用 [certbot](https://certbot.eff.org/) 工具快速换上https

不需要手动生成密钥对，根据帮助直接配好

`$ sudo certbot renew --dry-run` #自动更新

不过我遇到的一个问题是certbot找不到我的nginx，所以

`$ sudo certbot --nginx`
<br>
`--nginx-server-root /home/jason/qsboy/nginx/conf/ `
<br>
`--nginx-ctl /home/jason/qsboy/nginx/sbin/nginx`


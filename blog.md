## 当我拿到一台服务器

###### Ubuntu 16.04

------------------

#### 新建用户 *jason*

`$ adduser`

> 和useradd不同，adduser会帮你建好主目录,设置密码等

> `$ deluser` 删除用户

> `$ usermod -G sudo jason` 把jason加入到sudo组里

> */etc/passwd* 用户信息

> */etc/group* 组信息

#### 优化ssh链接

1. Mac 终端防超时掉线

    每隔60秒给服务器发送一个心跳包
    在 *~/.ssh/config* 里加上

    >ServerAliveInterval 60

2. 免密登录

    配置完后，只需输入`ssh j`就能连上ssh：

    首先 `$ ssh-keygen -t rsa` 在当前目录下生成密钥对
    它会叫你取个名字，我做了两把， *ali_jason_rsa* 和 *ali_root_rsa*

    把public key放到服务器- `~/.ssh/authorized_keys` 文件中，如果没有就新建，
    不过注意：*该文件除自己以外不能有可写权限，所以 `$ chmod 600 authorized_keys`*

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

3. 服务器禁止密码登录 (可选)

    在 */etc/ssh/sshd_config* 里加上

        PasswordAuthentication no

        AllowUsers deploy@(your-ip) deploy@(another-ip-if-any) # 添加允许登录IP

    重启服务 `systemctl restart sshd.service`
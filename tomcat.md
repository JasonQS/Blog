## Tomcat 遇到的一个坑

### 找不到servlet的路径

在配置虚拟主机时，<Host>标签下有个<Context>标签

大致长这样：

    <Host name="demo.localhost" appBase="/Users/jason/project/Web/qsboy/web/demo/out/artifacts/">

        <Context path="" docBase="demo_war_exploded"

    </Host>

上面是正确的写法，下面是坑位所在：

    <Host name="demo.localhost" appBase="/Users/jason/project/Web/qsboy/web/demo/out/artifacts/demo_war_exploded">

        <Context path="" docBase=""

    </Host>

哪里坑了呢，第二种写法，一般的网页都能找到都能打开，*唯独在server>.xml里配置的那些路径就是找不到*

docBase的值也不能为

    ""
    "."
    "/"
    "./"

但编译时不会告诉你这里不对，一定要连滚带爬才能出来
## 配置yum源

##### 一、配置本地yum源

1.使用CentOS光盘作为本地yum源

2.实体机：直接放入光盘

3.VM虚拟机：虚拟机-可移动设备-CD/DVD-连接

4.前期准备：        

```
   mkdir  /mnt/cdrom                 #创建用于挂载光盘的目
   mount  /dev/cdrom /mnt/cdrom      #挂载
   umount /mnt/cdrom                 #卸载
   cp-avf /mnt/cdrom   /yum          #若不想每次都放光盘，可复制光盘文件到本地硬盘yum目录下
```

5.创建repo文件：               

```
    cat>>/etc/yum.repos.d/CentOS-Local.repo<<-EOF           
```

```
       [Local
       name=LocalYum
       baseurl=file:///yum
       gpgcheck=1
       gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
       EOF
```

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml816\wps12.jpg) 

 6.cat>>EOF与cat>>-EOF的区别：

​        (1).如果重定向的操作符是<<-，那么分界符(EOF)所在行的开头部分的制表符（Tab）都将被去除

​        (2)可以解决由于脚本中的自然缩进产生的制表符

​        (3)在使用cat<<EOF时，输入完成后，需要在一个新的一行输入EOF结束stdin的输入。EOF必须顶行写，前面不能用制表符或空格键

7.更新yum缓存：            

```
    yum  clean  all        #清除缓存
    yum  makecache        #生成缓存
    yum  list           #显示所有已经安装和可以安装的程序包
```

​          

##### 二、配置网络yum源

​         1.备份原始yum源：                  

```
 cd   /etc/yum.repos.d
 mv  CentOS-Base.rpeo   CentOS-Base.repo.bak 
```

​         2.配置CentOS的DNS：               

```
    vim   /etc/resolv.conf
    nameserver   114.114.114.114               //国内dns
    nameserver   8.8.8.8                        //国外dns
```

  3.下载yum文件，替代原始yum源：

​    (1)网易yum源：      

```
wget -O  /etc/yum.repos.d/CentOS-Base.repo  http://mirrors.163.com/.help/CentOS7-Base-163.repo
yum   clean   all            //清除缓存
yum   makecache       //生成缓存
```

​       解析:wget -o,使用“-o”参数来指定一个文件名

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml816\wps13.jpg) 

 

  (2)阿里云yum源：        

```
 wget   -O   /etc/yum.repos.d/CentOS-Base.repo    http://mirrors.aliyun.com/repo/Centos-7.repo
 yum   clean  all
```

 4、更新cache缓存

```
# yum makecache 
```

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml816\wps14.jpg) 

5、查看

```
yum -y update 
```

 

**三、配置ELEP源：**                 

```
  yum  -y   install   epel-release
  yum   clean  all
  yum   makecache
```

 

**补充说明****关于repo 文件的格式**

所有repository 服务器设置都应该遵循如下格式：

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml816\wps15.jpg) 

· serverid 是用于区别各个不同的repository，必须有一个独一无二的名称；

· name 是对repository 的描述，支持像$releasever $basearch这样的变量；

· baseurl 是服务器设置中最重要的部分，只有设置正确，才能从上面获取软件。它的格式是：

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml816\wps16.jpg) 

其中url 支持的协议有 http:// ftp:// file:// 三种。baseurl 后可以跟多个url，你可以自己改为速度比较快的镜像站，但baseurl 只能有一个，也就是说不能像如下格式：

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml816\wps17.jpg) 

其中url 指向的目录必须是这个repository header 目录的上一级，它也支持$releasever $basearch 这样的变量。
url 之后可以加上多个选项，如gpgcheck、exclude、failovermethod 等

其中gpgcheck，exclude 的含义和[main] 部分相同，但只对此服务器起作用，failovermethode 有两个选项roundrobin 和priority，意思分别是有多个url可供选择时，yum 选择的次序，roundrobin 是随机选择，如果连接失败则使用下一个，依次循环，priority 则根据url 的次序从第一个开始。如果不指明，默认是roundrobin。

 

 
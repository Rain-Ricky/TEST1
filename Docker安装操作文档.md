## Docker安装操作文档

#### **一、安装准备**

系统要求：在CentOS下需要64位的CentsOS 7



#### **二、docker安装**

###### 1、检查内核版本

```
$ uname -r
```

![1554890663286](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554890663286.png)

###### 2、删除非官方的Docker Package

​    有些版本的Linux系统中自带有Docker，例如Red Hat。使用docker代替 docker-engine,如果想使用官方版本需要执行删除语句。

```
$ sudo yum -y remove docker docker-common container-selinux
```

[^sudo]: sudo命令可以让你以root身份执行命令，来完成一些我们这个帐号完成不了的任务。　其实并非所有用户都能够执行sudo，因为有权限的用户都在/etc/sudoers中呢。我们可以通过编辑器来打开/etc/sudoers，或者直接使用命令visudo来搞定这件事情。   

```
$ sudo vim /etc/sutoers
```

​       给用户添加root权限

```
  User Privilege specification
  root ALL=(ALL:ALL)  ALL
  ***  ALL=(ALL:ALL)  ALL      # 其中***为需要的添加root权限的用户
```



###### 3、升级本地yum包

```
$ sudo yum update
```

![1554891440704](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891440704.png)

![1554891445051](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891445051.png)

![1554891459783](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891459783.png)



###### 4、安装依赖包

```
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

![1554891498835](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891498835.png)



###### 5、设置稳定版的仓库

```
$ sudo  yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

![1554891547022](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891547022.png)

**注意：不要使用不稳定的版本仓库在生产环境或非测试环境中。如果同时拥有稳定的仓库和非稳定的仓库，在使用 yum install或者yum update 在没有指定特定版本的前提下进行安装或升级操作，需要注意大多数情况下获取的是最高的版本，并且极有可能是不稳定的版本。**



###### 6、更新 yum 缓存

```
$ sudo yum makecache fast
```

![1554891581619](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891581619.png)



###### 7、docker安装

（1）安装最新版本docker

​    docker分为社区版docker-ce（免费）和社区版docker-ee（收费），以下以社区版为例进行安装演示：

```
 $ sudo yum install docker-ce
```

![1554891770026](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891770026.png)

![1554891776940](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891776940.png)

（2）安装指定版本

​      首先查看仓库中所有docker版本，再选则版本安装

```
 $ sudo yum list docker-ce --showduplicates | sort -r
 $ sudo yum install docker-ce-18.03.0.ce
```

![1554891833265](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891833265.png)

（3）通过脚本快速安装

```
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
```

（4）使用rpm包安装

​     进入http://download.docker.com/linux/centos/7/x86_64/stable/Packages/页面，下载安装docker的rpm文件；然后执行如下语句：

```
$ sudo yum install docker.rpm
```



###### **8、启动 Docker 后台服务**

```
$ sudo systemctl start docker
```

![1554891962200](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554891962200.png)



###### 9、测试运行 hello-world

```
$ sudo docker run hello-world
```

​    如果本地不存在hello-world镜像， 将从docker hub中自动下载。



###### 10、删除docker

```
$ sudo yum remove docker-ce
```

![1554892039187](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554892039187.png)

![1554892043944](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554892043944.png)
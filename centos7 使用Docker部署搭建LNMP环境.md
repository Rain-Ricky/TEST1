# Docker部署LNMP环境



**1、搜索被收藏或使用较多的LNMP镜像**

```
$ sudo docker search -s 10 lamp
```

![1554892995113](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554892995113.png)

**2、下载镜像**

```
$ sudo docker pull imagine10255/centos6-lnmp-php56  
```

![1554889872919](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554889872919.png)

**3、重启**

```
$ systemctl daemon-reload
$ systemctl restart docker
```

  **4、查看镜像**

```
$ docker images
```

![1554893050959](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554893050959.png)

**5、启动容器**

```
$ docker run -d -p 32801:80 -p 32802:443 -p 32803:3306 -p 32804:22  --name lnmp  imagine10255/centos6-lnmp-php56
```

 -d 指的是在后台运行

  -p指定暴露的端口 第一个端口是对外暴露的接口 相对应的是内部的端口。

![1554890367144](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554890367144.png)

**6、启动成功后可以使用docker ps查看正在运行的docker镜像**

```
$ sudo docker ps 
```

![1554890389109](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554890389109.png)


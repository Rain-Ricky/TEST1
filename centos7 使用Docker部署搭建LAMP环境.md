# Centos 7使用Docker部署LAMP环境

### 

**1、搜索被收藏或使用较多的LAMP镜像**

```
$ sudo docker search -s 10 lamp
```

![1554892674700](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554892674700.png)

**2、下载镜像**

```
$ sudo docker pull nickistre/centos-lamp   
```

![1554889160738](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554889160738.png)

**3、使用默认方式启动LAMP**

```
$ sudo docker run -d -p 8080:80 -p 3306:3306 nickistre/centos-lamp
```

  -d 指的是在后台运行

  -p指定暴露的端口 第一个端口是对外暴露的接口 相对应的是内部的端口。

![1554889448532](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554889448532.png)

**4、查看容器运行情况**

```
$ sudo docker ps 
```

![1554892878883](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554892878883.png)


## 构建简单的Dockerfile

###### 1、在docker容器中创建文件夹，并创建Dockfile文件。

```
$ mkdir demo
$ cd demo
$ touch Dockerfile
```

![1554893478666](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554893478666.png)



###### 2、编辑Dockerfile文件

```
$ sudo vim Dockerfile
```

​    文件内容如下：

```
FROM a'lpine：latest
MAINTAINER xbf
CMD echo "hello world"
```

![1554893710385](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554893710385.png)

![1554893729024](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554893729024.png)

构建镜像：-t 是给镜像加一个标签，此标签名是hello_docker,千万要记住这里的一个 **.**  

它的意思是当前目录下东西都打包到镜像中。

![1554893807636](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554893807636.png)



###### 3、查看构建镜像是否成功

```
$ sudo docker images
```

![1554893906423](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554893906423.png)



###### 4、运行镜像

```
$ sudo docker run -it hello_docker
```

![1554893948613](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1554893948613.png)


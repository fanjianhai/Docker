# Docker镜像

## 镜像是什么

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201014171400685.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)



## Docker镜像加载原理

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201014171900464.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020101417230049.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)





## 分层理解

> 特点

Docker镜像都是只读的，当容器启动时， 一个新的可写层被加载到镜像的顶部！

这一层就是我们通常说的容器层， 容器之下的都叫做镜像层

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020081215123458.png)



## commit镜像

```bash
# 1. 启动一个默认的tomcat

[root@iZ2zeg4ytp0whqtmxbsqiiZ ~]# docker run -d --name tomcat007 -p 8888:8080 tomcat
Unable to find image 'tomcat:latest' locally
latest: Pulling from library/tomcat
e4c3d3e4f7b0: Pull complete 
101c41d0463b: Pull complete 
8275efcd805f: Pull complete 
751620502a7a: Pull complete 
a59da3a7d0e7: Pull complete 
9c0f1dffe039: Pull complete 
c886bd27ecb8: Pull complete 
30fb11aa7eaa: Pull complete 
c9f12e463311: Pull complete 
421d9a80377a: Pull complete 
Digest: sha256:988a39f8a105f7578e0493e80ec0b63c084c493ad204143f6ae4996ce264cb92
Status: Downloaded newer image for tomcat:latest
e66df2fe60018a32c19994c940649e899cd0d604d86643e3df8ca8861af5e80f
[root@iZ2zeg4ytp0whqtmxbsqiiZ ~]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                    NAMES
e66df2fe6001        tomcat              "catalina.sh run"   14 seconds ago      Up 12 seconds       0.0.0.0:8888->8080/tcp   tomcat007

# 2. 发现这个默认的tomcat是没有webapps应用， 镜像的原因，官方镜像默认webapps下面是没有内容的
# 3. 我自己拷贝进去了基本的文件

[root@iZ2zeg4ytp0whqtmxbsqiiZ ~]# docker exec -it e66df2fe6001 /bin/bash
root@e66df2fe6001:/usr/local/tomcat# ls
BUILDING.txt	 LICENSE  README.md	 RUNNING.txt  conf  logs	    temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin	      lib   native-jni-lib  webapps  work
root@e66df2fe6001:/usr/local/tomcat# cp -r webapps.dist/* webapps
root@e66df2fe6001:/usr/local/tomcat# 

# 4. 将我们操作过的容器通过commit提价为一个镜镜像！我们以后就使用我们自己制作的镜像了
```

```shell
docker commit 提交容器成为一个新的版本

# 命令和git 原理类似
docker commit -m="提交的描述信息" -a="作者" 容器id 目标镜像名：[TAG]

docker commit -a="xiaofan" -m="add webapps app" d798a5946c1f tomcat007:1.0

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201014182400454.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)






# 1. 名字解释

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013152904564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

- 镜像（image）
	- Docker镜像就好比是一个模板，可以通过这个模板来创建容器服务，tomcat镜像 ===> run ===> tomcat01容器， 通过这个镜像可以创建多个容器（最终服务运行或者项目运行就是在容器中的）
- 容器（container）
	- Docker利用容器技术，独立运行一个或者一组应用， 通过镜像来创建的
	- 启动，停止，删除，基本命令！
	- 就目前可以把这个容器理解为一个简易的linux系统
- 仓库（repository）
	- 存放镜像的地方
	- Docker Hub（默认是国外的）
	- 阿里云,,,都有容器服务（配置镜像加速！）

# 2. Docker 安装

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013153857919.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

- 下载Docker https://docs.docker.com/get-docker/

- 在Centos7上安装 https://docs.docker.com/engine/install/centos/

**帮助文档**

```shell
# 1. 卸载旧的版本
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
                  
# 2. 需要的安装包
yum install -y yum-utils

# 3. 设置镜像的仓库
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo		// 默认用的是国外的仓库，我们一般不用！
    
yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo		// 推荐使用阿里云的，十分的快
    
# 4. 更新yum软件包索引
yum makecache fast

# 5. 安装docker docker-ce社区版 docker-ee企业版
yum install docker-ce docker-ce-cli containerd.io

# 6. 启动docker
systemctl start docker

# 7. 测试
docker version
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020101316215783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

```shell
# 8. 测试helloworld
docker run hello-world
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013162734971.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

```shell
# 9. 查看一下下载的这个hello-world镜像
[root@iZ2zeg4ytp0whqtmxbsqiiZ /]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        9 months ago        13.3kB

# 10. 卸载docker
# 卸载依赖
yum remove docker-ce docker-ce-cli containerd.io
# 删除资源
rm -rf /var/lib/docker

# /var/lib/docker  docker默认的工作路径
```

# 3. 阿里云镜像加速

1. 登录阿里云服务器，找到`容器镜像服务`

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013170139702.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

2. 找到镜像加速器

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013173640736.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

   

3. 配置使用

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://pi9dpp60.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```



# 4. 底层原理

- HelloWorld镜像

  ![](https://img-blog.csdnimg.cn/20200411132204381.png)

  ![](https://img-blog.csdnimg.cn/20200411132044294.png)

![](https://img-blog.csdnimg.cn/20200411132109992.png)



- 底层原理

  Docker Engine是一个客户端-服务器应用程序，具有以下主要组件:

  - 一个服务器，它是一种长期运行的程序，称为守护进程
  - 一个REST API，它指定程序可以用来与守护进程对话并指示它做什么的接口。

  Docker是一个**Client Server结构的系统**，Docker守护进程运行在主机上，然后通过Socket连接从客户 端访问，守护进程从客户端接受命令并管理运行在主机上的容器。**容器，是一个运行时环境就是我们所说的集装箱。**

  ![](https://img-blog.csdnimg.cn/20200411132031597.png)

  

   

- 为什么Docker比Vm快

  - docker有着比虚拟机更少的抽象层。**由于docker不需要Hypervisor实现硬件资源虚拟化,\**运行在docker容器上的程序直接使用的都是实际物理机的硬件资源\**。因此在CPU、内存利用率上docker将会在效率上有明显优势。**
  - **docker利用的是宿主机的内核,而不需要Guest OS**。因此,当新建一个 容器时,docker不需要和虚拟机一样重新加载一个操作系统内核。仍而避免引寻、加载操作系统内核返个比较费时费资源的过程,当新建一个虚拟机时,虚拟机软件需要加载GuestOS,返个新建过程是分钟级别的。**而docker由于直接利用宿主机的操作系统,则省略了返个过程,因此新建一个docker容器只需要几秒钟。**

  ![](https://img-blog.csdnimg.cn/20200411132454634.png)
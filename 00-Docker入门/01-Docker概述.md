# 1. Docker 为什么会出现

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013103809810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013104056508.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)



# 2. Docker的历史

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020101311161547.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)



# 3. [Docker最新超详细版教程通俗易懂](https://www.bilibili.com/video/BV1og4y1q7M4)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200811092952284.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70)

- Docker是基于Go语言开发的！开源项目
- [官网](https://www.docker.com/)
- [官方文档](https://docs.docker.com/)**Docker文档是超详细的**
- [仓库地址](https://hub.docker.com/)

# 4. 虚拟化技术和容器化技术对比
## 4.1. 虚拟化技术的缺点
- 资源占用十分多
- 冗余步骤多
- 启动很慢

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200807193002905.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70)



## 2.2. 容器化技术

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200807193432803.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70)



- 比较Docker和虚拟化技术的不同
	- 传统虚拟机， 虚拟出一条硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件
	- 容器内的应用直接运行在宿主机的内部，容器是没有自己的内核的，也没有虚拟硬件，所以轻便
	- 每个容器间是相互隔离的，每个容器内都有一个属于自己的文件系统，互不影响
- 应用更快速的交互和部署
	- 传统：一堆帮助文档，安装程序
	- Docker： 打包镜像发布测试，一键运行
- 更便捷的升级和扩缩容
- 更简的系统运维
- 更高效的计算资源利用

## 4.3. DevOps

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201013150407661.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

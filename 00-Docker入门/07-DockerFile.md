## ��ʼDockerFile

DockerFile������������docker����Ĺ����ļ�������ű���������һ�£�

ͨ������ű��������ɾ��񣬾�����һ��һ��ģ��ű�һ���������ÿ�������һ�㣡

```shell
# ����һ��dockerfile�ļ��� ���ֿ������
# �ļ������� ָ������д�� ����

FROM centos

VOLUME ["volume01", "volume02"]

CMD echo "----end----"
CMD /bin/bash

# �����ÿһ������Ǿ����һ�㣡
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813102153118.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

```shell
# �����Լ�������
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813103117628.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

�������ⲿһ����һ��ͬ����Ŀ¼��

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813103318110.png#pic_center)

```shell
docker inspect ����id
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813103859654.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

����һ�¸ղŵ��ļ��Ƿ�ͬ�����������ˣ�

���ַ�ʽ����δ��ʹ�õ�ʮ�ֶ࣬ ��Ϊ����ͨ���ṹ���Լ��ľ���

���蹹������ʱ��û�й��ؾ�Ҫ�ֶ�������� -v ����:������·����



## ���ݾ�����

���mysqlͬ�����ݣ�

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813115602683.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

```shell
# ����3��������ͨ�����Ǹղ��Լ�д�ľ�������
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813120430844.png#pic_center)

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813121031935.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

���mysqlʵ�����ݹ���

```shell
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker run -d -p 3344:3306 -v /etc/mysql/conf.d -v /var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7

[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker run -d -p 3344:3306 -v /etc/mysql/conf.d -v /var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql02 --volumes-from mysql01 mysql:5.7
```

**����**

����֮��������Ϣ�Ĵ��ݣ� ���ݾ���������������һֱ������û������ʹ��Ϊֹ��

����һ����־û����˱��أ����ʱ�򣬱��ص������ǲ���ɾ���ģ�



## DockerFile

dockerFile����������docker������ļ�����������ű���

`��������`

`1. ��дһ��dockerFile�ļ�`

`2.docker build ������Ϊһ������`

`3. docker run ���о���`

`4. docker push ��������DockerHub�������ƾ���`

�鿴һ�¹ٷ�����ô���ģ�

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813141504113.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813141235209.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

�ܶ�ٷ��������ǻ��������ܶ๦�ܶ����߱�������ͨ�����Լ���Լ��ľ���

�ٷ���Ȼ����������������һ�����ԣ�



## DockerFile�Ĺ�������

**����֪ʶ��**

1. ÿ�������ؼ��֣�ָ����Ǳ����д��ĸ
2. ִ�д��ϵ���˳��ִ��
3. `#` ��ʾע��
4. ÿ��ָ��ᴴ���ύһ���µľ���㣬���ύ��

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813142333870.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

dockerFile�����򿪷��ģ� �����Ժ�Ҫ������Ŀ�� ������ ����Ҫ��дdockefile�ļ��� ����ļ�ʮ�ּ򵥣�

Docker�����𽥳�Ϊ��ҵ�Ľ�����׼������Ҫ���գ�

���裺���������� ��ά..... ȱһ���ɣ�



DockerFile�� �����ļ��� ������һ�еĲ��裬Դ����

DockerImages�� ͨ��DockerFile�������ɵľ��� ���շ��������еĲ�Ʒ��

Docker�������������Ǿ������������ṩ������



## DockerFileָ��˵��

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813144806291.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

```shell
FROM			# ��������һ�д����￪ʼ����
MAINTAINER		# ������˭д�ģ� ����+����
RUN				# ���񹹽���ʱ����Ҫ���е�����
ADD				# ���裬 tomcat���� ���tomcatѹ�������������
WORKDIR			# ����Ĺ���Ŀ¼
VOLUME			# ���ص�Ŀ¼
EXPOSE			# �����˿�����
CMD				# ָ���������������ʱ��Ҫ���е����ֻ�����һ������Ч�ɱ����
ENTRYPOINT		# ָ���������������ʱ��Ҫ���е���� ����׷������
ONBUILD			# ������һ�����̳�DockerFile ���ʱ��ͻ����� ONBUILD ��ָ�����ָ��
COPY			# ����ADD, �������ļ�������������
ENV 			# ������ʱ�����û���������
```

## ����һ���Լ���centos

```shell
# 1. ��дDockerfile���ļ�
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# cat mydockerfile-centos 
FROM centos
MAINTAINER xiaofan<594042358@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH		# ����Ĺ���Ŀ¼

RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80

CMD echo $MYPATH
CMD echo "---end---"
CMD /bin/bash

# 2. ͨ������ļ��������� ע�������һ�� .
# ���� docker build -f dockerfile�ļ�·�� -t ������:[tag] .

[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# docker build -f mydockerfile-centos -t mycentos:0.1 .

Successfully built d2d9f0ea8cb2
Successfully tagged mycentos:0.1
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813152240210.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)z

���ǿ����г����ؽ��еı����ʷ

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200813152814641.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

> CMD ��ENTRYPOINT����

```shell
CMD			# ָ���������������ʱ��Ҫ���е����ֻ�����һ������Ч�ɱ����
ENTRYPOINT		# ָ���������������ʱ��Ҫ���е���� ����׷������
```

����CMD

```shell
# 1. ��дdockerfile�ļ�
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# vim dockerfile-cmd-test 
FROM centos
CMD ["ls", "-a"]

# 2. ��������
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# docker build -f dockerfile-cmd-test -t cmdtest .

# 3. run���У� �������ǵ�ls -a ������Ч
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# docker run ebe6a52bb125
.
..
.dockerenv
bin
dev
etc
home
lib
lib64

# ��׷��һ������ -l ��� ls -al
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# docker run ebe6a52bb125 -l
docker: Error response from daemon: OCI runtime create failed: container_linux.go:349: starting container process caused "exec: \"-l\": executable file not found in $PATH": unknown.
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# docker run ebe6a52bb125 ls -l

# cmd������� -l�滻��CMD["ls", "-a"]��� -l����������Ա�����
```

����ENTRYPOINT

```shell
# 1. ��дdockerfile�ļ�
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# vim dockerfile-entrypoint-test 
FROM centos
ENTRYPOINT ["ls", "-a"]

# 2. �����ļ�
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# docker build -f dockerfile-entrypoint-test -t entrypoint-test .

# 3. run���� �������ǵ�ls -a ����ͬ����Ч
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# docker run entrypoint-test
.
..
.dockerenv
bin
dev
etc
home
lib

# 4. ���ǵ�׷����� ��ֱ��ƴ�ӵ�ENTRYPOINT����ĺ���ģ�
[root@iZ2zeg4ytp0whqtmxbsqiiZ dockerfile]# docker run entrypoint-test -l
total 56
drwxr-xr-x  1 root root 4096 Aug 13 07:52 .
drwxr-xr-x  1 root root 4096 Aug 13 07:52 ..
-rwxr-xr-x  1 root root    0 Aug 13 07:52 .dockerenv
lrwxrwxrwx  1 root root    7 May 11  2019 bin -> usr/bin
drwxr-xr-x  5 root root  340 Aug 13 07:52 dev
drwxr-xr-x  1 root root 4096 Aug 13 07:52 etc
drwxr-xr-x  2 root root 4096 May 11  2019 home
lrwxrwxrwx  1 root root    7 May 11  2019 lib -> usr/lib
lrwxrwxrwx  1 root root    9 May 11  2019 lib64 -> usr/lib64
drwx------  2 root root 4096 Aug  9 21:40 lost+found

```

## �ο�����

https://www.cnblogs.com/panwenbin-logs/p/8007348.html
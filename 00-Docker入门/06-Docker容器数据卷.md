# 1. �������ݾ�

## 1.1. docker�����ع�

��Ӧ�úͻ��������һ������

���ݣ�������ݶ��������У���ô��������ɾ�������ݾͻᶪʧ��`�������ݿ��Գ־û�`

MySQL������ɾ�ˣ�ɾ����·��`����MySQL���ݿ��Դ洢�ڱ��أ�`

����֮�������һ�����ݹ�������Docker�����в��������ݣ�ͬ�������أ�

����Ǿ�����Ŀ¼�Ĺ��أ������������ڵ�Ŀ¼���ص�linuxĿ¼���棡



**�ܽ᣺ **�����ĳ־û���ͬ������������������Ҳ�ǿ��Թ���ģ�



## 1.2. ʹ�����ݾ�

> ��ʽһ��ֱ��ʹ������������ -v	

```shell
docker run -it -v ����Ŀ¼������Ŀ¼

[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker run -it -v /home/ceshi:/home centos /bin/bash
```



![���������ͼƬ����](https://img-blog.csdnimg.cn/20200812165141715.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

**�����ļ���ͬ��**���������ϸĶ����۲������仯��

![���������ͼƬ����](https://img-blog.csdnimg.cn/2020081216585980.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

**��������**������ͨ����

1. ֹͣ����

2. �������޸��ļ�

3. ��������

4. �����ڵ�����������ͬ���ģ�

   

   
## 1.3. ʵս����װMySQL

˼����MySQL�����ݳ־û������⣡

```shell
# ��ȡ����
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker pull mysql:5.7

# ���������� ��Ҫ�����ݹ��أ� # ��װ����mysql����Ҫ�������루ע�⣩
# �ٷ����ԣ� docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

# �������ǵ�
-d		# ��̨����
-p		# �˿�����
-v		# �����
-e		# ��������
--name	# ����������
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker run -d -p 3344:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7
9552bf4eb2b69a2ccd344b5ba5965da4d97b19f2e1a78626ac1f2f8d276fc2ba

# �����ɹ�֮�������ڱ���ʹ��navicat���Ӳ���һ��
# navicat���ӵ���������3344 --- 3344 �� ������3306ӳ�䣬���ʱ�����ǾͿ���������mysqlඣ�

# �ڱ��ز��Դ���һ�����ݿ⣬�鿴�����ǵ�·���Ƿ�ok��
# �Ժ�������Linux�ϵ��޸Ļ��Զ�ͬ���������У���֮��Ȼ��
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200812174632321.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

   

   

   

 ## 1.4. �����;�������

  ```shell
# ��������
-v ������·��
docker run -d -P --name nginx01 -v /etc/nginx nginx		# -P ���ָ���˿�

# �鿴����volume�����
[root@iZ2zeg4ytp0whqtmxbsqiiZ ~]# docker volume ls
DRIVER              VOLUME NAME
local               561b81a03506f31d45ada3f9fb7bd8d7c9b5e0f826c877221a17e45d4c80e096
local               36083fb6ca083005094cbd49572a0bffeec6daadfbc5ce772909bb00be760882

# ���﷢�֣�������������������أ�������-v ����ֻд�������ڵ�·����û��д�������·����

# ��������
 [root@iZ2zeg4ytp0whqtmxbsqiiZ ~]# docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx nginx
26da1ec7d4994c76e80134d24d82403a254a4e1d84ec65d5f286000105c3da17
[root@iZ2zeg4ytp0whqtmxbsqiiZ ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                   NAMES
26da1ec7d499        nginx               "/docker-entrypoint.��"   3 seconds ago       Up 2 seconds        0.0.0.0:32769->80/tcp   nginx02
486de1da03cb        nginx               "/docker-entrypoint.��"   3 minutes ago       Up 3 minutes        0.0.0.0:32768->80/tcp   nginx01
[root@iZ2zeg4ytp0whqtmxbsqiiZ ~]# docker volume ls
DRIVER              VOLUME NAME
local               561b81a03506f31d45ada3f9fb7bd8d7c9b5e0f826c877221a17e45d4c80e096
local               36083fb6ca083005094cbd49572a0bffeec6daadfbc5ce772909bb00be760882
local               juming-nginx

# ͨ��-v �����������ڵ�·��
# �鿴һ�������
# docker volume inspect juming-nginx

[root@iZ2zeg4ytp0whqtmxbsqiiZ ~]# docker volume inspect juming-nginx
[
    {
        "CreatedAt": "2020-08-12T18:15:21+08:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/juming-nginx/_data",
        "Name": "juming-nginx",
        "Options": null,
        "Scope": "local"
    }
]
  ```

����docker�����ڵľ�û��ָ��Ŀ¼������¶�����`/var/lib/docker/volumes/xxxxx/_data`

����ͨ���������ؿ��Է�����ҵ����ǵ�һ��������������ʹ�õ���`��������`

```shell
# ���ȷ���Ǿ������ػ����������أ�����ָ��·�����أ�
-v	������·��					# ��������
-v	����:������·��			   # ��������
-v /����·��:������·��			  # ָ��·������
```

��չ

```shell
# ͨ�� -v ��������·�� ro rw �ı��дȨ��
ro	readonly	# ֻ��
rw	readwrite	# �ɶ���д

docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:ro nginx
docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:rw nginx

# ro ֻҪ����ro��˵�����·��ֻ��ͨ�������������������������޷�����
```



   

   


# 1.Docker�������ʵս

## Docker��װNginx

```shell
# 1. �������� search ����ȥdocker hub���������Կ��������ĵ�
# 2. ���ؾ��� pull
# 3. ���в���
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
centos              latest              0d120b6ccaa8        32 hours ago        215MB
nginx               latest              08393e824c32        7 days ago          132MB

# -d ��̨����
# -name ����������
# -p �������˿ڣ������ڲ��˿�
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker run -d --name nginx01 -p 3344:80 nginx	# ��̨��ʽ������������
fe9dc33a83294b1b240b1ebb0db9cb16bda880737db2c8a5c0a512fc819850e0
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
fe9dc33a8329        nginx               "/docker-entrypoint.��"   4 seconds ago       Up 4 seconds        0.0.0.0:3344->80/tcp   nginx01
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# curl localhost:3344	# ���ط��ʲ���

# ��������
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker exec -it nginx01 /bin/bash
root@fe9dc33a8329:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@fe9dc33a8329:/# cd /etc/nginx/
root@fe9dc33a8329:/etc/nginx# ls
conf.d		koi-utf  mime.types  nginx.conf   uwsgi_params
fastcgi_params	koi-win  modules     scgi_params  win-utf

```

**�˿ڱ�¶����**

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200812111035666.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70)



# 2. Docker��װTomcat

```shell
# �ٷ���ʹ��
docker run -it --rm tomcat:9.0

# ����֮ǰ���������Ǻ�̨�ģ�ֹͣ������֮�� �������ǿ��Բ鵽��docker run -it --rm һ���������ԣ������ɾ

# ����������
docker pull tomcat

# ��������
docker run -d -p 3344:8080 --name tomcat01 tomcat

# ���Է���û������

# ��������
docker exec -it tomcat01 /bin/bash

# �������⣺1.linux�������ˣ� 2. webapps������Ϊ�գ������ƾ����ɹ�Ĭ������С�ľ������в���Ҫ�Ķ��޳��ˣ���֤��С�����л�������
```

# 3. Docker����es + kibana

```shell
# es ��¶�Ķ˿ںܶ�
# es ʮ�ֵĺ��ڴ�
# es ������һ����Ҫ���õ���ȫĿ¼�� ����
# --net somenetwork	��������

# ����elasticsearch
docker run -d --name elasticsearch --net somenetwork -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2

[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2
a920894a940b354d3c867079efada13d96cf9138712c76c8dea58fabd9c7e96f

# ������linux�Ϳ����ˣ�docker stats �鿴cpu״̬

# ����һ��es�ɹ���
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# curl localhost:9200
{
  "name" : "a920894a940b",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "bxE1TJMEThKgwmk7Aa3fHQ",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}


# �����ڴ����ƣ��޸������ļ� -e ���������޸�
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2
```

## ���ӻ�

- portainer�����������

```shell
docker run -d -p 8088:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer

# ����
[root@iZ2zeg4ytp0whqtmxbsqiiZ home]# curl localhost:8088
<!DOCTYPE html
><html lang="en" ng-app="portainer">

# �������� http://ip:8088

```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200812143512159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70)

- Rancher(CI/CD����)













  
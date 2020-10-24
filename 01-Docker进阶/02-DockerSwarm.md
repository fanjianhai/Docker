# Docker Swarm

**�ٷ��ĵ�**

https://docs.docker.com/engine/swarm/

��Ⱥ

## ���������

1. ��¼�������˺ţ��������̨������ʵ��

   ```shell
   4̨������2G
   ```

   

   ![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817090932979.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

   ![�Ӵ���ʽ](https://img-blog.csdnimg.cn/20200817091433732.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)
   
   **k8s��ʱ���Ҫѡ����1��4G����**

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817092202155.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817092356986.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817092707986.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817093739844.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

���ˣ����ǵķ���������ɹ���

## ��̨������װdocker

�����ǵ�����װһ��

���ɣ� xshellֱ��ͬ��������ʡʱ�䣡

- [Docker�İ�װ](https://blog.csdn.net/fanjianhai/article/details/107860159)



## Swarm��Ⱥ�

- [��������](https://docs.docker.com/engine/swarm/how-swarm-mode-works/nodes/)

  ![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817104128335.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

```shell
docker swarm init --help

ip addr # ��ȡ�Լ���ip���������Ĳ�Ҫ������

[root@iZ2ze58v8acnlxsnjoulk5Z ~]# docker swarm init --advertise-addr 172.16.250.97
Swarm initialized: current node (otdyxbk2ffbogdqq1kigysj1d) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3vovnwb5pkkno2i3u2a42yrxc1dk51zxvto5hrm4asgn37syfn-0xkrprkuyyhrx7cidg381pdir 172.16.250.97:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

```

��ʼ�����`docker swarm init`

docker swarm join ����һ����㣡

```shell
# ��ȡ����
docker swarm join-token manager
docker swarm join-token worker
```

```shell
[root@iZ2ze58v8acnlxsnjoulk6Z ~]# docker swarm join --token SWMTKN-1-3vovnwb5pkkno2i3u2a42yrxc1dk51zxvto5hrm4asgn37syfn-0xkrprkuyyhrx7cidg381pdir 172.16.250.97:2377
This node joined a swarm as a worker.

```

�Ѻ���Ľ�㶼���ȥ

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817101603370.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

100̨��

1. �������ڵ�init
2. ���루�����ߣ�worker��

## RaftЭ��

˫��˫�ӣ�����һ�������ˣ���������Ƿ�����ã�

RaftЭ�飺��֤����������ſ���ʹ�ã�ֻҪ>1, ��Ⱥ���ٴ���3̨��

ʵ�飺

1����docker1����ֹͣ��崻���˫��������һ�����Ҳ����ʹ���ˣ�

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817102811431.png#pic_center)

2. ���Խ���������뿪`docker swarm leave`

![���������ͼƬ����](https://img-blog.csdnimg.cn/202008171034151.png#pic_center)

3. worker���ǹ����ģ������������ 3̨�������Ϊ�˹����㡣
4. [Docker swarm��Ⱥ���ӽڵ�](https://www.cnblogs.com/zoujiaojiao/p/10886262.html)



ʮ�ּ򵥣���Ⱥ�����ã� 3�����ڵ㡣 > 1̨�������

RaftЭ�飺��֤����������ſ���ʹ�ã��߿��ã�

## ��� 

���ԡ������ݣ���Ⱥ��

�Ժ��� docker run��

docker-compose up������һ����Ŀ��������

��Ⱥ�� swarm 	`docker-service`

k8s service

���� => ����

���� => ���� => ������

redis => 10����������ͬʱ����10��redis������

���飺�������񡢶�̬���ݷ��񡢶�̬���·���

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817115608918.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

- �Ҷȷ�������˿ȸ������

  - [������ӵĲ���](https://www.cnblogs.com/apanly/)
  
    ![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817124458860.png#pic_center)

```shell
docker run ���������� ��������������
docker service ���� ���������������������£�
```

�鿴���� 

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817124725880.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

��̬������

```shell
[root@iZ2ze58v8acnlxsnjoulk5Z ~]# docker service update --replicas 3 my-nginx
1/3: running   [==================================================>] 
1/3: running   [==================================================>] 
2/3: running   [==================================================>] 
3/3: running   [==================================================>] 
verify: Service converged 


[root@iZ2ze58v8acnlxsnjoulk5Z ~]# docker service scale my-nginx=5
my-nginx scaled to 5
overall progress: 3 out of 5 tasks 
overall progress: 3 out of 5 tasks 
overall progress: 3 out of 5 tasks 
overall progress: 5 out of 5 tasks 
1/5: running   [==================================================>] 
2/5: running   [==================================================>] 
3/5: running   [==================================================>] 
4/5: running   [==================================================>] 
5/5: running   [==================================================>] 
verify: Service converged 


[root@iZ2ze58v8acnlxsnjoulk5Z ~]# docker service scale my-nginx=1
my-nginx scaled to 1
overall progress: 1 out of 1 tasks 
1/1: running   [==================================================>] 
verify: Service converged 

```

�Ƴ���`docker service rm`

docker swarm��ʵ������

ֻҪ����Ⱥ�����������񡢶�̬���������Ϳ����ˣ�

---



## ������ܽ�

**swarm**

��Ⱥ�Ĺ���ͱ�ţ�docker���Գ�ʼ��һ��swarm��Ⱥ�����������Լ��롣�����������ߣ�

**Node**

����һ��docker��㣬������������һ�����缯Ⱥ�����������ߣ�

**Service**

���񣬿����ڹ�������߹�����������С����ģ��û����ʡ�

**Task**

�����ڵ����ϸ������

![���������ͼƬ����](https://img-blog.csdnimg.cn/2020081713583960.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

> service

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817135939796.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

���� -> ���� -> api -> ���� -> ������㣨����Task����ά����������

> ���񸱱���ȫ�ַ���

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817141046744.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

����service��ʲô��ʽ����

```shell
--mode string                        
Service mode (replicated or global) (default "replicated")

docker service create --mode replicated --name mytom tomcat:7 Ĭ�ϵ�
docker service create --mode global  --name haha alpine ping www.baidu.com
```

��չ�� ����ģʽ "PublishMode":"ingress"

Swarm:

Overlay:

ingress:�����Overlay���磡���ؾ���Ĺ��ܣ�ipvs vip��

```shell
[root@iZ2ze58v8acnlxsnjoulk5Z ~]# docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
74cecd37149f        bridge              bridge              local
168d35c86dd5        docker_gwbridge     bridge              local
2b8f4eb9c2e5        host                host                local
dmddfc14n7r3        ingress             overlay             swarm
8e0f5f648e69        none                null                local


[root@iZ2ze58v8acnlxsnjoulk5Z ~]# docker network inspect ingress
[
    {
        "Name": "ingress",
        "Id": "dmddfc14n7r3vms5vgw0k5eay",
        "Created": "2020-08-17T10:29:07.002315919+08:00",
        "Scope": "swarm",
        "Driver": "overlay",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "10.0.0.0/24",
                    "Gateway": "10.0.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": true,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "ingress-sbox": {
                "Name": "ingress-endpoint",
                "EndpointID": "9d6ec47ec8309eb209f4ff714fbe728abe9d88f9f1cc7e96e9da5ebd95adb1c4",
                "MacAddress": "02:42:0a:00:00:02",
                "IPv4Address": "10.0.0.2/24",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.driver.overlay.vxlanid_list": "4096"
        },
        "Labels": {},
        "Peers": [
            {
                "Name": "cea454a89163",
                "IP": "172.16.250.96"
            },
            {
                "Name": "899a05b64e09",
                "IP": "172.16.250.99"
            },
            {
                "Name": "81d65a0e8c03",
                "IP": "172.16.250.97"
            },
            {
                "Name": "36b31096f7e2",
                "IP": "172.16.250.98"
            }
        ]
    }
]

```



## ��������ѧϰ��ʽ

- Docker Stack

```shell
docker-compose ����������Ŀ
docker stack ��Ⱥ����

# ����
docker-compose up -d wordpress.yaml
# ��Ⱥ
docker stack deploy wordpress.yaml
```



- Docker Secret

```shell
��ȫ���������룡֤�飡

[root@iZ2ze58v8acnlxsnjoulk5Z ~]# docker secret --help

Usage:	docker secret COMMAND

Manage Docker secrets

Commands:
  create      Create a secret from a file or STDIN as content
  inspect     Display detailed information on one or more secrets
  ls          List secrets
  rm          Remove one or more secrets
```



- Docker Config

```shell
���ã�
[root@iZ2ze58v8acnlxsnjoulk5Z ~]# docker config --help

Usage:	docker config COMMAND

Manage Docker configs

Commands:
  create      Create a config from a file or STDIN
  inspect     Display detailed information on one or more configs
  ls          List configs
  rm          Remove one or more configs

```

## ��չ��k8s

**��ԭ��ʱ��**

Go���ԣ��������գ� Java Go��

�������ԣ�



B���ԣ�C���ԵĴ�ʼ�ˡ�Unix��ʼ��VB

go`ָ��`
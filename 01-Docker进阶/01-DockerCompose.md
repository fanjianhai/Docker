# Docker Compose

## ���

Docker

Dockerfile build run �ֶ�����������������

΢����100��΢����������ϵ��

Docker Compose �����ɸ�Ч�Ĺ����������������ж��������

>�ٷ�����

1. �������ж������
2. YAML file�����ļ�
3. single command����������Щ��

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application��s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see [the list of features](https://docs.docker.com/compose/#features).

4. ���еĻ���������ʹ��compose��

Compose works in all environments: production, staging, development, testing, as well as CI workflows. You can learn more about each case in [Common Use Cases](https://docs.docker.com/compose/#common-use-cases).

**�����裺**

Using Compose is basically a three-step process:

1. Define your app��s environment with a `Dockerfile` so it can be reproduced anywhere.
   - Dockerfile��֤���ǵ���Ŀ���κεط���������
2. Define the services that make up your app in `docker-compose.yml` so they can be run together in an isolated environment.
   - services ʲô�Ƿ���
3. Run `docker-compose up` and Compose starts and runs your entire app.
   - ������Ŀ

**���ã�������������**

> ���Լ������

Compose��Docker�ٷ��Ŀ�Դ��Ŀ����Ҫ��װ��

`Dockerfile`�ó������κεط����С�web����redis��mysql��nginx... ��������� run

Compose

```yaml
version: '2.0'
services:
  web:
    build: .
    ports:
    - "5000:5000"
    volumes:
    - .:/code
    - logvolume01:/var/log
    links:
    - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

docker-compose up 100������

Compose����Ҫ����

- ����services�� ������Ӧ�ã�web��redis��mysql...��
- ��Ŀproject�� һ�����������



## ��װ

1. ����

```shell
# �����ṩ ��û�����سɹ���
curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# ���ڵ�ַ
curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.5/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```

2. ��Ȩ

```shell
chmod +x /usr/local/bin/docker-compose
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200814210859399.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)



## ����(����ͨ��)

��ַ��https://docs.docker.com/compose/gettingstarted/

pythonӦ�á� ��������redis��



```bash
# 1. ����Ŀ¼
$ mkdir composetest
$ cd composetest

# 2. Ӧ��app.py
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
    
# 3. requirements.txt
flask
redis

# 4. Dockerfile Ӧ�ô��Ϊ����
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]

# 5. Docker-compose yaml�ļ�����������������Ҫ�Ļ��� web��redis�� ���������߷���
version: '3.8'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
  redis:
    image: "redis:alpine"

# 6. ����compose ��Ŀ ��docker-compose up��

# 7.����
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/2020101604241837.png#pic_center)

���̣�

1. ��������
2. ִ��Docker-compose.yaml
3. ��������



## yaml����

docker-compose.yaml ���ģ�

https://docs.docker.com/compose/compose-file/#compose-file-structure-and-examples



## ��Դ��Ŀ������

https://docs.docker.com/compose/wordpress/

���س��򡢰�װ���ݿ⡢����....

composeӦ�� => һ������

1. ������Ŀ��docker-compse.yaml��
2. �����Ҫ�ļ���Dockerfile
3. �ļ�׼����ȫ��һ��������Ŀ����

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200815160042298.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)



## ʵս���Լ���д΢��������

1. ��д��Ŀ΢����

2. Dockerfile��������

   ```shell
   FROM java:8
   
   COPY *.jar /app.jar
   
   CMD ["--server.port=8080"]
   
   EXPOSE 8080
   
   ENTRYPOINT ["java", "-jar", "/app.jar"]
   ```

   

3. docker-compose.yml������Ŀ

   ```yaml
   version '3.8'
   services:
     xiaofanapp:
       build: .
       image: xiaofanapp
       depends_on:
         - redis
       ports:
         - "8080:8080"
   
     redis:
       image: "library/redis:alpine"
   ```

   

4. �������������� docker-compose up

```shell
docker-compose down			# �ر�����
docker-compose up --build 	# ���¹���
```

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200815164213233.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200815163905484.png#pic_center)

**�ܽ᣺**

**���̡���������**

��Ŀ compose�� ����

- ���� Project
- ����
- ���� ����ʵ���� docker k8s ����
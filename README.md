# 服务器docker搭建集成

__请在shell中运行文档中的脚本，toolbox用户请使用toolbox自带的终端__

## 单独构建运行容器

1. 构建tomcat镜像

```shell
docker build -t fpure/tomcat ./tomcat
```

2. 运行tomcat1容器

```shell
docker run --name tomcat1 -d \
# -v $PWD/tomcat-v1/conf:/usr/local/tomcat/conf:ro \
-v $PWD/tomcat-v1/logs:/usr/local/tomcat/logs \
-v $PWD/tomcat-v1/webapps:/usr/local/tomcat/webapps \
# -p 8080:8080 \
fpure/tomcat
```

3. 运行tomcat2容器

```shell
docker run --name tomcat2 -d \
# -v $PWD/tomcat-v2/conf:/usr/local/tomcat/conf:ro \
-v $PWD/tomcat-v2/logs:/usr/local/tomcat/logs \
-v $PWD/tomcat-v2/webapps:/usr/local/tomcat/webapps \
# -p 8090:8080 \
fpure/tomcat
```

4. 运行nginx容器

```shell
docker run --name nginx -d \
-v $PWD/nginx-v/nginx.conf:/etc/nginx/nginx.conf:ro \
-v $PWD/nginx-v/html:/usr/share/nginx/html:ro \
-v $PWD/nginx-v/logs:/var/log/nginx \
-p 80:80 \
--link tomcat1:docker-tomcat1 \
--link tomcat2:docker-tomcat2 \
nginx:1.16.1
```

## 使用docker-compose构建运行

```shell
# 构建运行所有容器
docker-compose up -d

# 删除所有容器和镜像
docker-compose down

# 重启服务
docker-compose restart
```
## 部署

##### nginx

```shell
docker pull nginx
docker run -it -d --name nginx01 -p 80:80 nginx
```

##### elasticsearch+kibana

```shell
#默认配置启动
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2 
#限制内存使用
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2
#查看容器ip "IPAddress": "172.17.0.2"
docker inspect e68a05cdc87d |grep IPAddress
#配置kibana连接es容器ip地址172.17.0.2
```

##### portainer

```shell
docker run -d -p 9000:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portianer/portainer
```

##### cmmit镜像

```shell
docker commit -m="dist" -a="wangyu" 2042daa8605b tomcat:dist
```

##### 数据卷挂载

```shell
#指定路径挂载容器home目录到宿主机/home/centos目录下
docker run -it -v /home/centos:/home centos /bin/bash
#具名卷挂载
docker run -it -v centos-volume:/home centos /bin/bash
#只读，只能宿主机修改路径下的文件
docker run -it -v centos-volume:/home:ro centos /bin/bash
#读写
docker run -it -v centos-volume:/home:rw centos /bin/bash
#匿名挂载，容器内路径
#查看所有挂载卷
docker volume ls
#查看具名卷挂载路径
docker volume centos-volume
#查看匿名卷挂载路径 容器ID
docker inspect 146a9832fdd9
docker inspect 146a9832fdd9 |grep Source
```

##### mysql

```shell
#创建mysql容器
docker run -d -p 3306:3306 --name DockerMySQL -e MYSQL_ROOT_PASSWORD=123456 mysql
#创建mysql容器，挂载配置文件、数据文件
docker run -d -p 3306:3306 --name DockerMySQL -e MYSQL_ROOT_PASSWORD=123456 -v /home/mysql/conf:/etc/mysql/conf.d -v/home/mysql/data:/var/lib/mysql mysql:8.0.25

```

```shell
#多个mysql数据共享
docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7

docker run -d -p 3320:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql02 mysql:5.7

docker run -d -p 3330:3306 -e MYSQL_ROOT_PASSWORD=123456 --name mysql02 --volumes-form mysql01 mysql:5.7
#docker的数据卷生命周期直到没有任何人使用为止
```

##### DockerFile

###### 基础知识：

- 保留关键字命令必须是大写字母
- 每一个关键字从上到下顺序执行
- #表示注释
- 每一个指令都会提交一个新的镜像层，并提交

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg2020.cnblogs.com%2Fblog%2F1869289%2F202005%2F1869289-20200529090814461-1122968296.png&refer=http%3A%2F%2Fimg2020.cnblogs.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1625668972&t=ed71a20cc39b6aa16afc1c00a7da1b4c)

DockerFile是面向开发的镜像构建文件，发布项目时可以通过编写DockerFile文件，发布镜像。DockerImages就是通过DockerFile构建生成的镜像，然后通过Image创建镜像容器。

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fcommunity.arm.com%2Fresized-image%2F__size%2F1040x0%2F__key%2Fcommunityserver-blogs-components-weblogfiles%2F00-00-00-21-12%2FDockerfile-flow.png&refer=http%3A%2F%2Fcommunity.arm.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1625669318&t=1e950ba99164dc956541301c58d61f78)

```shell
FROM 		# 基础镜像，一切从这里开始
MAINTAINER 	# 镜像的作者描述
RUN 		# 镜像构建的时候需要运行的命令
ADD 		# 添加内容，例如tomcat压缩包
WORKDIR		# 镜像的工作目录
VOLUME 		# 挂载的目录
EXPOST 		# 保留端口配置
CMD 		# 指定这个容器启动的时候要运行的指令，只有最后一个生效，可被替代
ENTRYPOINT 	# 指定这个容器启动的时候要运行的指令，可追加命令
ONBUILD		# 当构建一个被继承DockerFile，这个时候就会运行ONBUILD的指令
COPY		# 类似ADD，将文件拷贝到镜像中
ENV			# 构建的时候设置环境变量
```

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fupload-images.jianshu.io%2Fupload_images%2F6870990-744e06b25e051ac7.png&refer=http%3A%2F%2Fupload-images.jianshu.io&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1625669843&t=66bd777f757e95da69443b85ff7b346a)
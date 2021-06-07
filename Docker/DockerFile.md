## DockerFile

通过DockerFile脚本可以生成镜像

```shell
#vi dockerfile01
FROM centos
VOLUME ["volume01","volume02"]
CMD echo "---end---"
CMD /bin/bash
```

```shell
docker build -f dockerfile01 -t wangyu/centos .
```


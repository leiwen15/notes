# 容器

## 打镜像 image
```shell
docker build . --build-arg "HTTP_PROXY=http://10.21.142.20:8080/" --build-arg "HTTPS_PROXY=http://10.21.142.20:8080/" --build-arg "NO_PROXY=localhost,127.0.0.1,.example.com" -t engine_32:0.1
```

## docker 创建容器

### docker 和宿主机之间共享文件  -v
#### 挂载一个文件夹
+ docker run -v /root/test_docker_file:/root/ engine_32:0.1
#### 挂载多个文件夹
+ docker run -v /root/test_docker_file:/root/ -v /root/auto_test/pattern:/root/auto_test/pattern/ engine_32:0.1
### docker 与宿主机共享网络
#### 便可以与宿主机共享网络，可以在容器内访问公司的github.local
+ ```shell
  docker run -v /root/test_docker_file:/root/ \
  -v /root/auto_test/pattern:/root/auto_test/pattern/ \
  -it --network=host engine_32:0.1
  ```
## 让容器在后台运行
+ docker run -d engine_32
## 进入docker 容器查看
+ docker exec -it youthful_bassi /bin/bash
+ docker exec -it stupefied_cray /bin/bash
+ docker exec -it dd61 /bin/bash
# 容器

## centos 安装docker(无坑版)
+ https://blog.csdn.net/qq_43674360/article/details/124674846
## 打镜像 image
```shell
docker build . --build-arg "HTTP_PROXY=http://10.21.142.20:8080/" --build-arg "HTTPS_PROXY=http://10.21.142.20:8080/" --build-arg "NO_PROXY=localhost,127.0.0.1,.example.com" -t engine_32:0.4
```

## docker 创建容器

### docker 和宿主机之间共享文件  -v
#### 挂载一个文件夹
+ docker run -v /root/test_docker_file:/root/ engine_32:0.1
#### 挂载多个文件夹
+ docker run -v /root/test_docker_file:/root/ -v /root/auto_test/pattern:/root/auto_test/pattern/ engine_32:0.1
+ ```shell
  docker run -v /root/test_docker_file:/root/ \
  -v /root/auto_test/pattern:/root/auto_test/pattern/ \
  -it --network=host engine_32:0.4
  ```
### docker 与宿主机共享网络
#### --network=host，即与宿主机共享网络
#### 便可以与宿主机共享网络，可以在容器内访问公司的github.local
+ ```shell
  docker run -v /root/auto_test/pattern_source:/root/auto_test/pattern_source/ \
  -v /root/auto_test/pattern:/root/auto_test/pattern/ \
  -it --network=host engine_32:0.4
  ```
## 让容器在后台运行
+ docker run -d engine_32
## 进入docker 容器查看
+ docker exec -it youthful_bassi /bin/bash
+ docker exec -it stupefied_cray /bin/bash
+ docker exec -it dd61 /bin/bash·
  
## 查看容器的内容()
+ docker cp 785d:/logs/temp ./
+ docker cp a335:/root/auto_test ./

## docker的container的持久化
### 容器的生命周期依赖于启动时的命令，只要该命令不结束，容器便不会退出
### -d 可以让容器在后台运行
+ docker run centos /bin/bash -d -c "while true ; do sleep 1 ; done"

## 容器可以利用 ssh login
### 需求：通过 SSH 登录到容器中进行一些修改
### 做法：将容器中的SSH端口映射到宿主机，并在容器中安装openssh服务
+ https://blog.csdn.net/qq_39626154/article/details/82856865
#### 一、创建容器
+ PS: 当使用宿主机网络, --network=host时，自定义的端口将被忽略
+ ```shell
  docker run -d -v /root/auto_test/pattern_source:/root/auto_test/pattern_source/ \
  -v /root/auto_test/pattern:/root/auto_test/pattern/ \
  -it --name test_pattern \
  -p 2222:22 engine_32:0.4
  ``` 
#### 二、进入容器，安装 openssh 服务
+ docker exec -it test_pattern /bin/bash
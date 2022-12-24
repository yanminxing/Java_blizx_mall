# 项目版本

1 jdk 17

2 springboot 3.0.1

#  1 开发环境的安装

## 1 linux虚拟机--virtualBox

## 2 安装vagrant

```
// 1 查看vagrant是否安装好
vagrant

// 2 初始化一个 centos7 系统
Vagrant init centos/7

// 3 可启动虚拟机
vagrant up

// 4 自动使用 vagrant 用户连接虚拟机
vagrant ssh

```



## 2   安装docker

```
// 1 卸载
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
                  
// 2 设置仓库
$ sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
  
 // 3 docker命令安装地址
 $ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
    
// 3 安装社区版
 $ sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    
    
// 4 启动docker
 $ sudo systemctl start docker
 
// 5 查看版本
docker -v

// 6 开机自启
sudo systemctl enable docker

// 7 配置镜像加速（阿里云）
sudo mkdir -p /etc/docker

sudo tee /etc/docker/daemon.json <<-'EOF' 
{ 
	"registry-mirrors": ["https://82m9ar63.mirror.aliyuncs.com"]
}
EOF

sudo systemctl daemon-reload

sudo systemctl restart docker

```

## 3 docker安装mysql

```
// 安装mysql
sudo docker pull mysql:5.7

// 检查镜像
sudo docker images

// 创建实例并启动（需要root命令）
docker run -p 3306:3306 --name mysql \
-v /mydata/mysql/log:/var/log/mysql \
-v /mydata/mysql/data:/var/lib/mysql \
-v /mydata/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-d mysql:5.7

// 查看运行中容器
docker ps

// 进入docker里面的容器
 docker exec -it mysql /bin/bash
 
 // 查看目录
ls /

// 退出容器
exit;

// 编辑配置文件
vi /mydata/mysql/conf/my.cnf

// 重启数据库
docker restart mysql

```

##  4 下载和安装redis

```
// 安装(sudo)
docker pull redis


// 创建目录结构（为了配置）
mkdir -p /mydata/redis/conf
touch /mydata/redis/conf/redis.conf // 创建

// 配置
docker run -p 6379:6379 --name redis -v /mydata/redis/data:/data \
-v /mydata/redis/conf/redis.conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf

// 链接redis
docker exec -it redis redis-cli
```



# 2 使用idea创建微服务项目

1 模块

商品服务、仓储服务、订单服务、优惠券服务、用户服务

2 共同：

- web、openfeign模块
- 每一个服务，包名都是com.blizx.xxx
- 模块名：blizx-xxx
- 

![image-20221224172539421](C:\Users\cml\AppData\Roaming\Typora\typora-user-images\image-20221224172539421.png)

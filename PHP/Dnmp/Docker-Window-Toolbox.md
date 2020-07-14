# 1. 安装Docker Toolbox
https://github.com/docker/toolbox/releases [查看版本]
https://github.com/docker/toolbox/releases/download/v19.03.1/DockerToolbox-19.03.1.exe

下载完毕，打开exe文件，一路next，完成安装，以下是安装后的应用  
![Demo Image](./imaegs/docker-win-toolbox.png)

# 2. 初始化Docker
#### 2.1 初始化
双击 Docker Quickstart Terminal, 等待docker  
![Demo Image](./imaegs/docker-win-toolbox1.png)
初始化成功  
![Demo Image](./imaegs/docker-win-toolbox2.png)
#### 2.2 查看VM配置
打开Oracle VM VirtualBox，这是运行的容器  
![Demo Image](./imaegs/docker-win-toolbox3.png)
#### 2.3 调整设置【可忽略】
- 系统可调整容器运行的内存【需要停止容器再设置】
- 共享文件夹，是docker的挂载文件夹，默认是用户文件夹

![Demo Image](./imaegs/docker-win-toolbox4.png)

# 3. dnmp
#### 3.1 下载
https://gitlab.sheincorp.cn/zhangbofa/dnmp-tms.git  
项目放到桌面上【共享目录是 /c/Users/】
#### 3.2 调整配置
- 将docker-compose-win-toolbar.yml => docker-compose.yml
- 将env.sample => .env文件，并且自定义组件的端口【如不修改，则使用默认端口】

# 4. MySql配置问题修改权限
#### 4.1 问题描述
由于mysql 高版本,对mysql.cnf文件有权限要求，不能为777。但是共享文件夹的权限均为777
#### 4.2 具体错误信息
```
Docker mysql [Warning] World-writable config file '.cnf' is is ignored
```
#### 4.3 解决方式
- 打开 Docker Quickstart Terminal
- 执行命令,进入虚拟机docker-machine ssh default
- 执行 chmod 0444 /c/Users/用户名/Desktop/dnmp-tms/services/mysql/mysql.cnf

# 5. 环境构建
#### 5.1 执行命令
```
$ cd 项目根目录
$ docker-compose up -d          # 构建镜像，并启动
```
#### 5.2 查看容器情况
```
$ docker-compose ps             # 查看镜像启动情况
$ docker-compose logs mysql     # 查看mysql启动日志情况
```

![Demo Image](./imaegs/docker-ps.png)

#### 5.3 访问应用
以RabbitMQ为例子, 默认地址是 192.168.99.100
![Demo Image](./imaegs/docker-rabbitmq.png)

# 6. 配置应用
- 应用在 ./www文件夹下
- nginx在 ./services/nginx/conf.d下

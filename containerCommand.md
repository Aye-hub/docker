## 新建并启动容器
```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```
### `options`说明：
- --name="容器新名字"：为容器指定一个名称
- -d：后台运行容器，并返回容器ID，即启动守护式容器
- -i：以交互模式运行容器  配合`-t`使用
- -t：为容器重新分配一个伪输入终端  配合`-i`使用
- -P：随机端口映射
- -p：指定端口映射
    - ip:hostPort:containerPort
    - ip::containerPort
    - hostPort:containerPort
    - containerPort

### 实例
```bash
# 以交互模式启动一个容器
docker run -it 容器名/容器id
```
```bash
# 以后台模式启动一个容器
docker run -d nginx
```

## 列出当前所有正在运行的容器
```bash
docker ps [options]
```
### 参数说明
```bash
# 显示最近创建的容器
docker ps -l

# 列出当前所有正在运行的容器，包括历史的
docker ps -a

# 显示最近5个创建的容器
docker ps -n 5

# 只显示容器编号
docker ps -lq

# 不截断输出
docker ps --no-trunc
```


## 退出容器
```bash
# 容器停止退出
exit

# 容器不停止退出
ctrl+P+Q
```

## 启动容器
```bash
docker start 容器名/容器id
```

## 重启容器
```bash
docker restart 容器名/容器id
```

## 停止容器
```bash
docker stop 容器id/容器名
```

## 强制停止容器
```bash
docker kill 容器id/容器名
```

## 删除已停止的容器
```bash
docker rm 容器id

# 一次性删除多个容器
docker rm -f $(docker ps -a -q)
docker ps -a -q | xargs docker rm
```

## 以后台模式启动一个容器
```bash
docker run -d 容器名
```
> 问题：使用`docker ps -a`查看，发现容器已经退出

!> 说明：`Docker`容器后台运行，就必须有一个前台进程

!> 容器运行的命令如果不是那些一直挂起的命令（如`top`、`tail`），就会自动退出

## 查看容器日志
```bash
docker logs -f -t --tail 容器id
```

### 参数说明
- -t：加入时间戳
- -f：跟随最新的日志打印
- --tail 数字：显示最后多少条

## 查看容器内运行的进程
```bash
docker top 容器id
```

## 查看容器内部细节
```bash
docker inspect 容器id
```

## 进入正在运行的容器并以命令行交互
```bash'
docker exec -it 容器id bashShell
# 或
docker attach 容器id
```

### 区别：
-attach：直接进入容器启动命令的终端，不会启动新的进程
-exec：在容器中打开新的终端，并且可以启动新的进程

## 容器内拷贝文件到主机
```bash
docker ps 容器id:容器内路径 目的主机路径
```
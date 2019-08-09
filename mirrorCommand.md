## 帮助命令

### 验证
```bash
docker version
```

### 显示`Docker`信息
```bash
docker info
```

### 帮助命令
```bash
docker --help
```

## 镜像命令

### 列出本地主机上的镜像
```bash
docker images
```

#### 参数说明
```bash
# 列出本地所有的镜像（包括中间映像层）
docker images -a

# 只显示镜像ID
docker images -q

# 显示镜像的摘要信息
docker images --digests

# 显示完整的镜像信息
docker images --no-trunc
```

#### 列表说明：
|    REPOSITORY    |    TAG     | IMAGE ID |   CREATED    | VIRTUAL SIZE |
| :--------------: | :--------: | :------: | :----------: | :----------: |
| 表示镜像的仓库源 | 镜像的标签 |  镜像ID  | 镜像创建时间 |   镜像大小   |

### 从`Docker Hub`查找镜像
```bash
docker search 镜像名
```

#### 参数说明
```bash
# 只列出 automated build类型的镜像
docker search --automated 镜像名

# 显示完整的镜像描述
docker search --no-trunc 镜像名

# 列出收藏数不小于指定值的镜像
docker search -s 20 镜像名
```

## 下载镜像
```bash
docker pull 镜像名
```
> 等价于`docker pull 镜像名:latest`，默认下载最新版本。

## 删除镜像
```bash
docker rmi 镜像名

# 强制删除
docker rmi -f 镜像名

# 删除多个
docker rmi -f 镜像名1:TAG 镜像名2:TAG

# 删除全部
docker rmi -f $(docker images -qa)
```

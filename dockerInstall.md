## 三要素

### 镜像
`Docker`镜像（image）就是一个只读的模板，镜像可以用来创建`Docker`容器，一个镜像可以创建很多容器。

### 容器
`Docker`利用容器（Container）独立运行的一个或一组应用。容器是用镜像创建的运行实例。

### 仓库
仓库（Repository）是集中存放镜像文件的场所。

## 仓库/镜像/容器概念
- `image`文件生成的容器实例，本身也是一个文件，称为镜像文件
- 一个容器运行一种服务，当我们需要的时候，就可以通过`Docker`客户端创建一个对应的运行实例，也就是我们的容器。
- 仓库就是放了一堆镜像的地方，我们可以把镜像发布到仓库种，需要的时候从仓库中拉下来就可以了。

## Docker安装并设置镜像加速
### **下载rpm包**

**首先，我们打开链接：**
[点击这里](https://download.docker.com/linux/centos/7/x86_64/stable/Packages/)

**下载以下2个rpm包**

`docker-ce-17.03.0.ce-1.el7.centos.x86_64.rpm`

`docker-ce-selinux-17.03.0.ce-1.el7.centos.noarch.rpm`

### **安装防火墙**

```bash
yum -y install iptables-services
```

**启动防火墙**

```bash
systemctl start iptables
```

**设为开机自启**

```bash
systemctl enable iptables
```

**清空默认规则**

```bash
iptables -F
```

**保存默认规则**

```bash
service iptables save
```

### 更新软件包

```bash
yum update
```

**重启**

```bash
reboot
```

### 安装rpm包

**在root目录下新建docker文件夹，把下载的两个文件放到文件夹里。**

**安装rpm包**

```bash
yum -y install *
```

**验证是否安装成功**

```bash
systemctl start docker
```

```bash
systemctl enable docker
```

**查看运行状态**

```bash
systemctl status docker
```

**查看是否能正常运行**

```bash
docker run hello-world
```

**如果看到 "Hello from Docker!"说明docker安装成功。**

![](https://user-gold-cdn.xitu.io/2019/8/1/16c4b00169f7aeb2?w=787&h=418&f=png&s=29448)

> 如果执行 `docker run hello-world` 的时候报`docker: Error response from daemon: Get https://registry-1.docker.io/v2/XXX`，请先执行底下的步骤设置加速，最后执行该命令即可解决。

### **Docker 镜像仓库加速配置**

```bash
cp /lib/systemd/system/docker.service  /etc/systemd/system/docker.service
```

**给权限**

```bash
chmod a+x /etc/systemd/system/docker.service
```

**打开管理脚本**

```bash
vim /etc/systemd/system/docker.service
```

**在 ExecStart=/usr/bin/dockerd 后加上下面这句**

```bash
--registry-mirror=https://kfp63jaj.mirror.aliyuncs.com
```

> 其中`https://kfp63jaj.mirror.aliyuncs.com`，这个地址大家可以去[阿里云Docker官网](https://dev.aliyun.com/)获取。也可以使用上面的地址，因为是免费的嘛。

**获取加速镜像地址（可选）**

控制台找到容器镜像服务，然后在镜像中心下的镜像加速器得到加速地址。

![](https://user-gold-cdn.xitu.io/2019/8/1/16c4b0031c1baeb8?w=938&h=885&f=png&s=169217)

**接下来重载管理脚本**

```bash
systemctl daemon-reload
```

**重启docker**

```bash
systemctl restart docker
```

**查看进程**

```bash
ps -ef|grep docker
```

**如何看到刚才链接的这句话，说明加速成功。**

![](https://user-gold-cdn.xitu.io/2019/8/1/16c4b0017238276c?w=764&h=192&f=png&s=16835)


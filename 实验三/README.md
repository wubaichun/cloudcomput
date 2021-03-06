### 1.Centos 7安装Docker

更新应用程序数据库

```
sudo yum check-update
```

![](./tupian/1.png)

***添加Docker官方仓库，安装最新Docker/***

```
curl -fsSL https://get.docker.com/ | sh
```

![](./tupian/2.png)

![](./tupian/3.png)

![](./tupian/4.png)

***启动Docker/***

```
sudo systemctl start docker
```

***设置Docker自启动/***

```
sudo systemctl enable docker
```

![](./tupian/5.png)

***查看Docker 版本信息/***

```
docker version
```

### 2.Docker加载CentOS镜像

***拉取 Centos 7/***

```
docker pull centos:7
```

***拉取完毕后查看镜像/***

```
docker images
```

![](./tupian/6.png)



***运行Docker容器

```
docker run -d -it --privileged --name wordpress -p 8888:80 -d centos:7 /usr/sbin/init
```

***查看已启动的容器/***

```
docker ps
```

![](./tupian/7.png)

***进入容器前台

```
docker exec -it 2d5 /bin/bash
```

![](./tupian/8.png)

### 3.容器中安装wordpress

#### 1.安装Apache Web服务器

***连接ssh后使用yum安装/***

```
yum install httpd
```

![](./tupian/9.png)

```
systemctl start httpd.service
```

***设置开机自启/***

```
systemctl enable httpd.service
```

![](./tupian/10.png)

访问服务器公网IP,出现下图代表Apache安装成功

![](./tupian/11.png)

#### 2.安装MySQL

***安装MariaDB/***

```
yum install mariadb-server mariadb
```

![](./tupian/12.png)

***启动MariaDB/***

```
systemctl start mariadb
```

***设置MySQL的root密码/***

```
mysql_secure_installation
```

![](./tupian/13.png)

初始密码为空，提示输入正确密码，直接回车，再设置密码，其他选择Y



***设置开机自启MariaDB/***

```
systemctl enable mariadb.service
```

![](./tupian/14.png)

#### 3.安装PHP

```
yum install epel-release yum-utils
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```

![](./tupian/16.png)

![15](./tupian/15.png)



***因为WordPress需要php5.6以上版本的支持，我们更新到7.2版本仓库/***

```
yum-config-manager --enable remi-php72
```

![](./tupian/17.png)

***安装PHP以及php-mysql/***

```
yum install php php-mysql
```

![](./tupian/18.png)

***查看安装的php版本/***

```
php -v
```

![](./tupian/19.png)

***重启Apache服务器以支持PHP/***

```
systemctl restart httpd.service
```

运行PHP，需要启动PHP附加模块/***

```
yum install php-fpm php-gd
```

![](./tupian/20.png)

***重启Apache服务/***

```
service httpd restart
```

![](./tupian/21.png)

#### 4.安装WordPress以及完成相关配置

***登录数据库/***

```
mysql -u root -p
```

***为WordPress创建一个新的数据库/***

```
CREATE DATABASE 数据库名 ;
```

***进入刚创建的数据库/***

```
use 数据库名 ;
```

![](./tupian/22.png)

***为WordPress创建一个独立的MySQL用户并授权给数据库访问权限/***

```
CREATE USER 用户名@localhost IDENTIFIED BY '密码';
GRANT ALL PRIVILEGES ON 数据库名.* TO 用户名@localhost IDENTIFIED BY '密码';
```

![](./tupian/23.png)

![](./tupian/24.png)

***刷新MySQL的权限/***

```
FLUSH PRIVILEGES;
```

![](./tupian/25.png)

***安装WordPress/***

```
tar xzvf latest.tar.gz
```

![](./tupian/26.png)

![](./tupian/27.png)

![](./tupian/28.png)

![](./tupian/29.png)

![](./tupian/30.png)

接下来访问你的服务器公网IP，就能进入WordPress安装的web页

![](./tupian/31.png)

![](./tupian/32.png)

###  4.推送带有wordpress的镜像

***前往[docker hub](https://hub.docker.com/)注册账号，下面需要用到。/***

***将容器生成镜像 (所生成的镜像名由 “Docker用户名/Docker仓库名“组成 ，否则推送会报错： denied: requested access to the resource is denied )/***

```
docker commit -a "Docker用户名" -m "提交描述" 容器id 镜像名:tag标签
```

![](./tupian/33.png)

***登录Docker/***

```
docker login
```

![](./tupian/34.png)

***推送镜像/***

```
docker push 镜像名:tag标签
```

![](./tupian/35.png)

***登录Docker网页查看仓库/***

![](./tupian/36.png)

![](./tupian/37.png)






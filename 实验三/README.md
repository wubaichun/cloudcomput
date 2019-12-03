### 1.Centos 7安装Docker

***更新应用程序数据库\***

```
sudo yum check-update
```

![](新建文件夹 (5)\QR[CV$F0EBG[VKR4@5$@LMI.png)

***添加Docker官方仓库，安装最新Docker\***

```
curl -fsSL https://get.docker.com/ | sh
```

![](新建文件夹 (5)\9_VM{D1ZZZTSMA@XHY_0C{1.png)

![](新建文件夹 (5)\V43~NCC5QKEB]IL1OTUY5(H.png)

![](新建文件夹 (5)\GQFWFV0KZ{0O(@K_VCNA%9Q.png)

***启动Docker\***

```
sudo systemctl start docker
```

***设置Docker自启动\***

```
sudo systemctl enable docker
```

![](新建文件夹 (5)\XJ89K%REOX2%CQC0%$F}V)R.png)

***查看Docker 版本信息\***

```
docker version
```

### 2.Docker加载CentOS镜像

***拉取 Centos 7\***

```
docker pull centos:7
```

***拉取完毕后查看镜像\***

```
docker images
```

![](新建文件夹 (5)\C2L{8HBAWB@4F$T)A2DLTEY.png)



***运行Docker容器

```
docker run -d -it --privileged --name wordpress -p 8888:80 -d centos:7 /usr/sbin/init
```

***查看已启动的容器\***

```
docker ps
```

![](新建文件夹 (5)\FRAAFNOJ$[~ZA_F04}LRFQY.png)

***进入容器前台

```
docker exec -it 2d5 /bin/bash
```

![](新建文件夹 (5)\8`YBA]0FEG@{KW9@78R[MW9.png)

### 3.容器中安装wordpress

#### 1.安装Apache Web服务器

***连接ssh后使用yum安装\***

```
yum install httpd
```

![](新建文件夹 (5)\(V$ZY1NVADMT77WD~(5WU{D.png)

***安装完成后，启动Apache Web服务器\***

```
systemctl start httpd.service
```

***设置开机自启\***

```
systemctl enable httpd.service
```

![](新建文件夹 (5)\AV8F@63S[C]BV%(1391TLDQ.png)

访问服务器公网IP,出现下图代表Apache安装成功

![](新建文件夹 (5)\DWP{[S%O_J$EEC3J8P`0KN1.png)

#### 2.安装MySQL

***安装MariaDB\***

```
yum install mariadb-server mariadb
```

![](新建文件夹 (5)\MIRO)QDQY{1IZ(NNLCQ1PLO.png)

***启动MariaDB\***

```
systemctl start mariadb
```

***设置MySQL的root密码\***

```
mysql_secure_installation
```

![](新建文件夹 (5)\NR4RDTW1$OW1Y1`(J[ASLMO.png)

初始密码为空，提示输入正确密码，直接回车，再设置密码，其他选择Y













***设置开机自启MariaDB\***

```
systemctl enable mariadb.service
```

![](新建文件夹 (5)\()Z%97PD1VU7RXMKYWM8N~C.png)

#### 3.安装PHP

```
yum install epel-release yum-utils
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```

![](新建文件夹 (5)\@M)J5S2_X_`%{3`OO8%LDI0.png)

![](新建文件夹 (5)\$AF)_%4ZS50JOLY4)G{}525.png)

***因为WordPress需要php5.6以上版本的支持，我们更新到7.2版本仓库\***

```
yum-config-manager --enable remi-php72
```

![](新建文件夹 (5)\`]CSPY32YTA%9Y5)9E[FCQQ.png)

***安装PHP以及php-mysql\***

```
yum install php php-mysql
```

![](新建文件夹 (5)\XVP__M3W41~RIYH`5XXAZ6V.png)

***查看安装的php版本\***

```
php -v
```

![](新建文件夹 (5)\_5C~C8H7J`CC4U~B}_D(S[S.png)

***重启Apache服务器以支持PHP\***

```
systemctl restart httpd.service
```

运行PHP，需要启动PHP附加模块\***

```
yum install php-fpm php-gd
```

![](新建文件夹 (5)\[3Z4{E_RX1Y13MTDFS7U~QG.png)

***重启Apache服务\***

```
service httpd restart
```

![](新建文件夹 (5)\P2%CUH]TZYR7_$LHHQ7(Y{V.png)

#### 4.安装WordPress以及完成相关配置

***登录数据库\***

```
mysql -u root -p
```

***为WordPress创建一个新的数据库\***

```
CREATE DATABASE 数据库名 ;
```

***进入刚创建的数据库\***

```
use 数据库名 ;
```

![](新建文件夹 (5)\`3PUD]OR5R5E433`IQ7EUAV.png)

***为WordPress创建一个独立的MySQL用户并授权给数据库访问权限\***

```
CREATE USER 用户名@localhost IDENTIFIED BY '密码';
GRANT ALL PRIVILEGES ON 数据库名.* TO 用户名@localhost IDENTIFIED BY '密码';
```

![](新建文件夹 (5)\753AHI19OQA1BDV2CMQY7X7.png)

![](新建文件夹 (5)\_K)5K%KS(F(`~J`C5JI03RI.png)

***刷新MySQL的权限\***

```
FLUSH PRIVILEGES;
```

![](新建文件夹 (5)\~M2MRUC@RH%%{M9R0S7I837.png)

***安装WordPress\***

```
tar xzvf latest.tar.gz
```

![](新建文件夹 (5)\D5]4Y$TUI83YKWVDFGT5V0O.png)

![S5MC~Q[$1IP31MC3AH98{`D](新建文件夹 (5)\S5MC~Q[$1IP31MC3AH98{`D.png)

![CD]AZP_1B{S]IF[_8M2T3MN](新建文件夹 (5)\CD]AZP_1B{S]IF[_8M2T3MN.png)

![X[7A8C0IHK3SGN81VB$3JX5](新建文件夹 (5)\X[7A8C0IHK3SGN81VB$3JX5.png)

![R76{$D{TE6L(0`BFQEZ8X6E](新建文件夹 (5)\R76{$D{TE6L(0`BFQEZ8X6E.png)

接下来访问你的服务器公网IP，就能进入WordPress安装的web页

![](新建文件夹 (5)\]B2SSNJ105[%FYY27_@IKT5.png)

![](新建文件夹 (5)\R_Z880Z0N$FIUKGW~`U}VHR.png)



###  4.推送带有wordpress的镜像

***前往[docker hub](https://hub.docker.com/)注册账号，下面需要用到。\***

***将容器生成镜像 (所生成的镜像名由 “Docker用户名/Docker仓库名“组成 ，否则推送会报错： denied: requested access to the resource is denied )\***

```
docker commit -a "Docker用户名" -m "提交描述" 容器id 镜像名:tag标签
```

![](新建文件夹 (5)\U73{}%A1SNXC)PFD[HUM~@7.png)

***登录Docker\***

```
docker login
```

![](新建文件夹 (5)\@P)9N9UK[UG(I}RBNK72PJP.png)

***推送镜像\***

```
docker push 镜像名:tag标签
```

![](新建文件夹 (5)\74EV]6D{VK7X@ECEZZ}G`15.png)

***登录Docker网页查看仓库\***

![](新建文件夹 (5)\IT8)Y7RVJ[[@D]9_`W8KUE.png)

![](新建文件夹 (5)\L[O{KK3XO{]FCM)C5(TA3[R.png)




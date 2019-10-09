- 购买腾讯云服务器 centOS 7.6版本

  [腾讯云学生计划]:( https://cloud.tencent.com/act/campus)

  ![](/tup/QQ图片20191008212101.png)

  安装Git并注册

  [Git]: ( https://git-scm.com/downloads)

  

- 下载PuTTY端实现远程登录云服务器（老师给的教程使用XShell,但是这个免费,性质似乎都一样）

  [PuTTY]: ( https://www.putty.org/)

  ![](/tup/QQ图片20191008213053.png)

  根据腾讯云公网IP地址远程登录
  
  

## SSH key

- ##### 验证是否有ssh key，在Git Bash客户端输入指令

  > ls -al ~/.ssh

如果出现id_rsa和id_rsa.pub文件，则ssh key存在，以下步骤可以跳过。

- ##### 创建新的ssh key

> ssh-keygen -t rsa -b 4096 -C “8348399288@qq.com](mailto:834839928@qq.com)”



复制密钥的内容到GitHub的SSH key中

- ##### 测试SSH Key是否配置成功

  ![](/tup/QQ图片20191008164939.png)

  此时配置成功

  ## 创建GitHub项目并在本地同步

- ##### 新建代码仓库

  

此处不初始化README文档，之后用直接touch。

- ##### 创建本地代码仓库

  ![](\tup\QQ图片20191008170611.png)

新建一个文件夹用于存放代码，右键单击bash here。

复制先前创建的代码仓url。

> git remote add origin https://github.com/sonettofighting/Cloud_Computing.git

> git pull origin master
>
> git touch README.md //由于做本实验的时候已经有这个文件了，在此就用一个test的文本文件替代
>
> git status

> git add . //添加所有modified文件

> git commit -m "sonettofighting"
>
> git push -u origin master

提交指令

![](\tup\QQ图片20191008170548.png)

- ##### 上传成功

  在代码仓查看到刚刚修改的文件

# 安装VMware和CentOS系统

*此处推荐使用VMware workstation player，在非商业用途时免费*

[VMware]: ( https://www.vmware.com/products/workstation-player/workstation-player-evaluation.html)

[CentOS]: ( https://www.centos.org/)

- ##### 创建新的虚拟机

  ![](/tup/QQ图片20191008213043.png)
  
  ![](/tup/QQ图片20191008213039.png)
  
  ![](/tup/QQ图片20191008213001.jpg)
  
  ![](/tup/QQ图片20191008212937.jpg)
  
  ![](/tup/QQ图片20191008212930.png)
  
  ![](/tup/QQ图片20191008212926.png)

语言设置为英语，安装桌面GUI，并设置开启网络，其他选项自行选择。

*有IP地址出现时，说明可以连接网络。*



接下来根据提示，设置root用户、当前用户密码，并同意term信息。

- ##### 成功登录



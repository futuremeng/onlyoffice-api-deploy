

# ![logo](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/favicon.ico)毕升文档云平台安装步骤

[毕升文档](https://ibisheng.cn)| onlyoffice中文 |onlyoffice部署

毕升office api 集成版本能够处理word,ppt,excel格式文件的印预览以及**多人协同编辑**，另外还能处理pdf，视频，音频文件的预览以及实现了100多种文本文件带语法高亮的预览 。详细介绍请参考[**毕升文档产品手册**](https://ibisheng.cn)。下面毕升文档的详细部署说明，如果你喜欢我们欢迎加入毕升文档交流群。

<a target="_blank" href="//shang.qq.com/wpa/qunwpa?idkey=9139c206ed47bb0fdf7e1f5468c447f0e9193354204659b1591477c0f70472da"><img border="0" src="https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/%E6%AF%95%E5%8D%87%E6%96%87%E6%A1%A3%E4%BA%A4%E6%B5%81%E7%BE%A4%E7%BE%A4%E4%BA%8C%E7%BB%B4%E7%A0%81.png" alt="毕升文档交流群" title="毕升文档交流群"></a>

## 硬件要求

安装过程在**centos7**以及**ubuntu 18.04LTS**系统下，硬件配置2核4G以及4核4G服务器均进行过测试。建议使用新安装的系统来安装毕升文档云平台。需要注意的是所有的安装都是root用户执行的。如果您的安装环境不能使用root用户，理论上是不会有问题的，如果碰到权限相关问题请自行搜索资料解决。

## 系统要求

毕升文档安装完成自带nginx，并且配置好全部全部的路径。**请确保你的系统中的80，443端口没有被占用**

## 步骤

1. 从[github](https://github.com/ibisheng/deploy.git)上clone相关的部署脚本到服务器上

   ```shell
   git clone https://github.com/ibisheng/onlyoffice-api-deploy.git
   cd onlyoffice-api-deploy
   ```

   或者你也可以从国内代码托管网站[码云](https://gitee.com/ibisheng) 上clone毕升文档部署脚本到服务器上

   ```
   git clone https://gitee.com/ibisheng/onlyoffice-api-deploy.git
   cd onlyoffice-api-deploy
   ```

2. 安装docker以及docker-compose

   这一步是准备毕升文档运行的系统条件，并不是安装毕升文档。**

   毕升文档云平台所有的服务均是基于docker-compose安装的，在进行下一步安装之前，**请确保你的服务器上已经安装了docker和docker-compose。**你可以使用我们准备的脚本安装,也可以自行参考资料进行安装。

   自行安装Docker 参考链接 ：<https://docs.docker.com/install/>；而docker-compose安装则可以执行如下命令：

   ```shell
   curl -L https://get.daocloud.io/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` \
      -o /usr/local/bin/docker-compose
   chmod +x /usr/local/bin/docker-compose
   systemctl start docker
   systemctl enable docker
   ```

   你也可以选择使用我们提供的脚本安装docker：**如果是你的系统是centos**

   ```shell
   bash preinstall.sh
   ```

   **如果你的系统是ubuntu，**则可以执行：

   ```shell
   bash preinstall-ubuntu.sh
   ```

   

   ![image-20190225144902164](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/docker-version.png)

3. 一键安装毕升文档云平台

   由于一些环境下脚本创建网络会失败，建议在一键安装前建议手动创建docker 网络 bisheng。

   ```shell
   docker network create bisheng
   ```

   如果你的安装脚本是以前下载的，在安装前，请确保是使用的最新脚本，执行git pull 更新最新脚本

   ```shell
   git pull
   ```

   在完成以上步骤之后，可以通过install.sh脚本来安装毕升文档

   ```shell
   bash install.sh /bisheng_data # 请确保/bisheng_data目录没有其他数据
   ```

   注意：** 安装目录的结尾**不要 斜杠 “/”**，否则安装目录最好拼接会出错。**即上面脚本 "/bisheng_data"不要写成“/bisheng_data/”**

   **另外需要强调的是，不要使用有数据的目录作为安装目录，<span style="color: red;">*<u>因为初次安装过程中会清空该目录</u>*</span>**

   该安装命令需要一个参数来指定安装目录，该目录是毕升文档的工作目录，所以的数据都会保存在该目录，需要保证该目录所有在的存储设备上有较大的空间。例如在上面的脚本是我们是使用 /bisheng_data目录作为安装目录

4. 测试

   待上一步骤脚本执行完成之后，先检查所有的docker容易是否全部正常启动。

   ```shell
   docker ps -a
   ```

   ![image-20190402175256521](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/image-20190402175256521.png)

   **其中tools这个容器正常状态是Exit的。**

5. 如何使用

   1. 

   2. 1. 以上安装完成之后，输入地址 http://192.168.2.108 或者http://hostname  即可进入到毕升文档主页面。其中IP，hostname时安装毕升文档的服务器的IP或者主机名，或者指向该服务器的域名

      ![image-20190402181901296](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/image-20190402181901296.png)




## 配置

完成前面5步操作之后，需要申请免费激活系统即可进行正常使用。参考链接：[免费激活](https://ibisheng.cn/apps/blog/posts/license.html)

毕升文档安装默认是自带ngix配置的，其中nginx的配置文件在安装目录下。如果安装安装目录是 /bisheng_data 具体路径则是： /bisheng_data/service/nginx/config/conf.d/bisheng.conf 。

如果你需要配置nginx 的https，则可以将https证书放在/bisheng_data/service/nginx/keys目录下，该目录在docker中的路径是/keys，**配置时路径应该填写docker的路径**

## 集成毕升文档文件服务，实现Office在线预览和编辑

上面的步骤完成之后，你就可以免费使用毕升文档包含drive功能以及在线文件服务功能。另外如果你的文件是存储在邮件附件，ERP，以及其他的各种在线系统，你也可以使用已经部署完成的毕升文档云平台的在线文件服务来来实现Office在线预览和编辑。你所需要做的是实现相关API就可以免费使用毕升在线文件服务。相关API请参考[**毕升文档文件在线服务集成API**](
## 相关问题

1. 如何查找毕升文档的技术文档

   毕升文档的全部技术文档可以去毕升官方博客文章目录：链接：<https://ibisheng.cn/apps/blog/categories/>

   这里可以查阅毕升文档的全部技术文档。

2. 安装完成以后管理员登录的默认用户名和密码是什么？

   管理员默认用户名为： admin ;密码为 bisheng

3. 为什么激活了之后还是重定向到了控制台？

   如果你没有激活，需要激活毕升文档，激活链接：<https://ibisheng.cn/apps/blog/posts/license.html> ；

   如果激活失败，检查是否是网络原因，或者试试离线激活，离线激活链接：<https://ibisheng.cn/apps/blog/posts/license.html#%E6%89%8B%E5%8A%A8%E7%A6%BB%E7%BA%BF%E6%BF%80%E6%B4%BB>

   正确激活完成之后，需要重启所有的结点，在安装脚本的目录下运行 restart.sh脚本

   ```shell
   sh restart.sh
   ```

4. 安装docker过程出错

   ![4407CA1C7C302F19E598F009FC8869FB](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/4407CA1C7C302F19E598F009FC8869FB.jpg)

   这个错误可以参考链接[docker 安装报错 container-selinux >= 2.9 解决](https://blog.csdn.net/qq_41772936/article/details/81080284)

   docker安装出错一般时由于系统层次的原因导致的。请参考相关资料修复。另外为了安装的顺利，建议centos系统使用使用7以上版本。其他linux系统也尽量使用较新版本。

   一般来说，docker环境安装无误之后，毕升文档安装会比较顺利

5. 如何重启所有的服务

   在安装脚本（**步骤1中所下载下载脚**)本所在的目录，有一个脚本 restart.sh。执行该脚本即可重启毕升文档

   ```shell
   sh restart.sh
   ```

   

6. 如何重写安装毕升文档

   执行脚本 reinstall.sh，该脚本将重新安装所有的结点，**但是会保留数据和配置文件**

   ```shell
   sh reinstall.sh
   ```

   

7. 如何升级毕升文档

   执行脚本upgrade.sh，**该脚本会保留所有的数据和配置文件**

   ```shell
   sh upgrade.sh
   ```

8. 执行过程出现错误： Network bushing  declared as external…..  如下图

   ![93D17738F207B6557723390F85D1CAA1](https://public-bisheng.oss-cn-zhangjiakou.aliyuncs.com/resource/93D17738F207B6557723390F85D1CAA1.png)

   这是因为有些服务器上脚本运行 docker create network bisheng 会出错。修复这个问题的方法是手动执行一下这个命令

   ```shell
   docker network create bisheng
   ```

   接下来重新执行安装过程。


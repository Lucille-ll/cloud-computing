# cloud-computing

------------------------------------------------------------------------------------------------------------



### **Docker基础实验**

### **掌握****Docker****基础知识**

------------------------------------------------------------------------------------------------------------

####  Docker的官方网站： 

◼ <https://www.docker.com/> 

####  了解什么是Docker以及相关的概念和安装： 

◼<https://docs.docker.com/engine/docker-overview/>

##### Docker的基本概念 

###### Docker包含了三个基本的概念将在本文中出现：镜像、容器、仓库。

- 镜像（Images）
- 容器（Containers）
- 仓库（Repositories）

#### 镜像

只读的模板，包含可以创建容器的指令，类比于面向对象中的类。

#### 容器

容器是镜像的一个运行实例，类比于面向对象中类的实例对象，如上图中最上层。你可以创建、运行、停止、移动和删除容器。容器的读写并不会写到镜像之中，并且Docker可以很好的隔离多个运行的容器。使用docker ps -a命令可以列出本地所有的容器，包括非活跃的容器。

#### 仓库

仓库是镜像集中存放的地方。你可以把镜像存放与本地，但若想要共享镜像，需要一种镜像分发服务，比如Docker Registry。比较有名的公共Registry服务如Docker官方的Docker Hub，本文后续将使用到。



###  **安装****Docker** 

------------------------------------------------------------------------------------------------------------

####  在CentOS环境下安装Docker，参考： 

◼ <https://blog.csdn.net/llfjfz/article/details/97964215>

#### 先决条件

- 已安装CentOS 7，并且内核版本大等于3.10，本文使用的是阿里云的镜像：[CentOS镜像](http://mirrors.aliyun.com/centos/7/isos/x86_64/)。
- 非root用户已获得sudo特权。

使用如下命令查看操作系统内核信息：

![1](D:\gitrepos\cloudcomputing\images3\1.png)

顺带看一下Linux的版本号：

![2](D:\gitrepos\cloudcomputing\images3\2.png)

可见阿里云镜像保存的是CentOS 7.6。安装Docker

####  安装Docker

CentOS 7的应用程序库可能不是最新的，因此首先更新应用程序数据库：

![3](D:\gitrepos\cloudcomputing\images3\3.png)

注：本文为了命令的通用性，需要root权限的地方都使用sudo。但其实笔者使用root用户，sudo可以省略。

##### 卸载旧版本

较旧的 Docker 版本称为 docker 或 docker-engine 。如果已安装这些程序，请卸载它们以及相关的依赖项。

![4](D:\gitrepos\cloudcomputing\images3\4.png)

##### 安装 Docker Engine-Community

##### 使用 Docker 仓库进行安装

在新主机上首次安装 Docker Engine-Community 之前，需要设置 Docker 仓库。之后，您可以从仓库安装和更新 Docker。

#####  **设置仓库** 

安装所需的软件包。yum-utils 提供了 yum-config-manager  ，并且 device mapper 存储驱动程序需要 device-mapper-persistent-data 和 lvm2。

![5](D:\gitrepos\cloudcomputing\images3\5.png)

使用以下命令来设置稳定的仓库：

![6](D:\gitrepos\cloudcomputing\images3\6.png)

### 安装 Docker Engine-Community

安装最新版本的 Docker Engine-Community 和 containerd，或者转到下一步安装特定版本：

![7](D:\gitrepos\cloudcomputing\images3\7.png)

如果提示您接受 GPG 密钥，请选是。

Docker 安装完默认未启动。并且已经创建好 docker 用户组，但该用户组下没有用户。

**要安装特定版本的 Docker Engine-Community，请在存储库中列出可用版本，然后选择并安装：**

1、列出并排序您存储库中可用的版本。此示例按版本号（从高到低）对结果进行排序。

![8](D:\gitrepos\cloudcomputing\images3\8.png)

2、通过其完整的软件包名称安装特定版本，该软件包名称是软件包名称（docker-ce）加上版本字符串（第二列），从第一个冒号（:）一直到第一个连字符，并用连字符（-）分隔。例如：docker-ce-18.09.1。

![9](D:\gitrepos\cloudcomputing\images3\9.png)

启动 Docker。

![10](D:\gitrepos\cloudcomputing\images3\10.png)

通过运行 hello-world 映像来验证是否正确安装了 Docker Engine-Community 。

![11](D:\gitrepos\cloudcomputing\images3\11.png)

验证Docker是否成功启动：

![12](D:\gitrepos\cloudcomputing\images3\12.png)

最后，确保Docker当服务器启动时自启动：

![13](D:\gitrepos\cloudcomputing\images3\13.png)

此外，还可以查看一下Docker的版本信息：

![14](D:\gitrepos\cloudcomputing\images3\14.png)



### **完成****Docker****安装之后加载****CentOS****镜像** 

------------------------------------------------------------------------------------------------------------

####  熟悉Docker的基本操作 

##### Docker基本操作

###### Docker的命令使用

注意：Docker的操作需要用户获得root权限。

Docker命令的基本格式：

> docker [选项] [命令] [参数]

查看docker所有的命令，键入：

> docker

![38](D:\gitrepos\cloudcomputing\images3\38.png)

特定命令的使用帮助：

> > docker 特定命令 --help

查看当前系统docker的相关信息：

> > docker info
> >
> > ![39](D:\gitrepos\cloudcomputing\images3\39.png)

 因为我是做完后面的实验才做的这个，所以这里面可以看出我有安装过镜像。

####  加载Docker的CentOS镜像（从官方镜像Docker Hub或 

#### 者国内的阿里镜像、daocloud等拉取），参考： 

◼ <https://blog.csdn.net/llfjfz/article/details/98596243>

加载Docker镜像
Docker镜像是容器运行的基础，默认情况下，将从Docker Hub拉取镜像。首先使用search命令查询Docker Hub中的可用镜像，这里以查询可用的CentOS镜像为例：

![15](D:\gitrepos\cloudcomputing\images3\15.png)

命令从Docker Hub拉取centos镜像的相关信息，并返回可用镜像的列表.
接下来拉取官方版本(OFFICIAL)的镜像：

![16](D:\gitrepos\cloudcomputing\images3\16.png)

一旦镜像下载完成，可以基于该镜像运行容器，使用run命令：

![17](D:\gitrepos\cloudcomputing\images3\17.png)

查看一下当前系统中存在的镜像：

![18](D:\gitrepos\cloudcomputing\images3\18.png)



### **在****Docker****的****CentOS****容器实例中安装****WordPress** 

------------------------------------------------------------------------------------------------------------

####  拉取CentOS镜像后运行一个容器实例，参考： 

◼ <https://blog.csdn.net/llfjfz/article/details/98596243> 

##### 运行Docker容器

以上述的CentOS镜像为例运行其容器，使用-it参数进入交互shell模式,并进行container内部shell：

![19](D:\gitrepos\cloudcomputing\images3\19.png)

其中dc802921feb0是容器的ID，后续要用到。你可以在此shell运行任何命令，比如安装Apache Web服务器：

![20](D:\gitrepos\cloudcomputing\images3\20.png)

现在此容器已经安装了Apache Web服务器。注意：所有对于容器的更改只保存在当前运行的容器中，并未写入镜像。

##### 创建新的镜像

在前序操作的基础上，本小节将创建新的镜像，即提交更改到新的镜像。首先从容器的交互shell退出并保存状态，使用exit命令

> exit
>
> 我们首先使用如下命令查看本地中的容器：(参数-a表示列出所有容器，包含活跃的和不活跃的。输出类似下图)

![21](D:\gitrepos\cloudcomputing\images3\21.png)

可以发现刚才运行的ID为dc802921feb0的容器也在列表之中。
现在使用commit命令来提交更改到新的镜像中，即创建新的镜像。命令格式

> docker commit -m “提交的消息” -a “提交人” container-id 仓库名/新的镜像名
>
> ![22](D:\gitrepos\cloudcomputing\images3\22.png)
>
> 这种提交类似于git协议的提交，同样这里提交的镜像只保存在本地。后续可以提交到远程镜像仓库，比如Docker Hub。
> 再次使用镜像查看命令：
>
> ![23](D:\gitrepos\cloudcomputing\images3\23.png)
>
> 可以看到刚才创建的新镜像“test_repository/centos-apache-web”，并且从大小（SIZE）来看，区别于我们原始从Docker Hub拉取的CentOS的官方镜像。
> 接下来要为新建的镜像打上标签（Tag），否则后续推送镜像到Docker Hub的时候将出现“ denied: requested access to the resource is denied”的错误。关于这个错误的解答详见stackoverflow。
> Tag命令的语法：
>
> > docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
> >
> > 进一步细化到推送至Docker Hub的镜像，使用如下格式：
> >
> > > docker tag  SOURCE_IMAGE[:TAG] docker-hub-username/repository-name:TARGET_IMAGE[:TAG]
> > >
> > > 其中hub-username是Docker Hub的用户账户，repository-name为仓库的名称，即上文中的test_respository。
> > > 这里采用如下命令：
> > >
> > > ![24](D:\gitrepos\cloudcomputing\images3\24.png)
> > >
> > > docker-hub-username替换为Docker Hub的实际用户名。这里使用镜像ID来指代想要打标签的镜像。完成之后，同样查看已存在的镜像，如上图。
> > >
> > > 推送镜像到远程镜像仓库
> > > 可以把本地镜像推送到远程镜像仓库，最为著名的就是Docker官方的Docker Hub。当然比如阿里也提供容器仓库，同时也可以自己构建镜像仓库。这里以Docker Hub为例介绍如何实现镜像推送。首先要到Docker Hub上进行注册，然后这里我们使用shell登录：
> > > ![25](D:\gitrepos\cloudcomputing\images3\25.png)
> > >
> > > 输入密码。用户名和密码都正确，随后会显示登录成功。
> > > 使用如下命令推送新创建的镜像：
> > >
> > > > docker push docker-hub-username/docker-image-name
> > > >
> > > > 对于本例为：
> > >
> > > ![26](D:\gitrepos\cloudcomputing\images3\26.png)
> > >
> > > docker-hub-username替换为实际的用户名，这将花费一定的时间，完成之后登陆Docker Hub，查看Repository，可以看到新上传的镜像。
> > >
> > > ![27](D:\gitrepos\cloudcomputing\images3\27.png)

####  在该容器实例中安装WordPress并制作成镜像，参考： 

◼ <https://blog.csdn.net/llfjfz/article/details/95501675>

##### 启动Docker守护进程，即Docker服务：

> sudo systemctl start docker
>
> ##### 安装WordPress
>
> 注意：创建并运行Docker容器（为了方便检测后续wordpress搭建是否成功，需设置端口映射（-p），将容器端口80 映射到主机端口8888，Apache和MySQL需要 systemctl 管理服务启动，需要加上参数 --privileged 来增加权限，并且不能使用默认的bash，要换成 init，否则会提示 Failed to get D-Bus connection: Operation not permitted）
>
> ![56](D:\gitrepos\cloudcomputing\images3\56.png)
>
> 查看容器：
>
> ![57](D:\gitrepos\cloudcomputing\images3\57.png)
>
> 进入容器：
>
> ![58](D:\gitrepos\cloudcomputing\images3\58.png)
>
> 在该容器中安装workpress，参见README-2.md,其中实验截图如下：
>
> ###### 1.使用yum工具安装Apache Web服务器
>
> ![59](D:\gitrepos\cloudcomputing\images3\59.png)
>
> ###### 2.启动Apache Web服务器
>
> ![60](D:\gitrepos\cloudcomputing\images3\60.png)
>
> ###### 3.测试Apache服务器是否成功运行，找到腾讯云实例的公有IP地址(your_cvm_ip)，在你本地主机的浏览器上输入：
>
> ![61](D:\gitrepos\cloudcomputing\images3\61.png)
>
> ###### 4.安装MySQL
>
> ![62](D:\gitrepos\cloudcomputing\images3\62.png)
>
> ![63](D:\gitrepos\cloudcomputing\images3\63.png)
>
> ![64](D:\gitrepos\cloudcomputing\images3\64.png)
>
> ![65](D:\gitrepos\cloudcomputing\images3\65.png)
>
> ###### 5.安装PHP
>
> ![66](D:\gitrepos\cloudcomputing\images3\66.png)
>
> ![67](D:\gitrepos\cloudcomputing\images3\67.png)
>
> ![68](D:\gitrepos\cloudcomputing\images3\68.png)
>
> ![69](D:\gitrepos\cloudcomputing\images3\69.png)
>
> ![70](D:\gitrepos\cloudcomputing\images3\70.png)
>
> ###### 6.安装PHP模块
>
> ![71](D:\gitrepos\cloudcomputing\images3\71.png)
>
> ![72](D:\gitrepos\cloudcomputing\images3\72.png)
>
> ![73](D:\gitrepos\cloudcomputing\images3\73.png)
>
> ![74](D:\gitrepos\cloudcomputing\images3\74.png)
>
> ###### 7.测试PHP
>
> ![75](D:\gitrepos\cloudcomputing\images3\75.png)
>
> 该命令使用vim在/var/www/html/处创建一个空白文件info.php，我们添加如下内容：
>
> ![76](D:\gitrepos\cloudcomputing\images3\76.png)
>
> ###### 8.安装WordPress以及完成相关配置
>
> ###### (1)为WordPress创建一个MySQL数据库
>
> ![77](D:\gitrepos\cloudcomputing\images3\77.png)
>
> ![78](D:\gitrepos\cloudcomputing\images3\78.png)
>
> ###### (2)安装WordPress
>
> 下载
>
> ![79](D:\gitrepos\cloudcomputing\images3\79.png)
>
> ![80](D:\gitrepos\cloudcomputing\images3\80.png)
>
> 解压
>
> ![81](D:\gitrepos\cloudcomputing\images3\81.png)
>
> 移动解压的文件
>
> ![82](D:\gitrepos\cloudcomputing\images3\82.png)
>
> ![83](D:\gitrepos\cloudcomputing\images3\83.png)
>
> 在Apache服务目录下为wordpress创建一个文件夹来保存上传的文件：
>
> ![84](D:\gitrepos\cloudcomputing\images3\84.png)
>
> 对Apache服务器的目录以及wordpress相关文件夹设置访问权限：
>
> ![85](D:\gitrepos\cloudcomputing\images3\85.png)
>
> ###### (3)配置WordPress
>
> ![86](D:\gitrepos\cloudcomputing\images3\86.png)
>
> ![87](D:\gitrepos\cloudcomputing\images3\87.png)
>
> ###### (4)通过Web界面进一步配置WordPress
>
> ![93](D:\gitrepos\cloudcomputing\images3\93.png)
>
> ##### 将安装有wordpress的centos镜像推送到docker hub上面
>
> ![88](D:\gitrepos\cloudcomputing\images3\88.png)
>
> ![89](D:\gitrepos\cloudcomputing\images3\89.png)
>
> ![90](D:\gitrepos\cloudcomputing\images3\90.png)
>
> ![91](D:\gitrepos\cloudcomputing\images3\91.png)
>
> ![92](D:\gitrepos\cloudcomputing\images3\92.png)
>
> #### *下面这个是一开始没理解好题目意思的时候，直接拉取wordpress和mariadb下来创建了一个网站的过程：（以后要安装workpress就可以用这个方法，方便，不用再按README-2.md里面那样繁琐的步骤去安装）*
>
> 首先让我们拉取WordPress的镜像
>
> ![30](D:\gitrepos\cloudcomputing\images3\30.png)

接下来就是创建容器了，首先我们的网站需要记录信息，有账号密码，所以第一个先拉取一个数据库容器，命令如下:

![29](D:\gitrepos\cloudcomputing\images3\29.png)

![33](D:\gitrepos\cloudcomputing\images3\33.png)

现在我们来创建一个word press镜像，并使之与MariaDB镜像互相连接，也就是直接采用数据库镜像的数据库服务

![34](D:\gitrepos\cloudcomputing\images3\34.png)

然后使用docker ps -a命令就可以看到，此时容器已经启动成功，分别是phpmyadmin容器，使用宿主机888端口，数据库容器，使用宿主机3306端口，还有一个lmp容器

![35](D:\gitrepos\cloudcomputing\images3\35.png)

然后不知道为啥–name参数不生效，所以我们再自己手动对该容器重命名

![36](D:\gitrepos\cloudcomputing\images3\36.png)

![48](D:\gitrepos\cloudcomputing\images3\48.png)

这时候我们来浏览器访问服务器地址

![37](D:\gitrepos\cloudcomputing\images3\37.png)

这时候已经可以配置网站信息了点击开始之后，进入下面这个页面

![31](D:\gitrepos\cloudcomputing\images3\31.png)

![32](D:\gitrepos\cloudcomputing\images3\32.png)

这时候我们需要查看MySQL容器的IP地址，以及进入MySQL容器创建一个数据库给wordpress使用

![40](D:\gitrepos\cloudcomputing\images3\40.png)

查询到地址之后，还要创建一个wordpress的数据库，所以我们要进入数据库容器,

进入之后，登录数据库,之后，我们需要创建一个数据库给word press使用：

![41](D:\gitrepos\cloudcomputing\images3\41.png)

然后新建一个数据库用户用于专属使用wordpress，第一个涂抹点就是用户名，第二个就是密码；%代表允许任何主机登陆，可以输入特定的IP：

![42](D:\gitrepos\cloudcomputing\images3\42.png)

创建完成之后给予该用户相关操作权限,下面这个命令就是给该用户对wordpress数据库所有的操作权限

![43](D:\gitrepos\cloudcomputing\images3\43.png)

最后刷新权限

![44](D:\gitrepos\cloudcomputing\images3\44.png)

这时候就可以回到网页那里了，输入刚才那些信息

![56](D:\gitrepos\cloudcomputing\images3\56.jpg)

点击提交之后就可以连接到数据库了

![45](D:\gitrepos\cloudcomputing\images3\45.png)

然后是设置网站信息，设置之后点击安装，提示安装成功

![46](D:\gitrepos\cloudcomputing\images3\46.png)

#### 还可以通过编写dockerfile来安装wordpress

因为这里我没有办法做到只通过一个镜像来安装wordpress,所以就不给出残缺的实验过程，但是看了那么多有关于dockerfile的编写教材知识，有一个写的比较干净利落的贴出来给大家看看：

<https://www.cnblogs.com/lingfengblogs/p/11093246.html>

同时如果在实验过程中有遇到 yum用不了的情况，这里有个解决方法;

<https://blog.csdn.net/xiaohuixing16134/article/details/82728841>

![94](D:\gitrepos\cloudcomputing\images3\94.png)

创建镜像的指令为：

![95](D:\gitrepos\cloudcomputing\images3\95.png)

运行结果：

![96](D:\gitrepos\cloudcomputing\images3\96.png)

查看镜像：

![97](D:\gitrepos\cloudcomputing\images3\97.png)

> 感觉做这个实验，虽然没有把dockerfile部署wordpress完整的做出来，但是，docker的指令，特别是删除镜像或者容器的指令的使用现在已经十分熟悉了。
>
> 有在一直尝试在一个dockerfile里面部署wordpress，不管是centos也好还是ubuntu也好，只能说坑不少，还不好填，技术长也给了我很悉心的帮助，真的十分感恩，但是，我还是没有办法搞出来，但也不是说没做出来就等于没有收获，希望老师之后能出个教程，既然不会就好好学习。

然后这里有个有关于Docker 容器后台运行和前台运行的区别：

<https://zhidao.baidu.com/question/1177563997920000339.html?qbl=relate_question_0&word=dockerfile%C0%EF%C3%E6%B5%C4systemctl>



### **将带有****WordPress****的****CentOS****镜像推送到容器仓库** 

------------------------------------------------------------------------------------------------------------

####  推送CentOS镜像到远程镜像仓库（Docker Hub），参 

#### 考： （步骤同上，这里不再详细描述）

◼ https://blog.csdn.net/llfjfz/article/details/98596243 

![48](D:\gitrepos\cloudcomputing\images3\48.png)

![49](D:\gitrepos\cloudcomputing\images3\49.png)

![50](D:\gitrepos\cloudcomputing\images3\50.png)

![51](D:\gitrepos\cloudcomputing\images3\51.png)

![52](D:\gitrepos\cloudcomputing\images3\52.png)

![53](D:\gitrepos\cloudcomputing\images3\53.png)

![54](D:\gitrepos\cloudcomputing\images3\54.png)

![55](D:\gitrepos\cloudcomputing\images3\55.png)

####  若Docker Hub访问速度较慢，请使用国内其他的 

#### Docker仓库。 
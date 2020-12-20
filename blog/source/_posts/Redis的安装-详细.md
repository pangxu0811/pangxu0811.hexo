---
index_img: /img/title_3.jpg
title: Redis的安装-详细
categories:
- [编程开发,数据库,Redis]
tags:
- 数据库
date: 2019/10/23 20:46:25
comments: true
---

## 第一步：下载redis的安装包，上传至服务器中

#### 1.**获取安装包**方式一：官网地址：https://redis.io/

​	点击下载。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429205002522.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)



#### 2.**获取安装包**方式二：百度网盘链接：https://pan.baidu.com/s/1vKLWzbLQrgtU74YJEtgtCQ 

​       提取码：dkhl 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204639834.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)


#### 3.上传到服务器。（自己练习的话，大家可以自己去装一台虚拟机，我使用的是阿里云的liunx服务器，本质上都是一样的没有什么区别。）

​      我选择上传到：/tmp 目录中。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204701612.png)

## 第二步：解压安装包

#### 1.使用`tar`命令 ：解压安装包， 并重命名为 `redis` 移动至 `/usr/local/redis` 目录下。

```shell
tar -zvxf redis-5.0.8.tar.gz -C /usr/local/redis
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204726109.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)

#### 2.目录之后:使用4个CPU进行`make`。(因为我的服务器是4核，没有4核也没关系)

- ​	输入命令：

```shell
make -j 4
```

- ​       等待编译

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204745837.png)



- 这样显示，则是编译完成

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204828502.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)


#### 3.然后使用`make install`命令。

######        作用：将编译完成后的可执行文件，添加到系统目录中，然后就可以正常访问了。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204930230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)


#### 4.编辑redis.conf。

###### 	虽然现在可以启动redis服务了，使用`redis-server`命令。但是在启动服务之前，需要我们指定一个配置文件。

- ​      我们先查看一下当前目录下的文件，会发现系统给我们自动生成了一个叫 `redis.conf` 的文件。


![在这里插入图片描述](https://img-blog.csdnimg.cn/202004292048066.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)


- ​      我们再查看一下这个文件。

```
vi  ./redis.conf
```

- ​       进去之后我们首先就看到了这些，后面还有很多，这个配置文件很长：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204603607.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)

######       关于这个redis.conf这个配置文件，如果是想要学习redis的，那就一定要通读一遍。现在也有很多redis的讲解视频，大家有兴趣的话也可以去看一看，这里就不做赘述了。

#### 		**那么针对redis的安装，我可以给大家讲一下，我们现在需要用到哪几个参数。**

##### 1）第一个参数：“`bind`” （绑定参数）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429205200524.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)

###### 		这个参数的意思是说，允许哪一个ip来访问redis的服务器，它的默认是`127.0.0.1`也就是说只能本机访问，我们把它给改一下。问什么要改：是因为我的redis服务器部署在远程服务器上，并不在本机。如果说redis服务器是在虚拟机上的，同样也需要更改的。其实最重要的原因还是项目是分布式的，肯定需要多台机器访问的。

-    所以修改bind参数为：`bind 0.0.0.0`


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429205223277.png)


##### 2）第二个参数：“`daemonize`”

######      文件内容很长，直接手动翻页找很费时间，vi提供了快速定位的方法，我们直接按`“/” 在输入“daemonize”`, 就可以找到这个参数了。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204540625.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)


- ​     这个参数的意思是允许后台运行。默认为`yes`，所以我们不需要更改，认识就好。


##### 3）第三个参数：”`protected-mode`“。

- ​    `redis3.2`版本后新增`protected-mode`配置，默认是`yes`，即开启。我们是设置外部网络连接redis服务，所以我们不仅需要修改`bind`参数，还需要关闭`protected-mode`模式，此时外部网络可以直接访问。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204501417.png)


##### 4）最后一个参数： ”`requirepass` “

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204441229.png)


- ​     这个参数是给redis服务器设置密码，redis服务器默认是没有密码的，所以我们需要手动添加一下。如下我添加的密码就是`123`。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204421955.png)


##### 5）我们可以尝试用`redis-server` 命令来启动redis服务器了，同时指定一下配置文件。

```shell
redis-server ./redis.conf
```

- ​        OK， 看到如下图这个输出，那就说明成功了！服务器已经运行起来了。![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204359421.png)



- ​        我们可以选择再查看一下是否真的已经启动成功了！输入：


```shell
  ps -ef | grep redis
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204334389.png)


-    可以看到进程号了 说明redis服务确实启动成功了！


##### 6)安装上面的步骤，已经启动好了服务器，那么我们接下来就是来访问redis服务器了。

- ​	执行`*redis-cli*` 命令。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204310998.png)


- 可以看到，通过直接输入`redis-cli`命令，进入到了与服务器的交互模式。


​	说到`redis-cli`，补充如下：

> *redis-cli*是Redis命令行接口，一个允许从终端向Redis服务器发送命令和从服务器读取响应的简单程序。
>
> 它有两种主要使用的模式：一是交互模式，即在一窗口内用户键入命令，服务器应答的模式；另一种则是将*redis-cli*作为一个程序，命令做为其参数，执行，最后以标准输出打印。
>
> 在交互模式下，*redis-cli*提供基本的行编辑能力以提高输入体验。
>
> 然而*redis-cli*不仅仅如此，还可以使用一些*options*启动程序进入特定的模式，以便*redis-cli*可以做一些更复杂的任务，比如模拟一个分支并且打印从主干接收到的复制流、检测一个Redis服务器的延迟并且显示满意度或者基至是延迟的样本和频率的图谱，还有许多其他一些事情。
>
> 如果你将要广泛Redis或者已经在使了，那么你将碰到许多使用*redis-cli*的机会。所以花费一些时间熟悉它还是很不错的，你会发现一旦你知道了所有的命令行使用决窍，你的工作效率将更高效。

######     关于redis-cli的第二种模式，大家感兴趣的可以去看看其他更多的一些博客，都有详 解，这里就不多赘述了。

#### 5.那么在交互模式下如何来操作呢？redis作为一个缓存系统，无非也就是`set,get`之类的操作。大家可以移步到大佬博客，都有更为复杂且详细的演示操作。这里我就给初学者演示一下简单的`set value`和`get value`。

- ​	之前我们设置过redis服务器的密码，那么在命令行模式需要进行操作时，我们也就先需要输入密码。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204239468.png)


- ​    然后继续操作。


- ​    我们使用"`set`"命令，设置一个`Key: key1, Value:123`。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429204206257.png)

-   使用“`get`”命令，通过`Key` 来获取 `Value`。![](https://img-blog.csdnimg.cn/20200429204122434.png)



-    进行了前面两个命令的操作，细心的朋友会发现，你在输入一个命令的时候，可以看到它会自动在后面提示可以匹配的格式，这就是redis的一个很人性化的地方：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203915753.png)


#### 6.  操作完之后，我们学习下如何关闭redis服务器：

- ​    在交互模式下输入：`shutdown sava` 。保存并且退出，当然后面也有提示，显示“`NOSAVE|SAVA`",我们也可以 `shutdown nosava` 。不包存且退出。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203839367.png)


 

-   关闭服务器，断开了链接，我们就可以退出交互模式：`exit`


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203756860.png)


-  我们可以再检验下：输入


```
  ps -ef | grep redis
```

-    可以看到进程已经关闭了！

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203704811.png)


#### 7.到了这一步为止，我们的redis服务器就已经安装好了。但是呢一般这种服务呢，我们都会把它做成一个系统服务。那么我们如何将它做成系统服务呢？这里，redis就做的相当人性化了，它就给我们提供了这样一个工具。

-  我们去到 `utils/` 目录下


```shell
 cd ./utils/
```

- 可以看到有一个 `install_server.sh`的执行文件，它就是来帮助我们做这个事的。


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203452506.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQyMTY2OTIz,size_16,color_FFFFFF,t_70)


- 我们执行一下这个文件：


```Shell
./install_server.sh
```

- 然后它会让他们选择一个默认端口为[6379]，这里我们直接回车就行了。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203423121.png)


- 接下来它让我们选择redis的配置文件：


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203357960.png)


- 那么这里我们的redis配置文件就不是这个[`/etc/redis/6379.conf`]了。我们手动填写一下：`/usr/local/redis.conf` 。回车![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203243715.png)



- 然后它还要选择redis的日志文件：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203148878.png)


- 同样我们手动修改一下：`/usr/local/redis.log`。回车


![](https://img-blog.csdnimg.cn/20200429203107322.png)


-   我们都放在同一个目录下的好处是方便我们以后进行查阅，管理。

  接下来它问我要选择一个数据文件。同样我们还是放在相同目录，手动修改一下：


`/usr/local/redis/data`。回车

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429203030997.png)


- 最后它还需要我们选择一个启动路径，这个我们之前就用的就是这个启动路径了，所以不需要修改，直接回车。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429202958581.png)


- 继续回车！

  可以看到我们已经将redis修改为系统服务了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429202916557.png)
- 那么我们验证一下，输入：


```
chkconfig --list | grep redis
```

![](https://img-blog.csdnimg.cn/20200429202615430.png)


- 很成功，可以发现 `redis_6379`的系统服务。

  既然已经有了`redis_6379`的系统服务了，那么redis的启动方式就可以使用：


`systemctl  start redis_6379` 命令来启动了。关闭命令为：`systemctl  stop redis_6379`

#### 8.那么现在为止我们的redis就已经完全安装好了。

​        如果我们觉得`redis_6379`这个名太丑了，想修改一下服务名。
我们可以去系统文件中修改这个服务的文件: `vi /etc/inin.d/redis_6379`。
其实所谓系统服务也不过是系统的一些可执行文件，这里就不做赘述了。希望以上内容能帮助到大家！


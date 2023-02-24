

# 监控代理

监控代理是UCloud自主研发并开源的辅助agent程序，在云主机或物理云主机中安装监控代理，能够让资源与云平台监控系统更好的协同工作，以扩展对资源的监控深度，丰富监控指标（如内存、磁盘空间、进程等）。



## 1.版本说明

| 更新时间   | Agent版本 | 更新内容说明                                                 | 备注 |
| ---------- | --------- | ------------------------------------------------------------ | ---- |
| 2022.12.07 | v1.2.1    | 新增 uma采集支持多磁盘分区使用率监控                                       |      |
| 2022.09.05 | v1.2.0    | 优化 uma采集内存使用率的逻辑                                             |      |
| 2022.08.15 | v1.1.9    | 新增 物理机多磁盘监控功能                                                |      |
| 2022.07.30 | v1.1.8    | 新增 uma安装后即可自启动                                                |      |
| 2022.01.25 | v1.1.7    | 新增 加入物理云主机内存ECC报错数、磁盘异常(ro)个数，支持centos和ubuntu操作系统 |      |
| 2021.03.08 | v1.1.6    | 新增 支持裸金属2.0版本                                       |      |
| 2018.01.03 | v1.1.4    | 修复 可能产生僵尸进程的bug                                   |      |
| 2017.10.31 | v1.1.3    | 新增 支持物理云采集GPU温度                                   |      |
| 2017.05.15 | v1.1.2    | 优化 Agent采集方式                                           |      |
| 2017.03.07 | v1.1.1    | 新增 加入物理云主机磁盘健康状态检查（0表示正常，1表示异常），支持centos和ubuntu操作系统 |      |
| 2016.11.01 | v1.1.0    | 1、新增 支持内网上报&支持内网下载Agent（**Windows版本更新**）。2、优化 WIndows版本不再需要配置公私钥，安装后启动即生效 |      |
| 2016.05.19 | v1.0.5    | 1、优化 Linux版本支持内网上报功能，uma不再需要外网上报数据。2、支持自动配置，不在需要手动配置 |      |
| 2016.03.25 | v1.0.2    | 1、修复 Windows版本上报阻塞bug。2、优化 Linux版本tcp连接数采集 |      |
| 2016.01.07 | v1.0.1    | 修复 磁盘名称过长导致采集数据错误的bug                       |      |
| 2015.10.29 | v1.0.0    | 1、优化 新版使用C和Python混合编写，无需安装nodejs等依赖库文件。2、优化 简化配置并能够将配置复用，避免了拷贝配置无法供其他主机使用的问题。3、修复 内存泄露问题。4、优化 支持自动更新。5、新增 支持windows操作系统的监控代理 |      |

> **注释**：
> 1、如需使用Linux内网数据上报版本，请重新安装agent；umagent已支持物理云主机，如安装后启动报错，请根据报错信息解决依赖关系。
> 2、监控代理只支持4.8以下内核版本，使用内核4.8以上和UMA配合使用，可能出现部分指标无法获取的情况





## 2.监控代理安装准备工作

- 安装过程需要使用系统管理员用户(如root, administrator等)。
- 安装过程需要在UCloud云主机的内网环境下进行。





## 3.Red Hat/CentOS 全系列

### 3.1.1 python2版本uma安装

64位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.2.1-1.x86_64.rpm
rpm -ivh uma-1.2.1-1.x86_64.rpm
```

32位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.2.1-1.i386.rpm
rpm -ivh uma-1.2.1-1.i386.rpm
```

### 3.1.2 python3版本uma安装 

64位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-py3-1.1.5-1.x86_64.rpm
rpm -ivh uma-py3-1.1.5-1.x86_64.rpm
```



### 3.2 启动

```
service uma start
```



### 3.3 停止

```
service uma stop
```



### 3.4.1 python2版本uma卸载

```
rpm -e uma
```

### 3.4.2 python3版本uma卸载

```
rpm -e uma-py3
```





## 4. Ubuntu/Debian 全系列

### 4.1.1 python2版本uma安装

64位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma_1.2.1-1_amd64.deb
dpkg -i uma_1.2.1-1_amd64.deb
```

32位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma_1.2.1-1_i386.deb
dpkg -i uma_1.2.1-1_i386.deb

```

### 4.1.2 python3版本uma安装

64位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-py3_1.1.5-1_amd64.deb
dpkg -i uma-py3_1.1.5-1_amd64.deb
```



### 4.2 启动

```
service uma start
```



### 4.3 停止

```
service uma stop
```



### 4.4.1 python2版本uma卸载

```
dpkg -P uma
```

### 4.4.2 python3版本uma卸载


```
dpkg -P uma-py3
```






## 5.OpenSUSE系列

### 5.1 安装

64位操作系统:

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.2.1-1.suse.x86_64.rpm
rpm -ivh uma-1.2.1-1.suse.x86_64.rpm
```



### 5.2 启动

```
service uma start
```



### 5.3 停止

```
service uma stop
```



### 5.4 卸载

```
rpm -e uma
```





## 6.其他版本Linux系统

### 6.1 安装

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.2.1-1.tar.gz
tar zxvf uma-1.2.1-1.tar.gz
cd uma
make && make install
```



### 6.2 启动

```
/usr/sbin/uma 或 ./bin/uma
```



### 6.3 停止

```
源代码编译版本，需要手动执行kill终结进程。
```



### 6.4 卸载

```
进入源代码安装包，执行 make uninstall 卸载程序。

```



### 6.5 自动启动

在 /etc/rc.local中添加以下内容

```
/usr/sbin/uma
```



## 7.Windows操作系统

本安装示例基于Windows2008操作系统。

> 注解：Windows系统暂不支持CPU负载与TCP连接数监控指标，暂不支持物理云





### 7.1 安装

将以下链接复制到浏览器中，下载win-uma监控代理。 下载链接:
<http://umon.api.service.ucloud.cn/static/uma-win/uagent-1.1.1-setup.rar>

双击应用程序，选择安装语言为简体中文，点击确定继续;

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma01.png)

在安装界面点击下一步，进入安装配置选项;

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma02.png)

选择需要安装的位置，这里使用默认的安装位置 “C:\\Program Files (x86)\\uagent”;

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma03.png)

配置开始菜单文件夹，点击下一步继续;

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma04.png)

以上配置完成后，点击安装以完成监控代理的安装。

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma05.png)

### 7.2 启动

打开开始菜单，在运行中输入cmd开启命令行终端;

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma11.png)

在命令行终端中输入以下命令启动监控代理;

```
sc start uagent
```

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma12.png)

输入以下命令查看监控代理是否启动成功，如启动成功，则STATE会显示为Running。

```
sc query uagent
```

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma13.png)



### 7.3 卸载

点击开始菜单，选择卸载uagent;

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma14.png)

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma15.png)

```
注解：卸载完成后，需要进入目录删除剩余文件。如卸载失败，请按照以下流程进行手动卸载。
```

打开命令行终端，输入以下命令停止监控代理服务;

```
sc stop uagent
```

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma16.png)

输入以下命令卸载uagent服务;

![](D:/MyCloud/GitHub/umon%20-%20%E5%89%AF%E6%9C%AC/images/win-uma17.png)

最后，删除uagent安装目录，即可完成卸载。



### 7.4 配置

windows uagent默认使用ip为10.x.x.x的网卡识别主机，若用户主机使用了子网特性后，可能会出现多张网卡，或者网卡ip非10.x.x.x的情况，该情况可能导致主机识别失败，对于此种情况，可以在配置文件uagent安装目录下：configure/static\_conf.json中添加配置macAddress解决(mac地址可在ipconfig
-all中获取，选择原始ip所对应的mac地址)，如：

```
{
    "dataHost":"http://umon.api.service.ucloud.cn",
    "macAddress":"xx:xx:xx:xx:xx:xx"
}
```





## 8.物理云磁盘状态监控的安装

当前agent版本已加入物理云主机磁盘健康状态检查的指标。该指标只返回0和1，0表示磁盘健康，否则返回1

安装依赖关系：依赖关系： 1. smartmontools 2. MegaCli64 3. dmidecode 4. hpssacli

### 8.1 CentOS操作系统

在/etc/yum.repos.d/新建kernel.repo文件并加入以下内容：

```
[kernel]
name=kernel Repository
baseurl=http://ucloud.mirror.ucloud.cn/centos/$version/$basearch
gpgcheck=0
enabled=1
```

其中对CentOS 6.X，$version = 6;CentOS 7.X，$version = 7. 系统会自动识别$basearch
安装依赖软件：

```
yum clean all
yum makecache
yum install smartmontools dmidecode MegaCli hpssacli
```



### 8.2 Ubuntu操作系统

在/etc/apt/sources.list添加以下内容：

```
deb http://ucloud.mirrors.ucloud.cn/ubuntu/ucloud ubuntu-ucloud main

```

更新软件源：

```
apt-get update

```

安装依赖软件:

```
sudo apt-get install smartmontools dmidecode megacli hpssacli

```





## 9.软件源安装下载过慢的解决方法

1.建议开启timestamp来解决过慢问题。确认timestamp是否开启的方法：

```
cat /proc/sys/net/ipv4/tcp_timestamps

```

检查是否返回1

2.通过手动下载依赖包安装

rpm包下载链接（暂仅支持登录主机后下载）

<http://ucloud.mirror.ucloud.cn/centos/6/x86_64/Packages/MegaCli-8.07.14-1.noarch.rpm>
<http://ucloud.mirror.ucloud.cn/centos/6/x86_64/Packages/hpssacli-2.0-23.0.x86_64.rpm>
<http://mirrors.ucloud.cn/centos/6/os/x86_64/Packages/smartmontools-5.43-1.el6.x86_64.rpm>
<http://mirrors.ucloud.cn/centos/6/os/x86_64/Packages/mailx-12.4-8.el6_6.x86_64.rpm>
<http://mirrors.ucloud.cn/centos/6/os/x86_64/Packages/dmidecode-2.12-7.el6.x86_64.rpm>

deb下载链接（暂仅支持登录主机后下载）

<http://ucloud.mirrors.ucloud.cn/ubuntu/ucloud/pool/main/m/megacli/megacli_8.07.10-2_all.deb>
<http://ucloud.mirrors.ucloud.cn/ubuntu/ucloud/pool/main/h/hpssacli/hpssacli_2.0-24_amd64.deb>

{{indexmenu_n>30}}

# 监控代理

监控代理是UCloud自主研发并开源的辅助agent程序，在云主机或物理云主机中安装监控代理，能够让资源与云平台监控系统更好的协同工作，以扩展对资源的监控深度，丰富监控指标（如内存、磁盘空间、进程等）。

## 1.版本说明

> 注解 如需使用Linux内网数据上报版本，请重新安装agent。

> 注解 本次更新后，umagent已支持物理云主机。如安装后启动报错，请根据报错信息解决依赖关系。

    当前版本：v1.1.4
    最后更新时间：2018年01月03日

    2018年01月03日版本更新说明:
      1. 修复可能产生僵尸进程的bug

    2017年10月31日版本更新说明:
      1. 支持物理云采集GPU温度

    2017年5月16日版本更新说明:
      1. 优化采集方式

``` 
2017年3月7日 版本更新说明：
  1.加入物理云主机磁盘健康状态检查（0表示正常，1表示异常）。限制条件：目前只支持centos和ubuntu两个操作系统 
```

    2016年11月1日 版本更新说明：
      1.Windows版本更新，支持内网上报，并且支持内网下载Agent
      2.WIndows版本不再需要配置公私钥，安装后启动即可生效

    2016年5月19日 版本更新说明：
      1.Linux版本支持内网上报功能，uma不再需要外网上报数据
      2.支持自动配置，不在需要手动配置

    2016年3月25日 版本更新说明：
      1. Windows修复上报阻塞的bug
      2. Linux优化tcp连接数采集

    2016年1月7日 版本更新说明：  
      1. 修复了一个磁盘名称过长导致采集数据错误的bug

    2015年10月29日 版本更新说明：
      1. 新版使用C和Python混合编写，无需安装nodejs等依赖库文件
      2. 简化配置并能够将配置复用，避免了拷贝配置无法供其他主机使用的问题。
      3. 修复内存泄露问题
      4. 支持自动更新
      5. 新增windows操作系统的监控代理

## 2.监控代理安装基本需求

1\. 安装过程需要使用系统管理员用户(如root, administrator等)。 2.
Linux或ubuntu系统需要安装**Python2.6或Python2.7版本**（暂不支持Python3.x版本）。

## 3.Red Hat 6.0+/7.0+/CentOS 6.0+/7.0+

### 1.安装

64位操作系统：

    wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.1.4-1.x86_64.rpm
    rpm -ivh uma-1.1.4-1.x86_64.rpm

32位操作系统：

    wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.1.4-1.i386.rpm
    rpm -ivh uma-1.1.4-1.i386.rpm

### 2.启动

    service uma start

### 3.停止

    service uma stop

### 4.卸载

    rpm -e uma

## 4.Ubuntu/Debian 全系列

### 1.安装

64位操作系统：

    wget http://umon.api.service.ucloud.cn/static/umatest/uma_1.1.4-1_amd64.deb
    dpkg -i uma_1.1.4-1_amd64.deb

32位操作系统：

``` 
wget http://umon.api.service.ucloud.cn/static/umatest/uma_1.1.4-1_i386.deb
dpkg -i uma_1.1.4-1_i386.deb

```

### 2.启动

    service uma start

### 3.停止

    service uma stop

### 4.卸载

    dpkg -P uma

## 5.OpenSUSE系列

### 1.安装

64位操作系统:

    wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.1.4-1.suse.x86_64.rpm
    rpm -ivh uma-1.1.4-1.suse.x86_64.rpm

### 2.启动

    service uma start

### 3.停止

    service uma stop

### 4.卸载

    rpm -e uma

## 6.其他版本Linux系统

### 1.安装

    wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.1.4-1.tar.gz
    tar zxvf uma-1.1.4-1.tar.gz
    cd uma
    make && make install

### 2.启动

    /usr/sbin/uma 或 ./bin/uma

### 3.停止

    源代码编译版本，需要手动执行kill终结进程。

### 4.卸载

``` 
进入源代码安装包，执行 make uninstall 卸载程序。

```

### 5.自动启动

在 /etc/rc.local中添加以下内容

    /usr/sbin/uma

## 7.Windows操作系统

本安装示例基于Windows2008操作系统。

    注解：Windows系统暂不支持CPU负载与TCP连接数监控指标。

### 1.安装

将以下链接复制到浏览器中，下载win-uma监控代理。 下载链接:
<http://umon.api.service.ucloud.cn/static/uma-win/uagent-1.1.1-setup.rar>

双击应用程序，选择安装语言为简体中文，点击确定继续;

![](/images/win-uma01.png)

在安装界面点击下一步，进入安装配置选项;

![](/images/win-uma02.png)

选择需要安装的位置，这里使用默认的安装位置 “C:\\Program Files (x86)\\uagent”;

![](/images/win-uma03.png)

配置开始菜单文件夹，点击下一步继续;

![](/images/win-uma04.png)

以上配置完成后，点击安装以完成监控代理的安装。

![](/images/win-uma05.png)

### 2.启动

打开开始菜单，在运行中输入cmd开启命令行终端;

![](/images/win-uma11.png)

在命令行终端中输入以下命令启动监控代理;

    sc start uagent

![](/images/win-uma12.png)

输入以下命令查看监控代理是否启动成功，如启动成功，则STATE会显示为Running。

    sc query uagent

![](/images/win-uma13.png)

### 3.卸载

点击开始菜单，选择卸载uagent;

![](/images/win-uma14.png)

![](/images/win-uma15.png)

    注解：卸载完成后，需要进入目录删除剩余文件。如卸载失败，请按照以下流程进行手动卸载。

打开命令行终端，输入以下命令停止监控代理服务;

    sc stop uagent

![](/images/win-uma16.png)

输入以下命令卸载uagent服务;

![](/images/win-uma17.png)

最后，删除uagent安装目录，即可完成卸载。

### 4.配置

windows
uagent默认使用ip为10.x.x.x的网卡识别主机，若用户主机使用了子网特性后，可能会出现多张网卡，或者网卡ip非10.x.x.x的情况，该情况可能导致主机识别失败，对于此种情况，可以在配置文件uagent安装目录下：configure/static\_conf.json中添加配置macAddress解决(mac地址可在ipconfig
-all中获取，选择原始ip所对应的mac地址)，如：

    {
        "dataHost":"http://umon.api.service.ucloud.cn",
        "macAddress":"xx:xx:xx:xx:xx:xx"
    }

## 8.物理云磁盘状态监控的安装

1.1.1版的agent加入物理云主机磁盘健康状态检查的指标。该指标只返回0和1，0表示磁盘健康，否则返回1

安装依赖关系：依赖关系： 1. smartmontools 2. MegaCli64 3. dmidecode 4. hpssacli

### 1.CentOS操作系统

在/etc/yum.repos.d/新建kernel.repo文件并加入以下内容：

    [kernel]
    name=kernel Repository
    baseurl=http://ucloud.mirror.ucloud.cn/centos/$version/$basearch
    gpgcheck=0
    enabled=1

其中对CentOS 6.X，$version = 6;CentOS 7.X，$version = 7. 系统会自动识别$basearch
安装依赖软件：

    yum clean all
    yum makecache
    yum install smartmontools dmidecode MegaCli hpssacli

### 2.Ubuntu操作系统

在/etc/apt/sources.list添加以下内容：

    deb http://ucloud.mirrors.ucloud.cn/ubuntu/ucloud ubuntu-ucloud main

更新软件源：

    apt-get update

安装依赖软件:

    sudo apt-get install smartmontools dmidecode megacli hpssacli

## 9.软件源安装下载过慢的解决方法

1.建议开启timestamp来解决过慢问题。确认timestamp是否开启的方法：

    cat /proc/sys/net/ipv4/tcp_timestamps

检查是否返回1

2.通过手动下载依赖包安装

rpm包下载链接

<http://ucloud.mirror.ucloud.cn/centos/6/x86_64/Packages/MegaCli-8.07.14-1.noarch.rpm>
<http://ucloud.mirror.ucloud.cn/centos/6/x86_64/Packages/hpssacli-2.0-23.0.x86_64.rpm>
<http://mirrors.ucloud.cn/centos/6/os/x86_64/Packages/smartmontools-5.43-1.el6.x86_64.rpm>
<http://mirrors.ucloud.cn/centos/6/os/x86_64/Packages/mailx-12.4-8.el6_6.x86_64.rpm>
<http://mirrors.ucloud.cn/centos/6/os/x86_64/Packages/dmidecode-2.12-7.el6.x86_64.rpm>

deb下载链接

<http://ucloud.mirrors.ucloud.cn/ubuntu/ucloud/pool/main/m/megacli/megacli_8.07.10-2_all.deb>
<http://ucloud.mirrors.ucloud.cn/ubuntu/ucloud/pool/main/h/hpssacli/hpssacli_2.0-24_amd64.deb>



# 监控代理

监控代理是UCloud自主研发并开源的辅助agent程序，在云主机或物理云主机中安装监控代理，能够让资源与云平台监控系统更好的协同工作，以扩展对资源的监控深度，丰富监控指标（如内存、磁盘空间、进程等）。



## 1.版本说明

| 更新时间   | Agent版本 | 更新内容说明                                                 | 备注 |
| ---------- | --------- | ------------------------------------------------------------ | ---- |
| 2023.08.15 | v1.2.3    | 新增 支持适配Rocky 9.1 64位、Ubuntu 22.04 64位、Ubuntu 20.04 64位、Ubuntu 18.04 64位、高内核Ubuntu 18.04 64位镜像                             |     |
| 2023.06.20 | v1.2.2    | 新增 在python3上支持物理云主机/dev/nvme监控                               |     |
| 2022.12.07 | v1.2.1    | 新增 uma采集支持多磁盘分区使用率监控                                       |    |
| 2022.09.05 | v1.2.0    | 优化 uma采集内存使用率的逻辑                                             |   |
| 2022.08.15 | v1.1.9    | 新增 物理机多磁盘监控功能                                                |     |
| 2022.07.30 | v1.1.8    | 新增 uma安装后即可自启动                                                |     |
| 2022.01.25 | v1.1.7    | 新增 加入物理云主机内存ECC报错数、磁盘异常(ro)个数，支持centos和ubuntu操作系统 |内存ECC报错数仅在python2上支持该功能|
| 2021.03.08 | v1.1.6    | 新增 支持裸金属2.0版本                                       |       |
| 2019.08.12 | v1.1.5    | 修复 内核版本高于4.18时无法使用问题                          |      |
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

> **注释**：
> 根据当前系统默认python版本，安装py2或者py3版本的uma安装包，如若安装失败可尝试安装另一版本。



### 3.1.1 python2版本uma安装

64位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.2.3-1.x86_64.rpm
rpm -ivh uma-1.2.3-1.x86_64.rpm
```

32位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-1.2.3-1.i386.rpm
rpm -ivh uma-1.2.3-1.i386.rpm
```

### 3.1.2 python3版本uma安装 

64位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-py3-1.2.3-1.x86_64.rpm
rpm -ivh uma-py3-1.2.3-1.x86_64.rpm
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

> **注释**：
> 根据当前系统默认python版本，安装py2或者py3版本的uma安装包，如若安装失败可尝试安装另一版本。


### 4.1.1 python2版本uma安装

64位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma_1.2.3-1_amd64.deb
dpkg -i uma_1.2.3-1_amd64.deb
```

32位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma_1.2.3-1_i386.deb
dpkg -i uma_1.2.3-1_i386.deb

```

### 4.1.2 python3版本uma安装

64位操作系统：

```
wget http://umon.api.service.ucloud.cn/static/umatest/uma-py3_1.2.3-1_amd64.deb
dpkg -i uma-py3_1.2.3-1_amd64.deb
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






## 5.物理云磁盘状态监控的依赖包

当前agent版本已加入物理云主机磁盘健康状态检查的指标。该指标只返回0和1，0表示磁盘健康，否则返回1

安装依赖关系：依赖关系： 1. smartmontools 2. MegaCli64 3. dmidecode 4. hpssacli



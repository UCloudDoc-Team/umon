{{indexmenu_n>5}}

# 回调接口

## 定义

将公网可访问到的http服务地址作为回调地址，当触发告警时，监控中心会将告警推送到该地址。

创建webhook后您的系统可以收到UCloud告警信息。当有告警时，UCloud的系统会将告警信息以HTTP
POST方式发送到指定URL，您可以对收到信息进行处理。



## 条件

用户需要提供接收POST请求的HTTP服务，以处理UCloud发送的POST请求，并将该服务的URL注册到UCloud的告警系统中。



## JSON Body Example

#### 告警

``` json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    Region: " cn-north-03",
    ResourceType: "uhost",
    ResourceId: "uhost-xxxx",
    MetricName: "MemUsage",
    AlarmTime: 1458733318,
    RecoveryTime : 0
}
```

#### 恢复

``` json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    Region: "cn-north-03",
    ResourceType: "uhost",
    ResourceId: "uhost-xxxx",
    MetricName: "MemUsage",
    AlarmTime: 0,
    RecoveryTime: 1458733318
}
```

#### Field Explaination

| Field        | Explaination                    |
| ------------ | ------------------------------- |
| SessionID    | Session ID for this message     |
| Region       | Region Name                     |
| ResourceType | Resource Type                   |
| MetricName   | Metric Name for current warning |
| AlarmTime    | Alarm time                      |
| RecoveryTime | Restory time                    |
| Content      | Warning content                 |

**Response**

我们这边需要收到这样的response， 表明用户成功接收推送信息，否则会再重试2次：

``` json
{
    SessionID: "xxxxxxxxxxxxxxxxxxxxxxx",
    RetCode: 0
}
```



## WebHookServer Demo 编译、安装

本Demo提供实现支持WebHook服务的一种方式，基于Golang实现，使用MySQL存储收到的报警数据，Demo仅供参考。
下面以UHost及UDB为例介绍如何使用该Demo。

**依赖外部环境**

根据UCloud相关操作说明创建系统为CentOS的UHost

    弹性IP: 106.75.49.79 BGP 2 Mb
    外网防火墙: Web服器推荐(22，3389，80，443)



#### 准备工作

##### 1.安装数据库

```
# yum install mysql mysql-server -y
# service mysqld start
# chkconfig mysqld on
```

创建名为monitor\_warn的数据库，并使用以下表结构

``` mysql
# mysql
# CREATE DATABASE `monitor_warn`;
# USE monitor_warn
# CREATE TABLE IF NOT EXISTS `warn_message` (
    `session_id` char(36) NOT NULL,
    `region` varchar(20) NOT NULL,
    `resource_type` varchar(45) NOT NULL,
    `resource_id` varchar(45) NOT NULL,
    `metric_name` varchar(50) NOT NULL,
    `alarm_time` int(11) DEFAULT NULL,
    `recovery_time` int(11) DEFAULT '0',
    PRIMARY KEY (`session_id`)
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



##### 2.配置Golang编译环境

```
# yum install golang -y
# mkdir /usr/local/golang
```

修改\~/.bashrc，添加如下内容:

```
export GOPATH=/usr/local/golang
export PATH=$PATH:$GOPATH/bin
```

加载已配置环境变量

```
# source ~/.bashrc
```

查看已配置go环境变量

```
# go env
GOARCH="amd64"
GOBIN=""
GOEXE=""
GOHOSTARCH="amd64"
GOHOSTOS="linux"
GOOS="linux"
GOPATH="/usr/local/golang"
GORACE=""
GOROOT="/usr/lib/golang"
GOTOOLDIR="/usr/lib/golang/pkg/tool/linux_amd64"
GO15VENDOREXPERIMENT=""
CC="gcc"
GOGCCFLAGS="-fPIC -m64 -pthread -fmessage-length=0"
CXX="g++"
CGO_ENABLED="1"
```



##### 3.安装Golang第三方依赖包

```
# yum install git -y
# go get github.com/gorilla/mux
# go get github.com/google/uuid
# go get github.com/go-sql-driver/mysql
```



#### 部署代码

1.从github上将代码拷贝下载到本地

```
# git clone https://github.com/ucloud/umon_webhook.git
```

2.在目录umon\_webhook中创建名为src指向webhook-demo-go的软链接

```
# cd umon_webhook
# ln -s $PWD/webhook-demo-go src
```

3.将目录umon\_webhook添加到GOPATH中

```
# export GOPATH=$GOPATH:$PWD
```

4.在目录webhook-demo-go中编译

```
# cd webhook-demo-go
# go build -a .
```



#### 配置

1\. 根据数据库表相关信息，修改webhook-demo-go/etc/conf.ini

``` json
{
    "api-port": 80,
    "mysql-user": "root",
    "mysql-passwd": "",
    "mysql-db": "monitor_warn",
    "mysql-host": "127.0.0.1",
    "mysql-port": 3306
}
```

2.执行编译生成的可执行程序webhook-demo-go，默认加载etc/conf.ini文件，也可以指定其他位置配置文件

```
# ./webhook-demo-go &
2016/08/10 16:58:25 Welcome to ucloud monitor webhook demo ...
2016/08/10 16:58:25 Monitor webhook demo use 2 process cores
2016/08/10 16:58:25 Start monitor warn webhook server ...
2016/08/10 16:58:25 Webhook Server listen on : :80
```

> 注解 webhook-demo-go 可使用-c参数指定配置文件路径



## 客户端说明

用于测试添加报警信息，实际数据以接口实际返回为准，具体操作如下：

```
# cd umon_webhook
# go build ./webhook-client.go
# ./webhook-client -u http://$IP/add
Post request for webhook:  0
{"SessionID":"07a89fb8-5ee0-11e6-b059-00ffbeabee13","Region":"cn-north-03","Reso
urceType":"uhost","ResourceId":"uhost-xxxx","MetricName":"MemUsage","AlarmTime":
1470822697,"RecoveryTime":0}
......
```

> 注解 $IP为外网IP地址



## 资源路径及接口

1.访问$IP地址，默认端口为80

![](/images/guide/webhook0.png)

2.访问/add，添加报警信息，即实际WebHook调用接口

3.访问/get，获取当前已经添加的报警信息

![](/images/guide/webhook1.png)

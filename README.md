# Alertmanager

## 1. 简述

该项目是在官方主分支`8d050da`基础上进行二次定制开发的，主要为适应我们使用K8S部署时配置文件无法自动重载的问题。



## 2. 编译安装

```shell
$ mkdir -p $GOPATH/src/github.com/prometheus
$ cd $GOPATH/src/github.com/prometheus
$ git clone https://github.com/prometheus/alertmanager.git
$ cd alertmanager
$ make build
$ ./alertmanager --config.file=<your_file>
```

您还可以通过将名称传递给build函数来仅构建此仓库中的二进制文件之一：

```shell
make build BINARIES=alertmanager
```



## 3. 新增功能-配置文件监听重载

使用`--monitor`参数指明开启文件监听

其他信息请参见[官方README](https://github.com/jwping/alertmanager/blob/master/AREADME.md)

## 4. 修改说明

```shell
cmd/alertmanager/main.go

// L42引入fsnotify包
fsnotify "gopkg.in/fsnotify/fsnotify.v1"

// L187新增配置文件变动监听项开关
monitorConfig   = kingpin.Flag("monitor", "Monitor profile changes.").Default("false").Bool()

// L503定义错误缓冲chan
monitorChan = make(chan error)

// L509增加配置文件监听器逻辑
// 详见源码

// L585配置文件监听器error chan捕获
case <-monitorChan:
	return 1
	
// 新增主程序配置文件模板、邮件以及微信告警模板（短信告警模板在iflytek_sms程序内，无template）
```

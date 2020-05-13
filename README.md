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
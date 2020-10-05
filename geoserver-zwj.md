# GeoServer Notes 

安装文档：http://geoserver.org/download/
		配置文档：https://docs.geoserver.org/latest/en/user/                                                                                                                                                                                                                 		支持平台：Debian家族 | RHEL家族 | Windows | Kubernetes |Docker                                                                                                                                                      		任务提交者：wenjian

## 介绍

Geoserver是一个功能齐全，遵循OGC开放标准的开源WFS-T和WMS服务器，利用 GeoServer 可以方便的发布地图数据，允许用户对特征数据进行更新、删除、插入操作，通过 GeoServer 可以比较容易的在用户之间迅速共享空间地理信息。

## 环境要求

* 程序语言：Java 
* 应用服务器：自带
* 数据库：无
* 依赖组件：java8或Java11
* 服务器配置：不低于1核1G

## 安装说明

下面基于不同的安装平台，分别进行安装说明。

### CentOS

```shell
# 下载安装包
wget https://nchc.dl.sourceforge.net/project/geoserver/GeoServer/2.18.0/geoserver-2.18.0-bin.zip

# 安装
yum -y install java-1.8.0-openjdk
unzip /root/geoserver-2.18.0-bin.zip -d /usr/share/geoserver
echo "export GEOSERVER_HOME=/usr/share/geoserver" >> /etc/profile 
. /etc/profile
```

### Ubuntu

```shell
# 下载安装包
wget https://nchc.dl.sourceforge.net/project/geoserver/GeoServer/2.18.0/geoserver-2.18.0-bin.zip
宿主机在https://www.oracle.com/cn/java/technologies/javase/javase-jdk8-downloads.html下载jdk-8u261-linux-x64.tar.gz，然后传到虚拟机/root目录下

# 安装
mkdir /usr/java
tar -zxf /root/jdk-8u261-linux-x64.tar.gz -C /usr/java
unzip /root/geoserver-2.18.0-bin.zip -d /usr/share/geoserver
cat >> /etc/profile <<EOF
JAVA_HOME=/usr/java/jdk1.8.0_261
JRE_HOME=/usr/java/jdk1.8.0_261/jre
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH 
export GEOSERVER_HOME=/usr/share/geoserver
EOF
. /etc/profile
```

## 配置说明

安装完成后，需要依次完成如下配置方可使用

### 基本配置

```shell
cd /usr/share/geoserver/bin
sh startup.sh &
```

## 使用说明

### 路径

* 程序路径：/usr/share/geoserver/bin/
* 日志路径：/var/log/geoserver.log 
* 配置文件路径：/usr/share/geoserver/etc/

### 账号密码

* 用户名： `admin`
* 密码： `geoserver`


### 版本号

通过如下的途径获取版本号: 

```shell
在网络浏览器中，导航到http://公网ip:8080/geoserver即可看到版本号
```

### 端口号

本项目需要开启的端口号：

| item | port       |
| ---- | ---------- |
| Java | 8079、8080 |

## 常见问题

#### 有没有管理控制？

访问http://公网ip:8080/geoserver登录即可

#### 有没有CLI工具？

无

## 日志

* 2020-10-02 完成CentOS和Ubuntu安装研究

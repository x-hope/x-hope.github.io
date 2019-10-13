---
title: Linux上java项目部署
layout: post
categories: 编程
tags: Linux
excerpt: 完整版markdown语法
---

# Linux上java项目部署

## linux安装java

### 下载地址

http://www.oracle.com/technetwork/java/javase/downloads/index.html

### 解压缩

先把jdk的压缩文件解压出来

`tar -zxvf 文件名`

### 创建目录

`mkdir  /usr/local/java`

### 移动安装包

`mv    jdk1.8 /     /usr/local/java/`

自己所有手动装的软件，都必须放在usr/local文件夹下面

也可以以先移动在解压

###  配置文件变量

配置系统环境变量

1. `vi /etc/environment`

2. 添加如下语句

```text
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"
export JAVA_HOME=/usr/local/java/jdk1.8.0_152
export JRE_HOME=/usr/local/java/jdk1.8.0_152/jre
export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
```

修改jdk文件版本就行

配置用户环境变量

`vi  /etc/profile `

jre1.8.0_221

```reStructuredText
if [ "$PS1" ]; then
  if [ "$BASH" ] && [ "$BASH" != "/bin/sh" ]; then
    # The file bash.bashrc already sets the default PS1.
    # PS1='\h:\w\$ '
    if [ -f /etc/bash.bashrc ]; then
      . /etc/bash.bashrc
    fi
  else
    if [ "`id -u`" -eq 0 ]; then
      PS1='# '
    else
      PS1='$ '
    fi
  fi
fi

export JAVA_HOME=/usr/local/java/jdk1.8.0_152
export JRE_HOME=/usr/local/java/jdk1.8.0_152/jre
export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH:$HOME/bin

if [ -d /etc/profile.d ]; then
  for i in /etc/profile.d/*.sh; do
    if [ -r $i ]; then
      . $i
    fi
  done
  unset i
fi
```

放在中间位置

### 使用户环境变量生效

`source /etc/profile`

### 测试是否安装成功

```text
java -version
```





## linux安装tomcat

### 下载地址

https://tomcat.apache.org/

### 解压缩

### 移动解压后的目录

`mv tomcat/   /usr/local/`

### 目录内启动

./startupp.sh



## linux安装MySQL

### 更新数据源

`apt-get update`

### 安装MySQL

`apt-get install mysql-server`

然后会提示设置密码

安装成功后，whereis  mysql找到安装地址

### 配置远程访问

1. 修改配置文件 `vi /etc/mysql/mysql.conf.d/mysqld.cnf`

2. ```text
   bind-address = 127.0.0.1  修改为0.0.0.0 为全部可访问
   ```

3. 重启MySQL        service mysql restart

4. 登录MySQL         mysql -u root   -p

5.  授权 grant all privileges on *.* to 'root'@'%' identified by '你的 mysql root 账户密码';



### 常用命令

停止 `serivce mysql stop`

重启  `serivce mysql restart`

启动  `serivce mysql start`


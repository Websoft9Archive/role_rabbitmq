# RabbitMQ Notes

组件名称：RabbitMQ-Server  
安装文档：https://www.rabbitmq.com/download.html  
配置文档：https://www.rabbitmq.com/admin-guide.html  
支持平台： Debian家族 | RHEL家族 | Windows | Kubernetes | Docker  

责任人：helin  


## 概要

RabbitMQ是一款开源的MQ系统

## 环境要求

* 程序语言：Java 
* 应用服务器：自带
* 数据库：无
* 依赖组件：Erlang

## 安装说明

下面基于不同的安装方式，分别进行安装说明。

### CentOS

官方提供了erlang和rabbitmq-server的仓库，且官方建议使用其自身提供的仓库，不建议使用操作系统自带的仓库或其他第三方仓库。

```shell
# 分别安装erlang源和rabbitmq-server源
curl -s https://packagecloud.io/install/repositories/rabbitmq/erlang/script.rpm.sh | sudo bash
curl -s https://packagecloud.io/install/repositories/rabbitmq/rabbitmq-server/script.rpm.sh | sudo bash

# 安装
yum install erlang rabbitmq-server -y
```

### Ubuntu

官方提供了erlang和rabbitmq-server的仓库，且官方建议使用其自身提供的仓库，不建议使用操作系统自带的仓库或其他第三方仓库。

需要注意的是：RabbitMQ官方没有提供packagecloud上的erlang仓库，而是 Install Erlang from an Apt Repostory on Bintray

```yaml
- name: add a key used to sign RabbitMQ
  apt_key:
    url: https://github.com/rabbitmq/signing-keys/releases/download/2.0/rabbitmq-release-signing-key.asc

- name: add the apt repository
  apt_repository:
    repo: "{{item}}"
    state: present
    filename: bintray.rabbitmq
  with_items:
    - deb https://dl.bintray.com/rabbitmq-erlang/debian bionic erlang
    - deb https://dl.bintray.com/rabbitmq/debian bionic main

- name: Install RabbitMQ
  apt:
    name: rabbitmq-server
```

## 配置

安装完成后，需要依次完成如下配置

```shell
# Set RabbitMQ
- name: Restart RabbitMQ
  shell: systemctl start rabbitmq-server

- name: Enable the management console of RabbitMQ
  shell: rabbitmq-plugins enable rabbitmq_management

- name: Create administrator for RabbitMQ console
  shell: |
    rabbitmqctl add_user admin admin
    rabbitmqctl set_user_tags admin administrator
```


## 服务

本项目安装后自动生成：rabbitmq-server 服务

## 常见问题

#### 有没有管理控制台？

*http:// 公网 IP:15672* 即可访问控制台，系统默认存在一个无法通过外网访问的guest/guest账号

#### 本项目需要开启哪些端口？

| item      | port  |
| --------- | ----- |
| lustering | 25672 |
| AMQP      | 5672  |
| http      | 15672 |

#### 前置条件erlang的版本可能不满足RabbitMQ的安装要求导致无法安装

错误信息：failed to start RabbitMQ broker  
解决方案：/var/lib/rabbitmq/mnesia 目录下存在rabbit@localhost.pid、rabbit@localhost、rabbit@localhost-plugins-expand，删除这3项后，再使用systemctl start rabbitmq-server启动

#### 增加新用户后无法登录?

解决方案：新增用户，并赋予管理员权限

```shell
rabbitmqctl add_user admin admin      #新增一个用户
rabbitmqctl set_user_tags admin administrator #授予管理员
```

#### 前置条件erlang是必要的吗？

是的

#### 如何获取RabbitMQ版本？
```shell
sudo rabbitmqctl status | grep RabbitMQ*
```

## 日志
* 2020-04-14 完成CentOS安装研究

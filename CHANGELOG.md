# CHANGELOG

## Bug Fixes

* 2020-06-02  optimize init password 
* 2020-05-07  通过给role_init中增加 rabbitmqctl delete_user admin 然后再创建用户，解决AWS,Azure基于镜像开机后admin不存在的问题

## Features

* 2020-04-17  修成改官方的脚本处理apt/yum源问题，输出版本号
* 2020-03-27  改写项目，测试成功（包含随机密码）

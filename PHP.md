# PHP(Personal Home Page)

## 一、PHP介绍

### 1、PHP 功能介绍

- 开发周期短，效率高，入门简单
- web服务器的开发语言，用来实现用户的请求
- 开源软件，所有操作系统稳定执行
- 实现面向过程(上学)，面向对象(洗车的过程)
- 支持的主流数据库：MySQL、Oracle等

### 2、开发环境

#### 1）WAMP

​		Windows + Apache + MySQL + PHP

#### 2）LAMP

​		Linux + Apache + MySQL + PHP



## 二、Web基本概念

### 1、Apache

- Apache 是一种服务器软件。
- 下载安装
- 系统环境变量配置

> 服务管理器的打开方式：win + r 打开运行窗口，在其中输入services.msc

### 2、MySQL安装

- 测试安装成功命令：在安装目录下cmd，然后输入 `mysql -uroot -p` ，然后输入自己的MySQL密码，登录成功出现如下：

  ```haskell
  Microsoft Windows [版本 10.0.17134.765]
  (c) 2018 Microsoft Corporation。保留所有权利。
  
  D:\wamp\MySQL5.5\bin>mysql -uroot -p
  Enter password: ****
  Welcome to the MySQL monitor.  Commands end with ; or \g.
  Your MySQL connection id is 3
  Server version: 5.5.28 MySQL Community Server (GPL)
  
  Copyright (c) 2000, 2012, Oracle and/or its affiliates. All rights reserved.
  
  Oracle is a registered trademark of Oracle Corporation and/or its
  affiliates. Other names may be trademarks of their respective
  owners.
  
  Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
  
  mysql>
  ```

  mysql命令的运行环境是cmd窗口，格式为： `mysql -uroot -p` ，示例如上代码所示。

### 3、PHP的安装

- 部署：PHP就是一个软件包，不需要安装，只需要在Apache启动的过程中来加载PHP功能模块即可。

- Apache加载PHP：默认Apache仅能处理HTML文件的请求。如果想让Apache支持PHP文件的请求，必须加载PHP这个功能模块。

  - 加载PHP功能模块：

    ```
    httpd.conf文件中：
    
    #加载PHP功能模块
    LoadModule php7_module 'd:/wamp/php7.3/php7apache2_4.dll'
    
    #配置PHP文件的扩展名
    AddType Application/x-httpd-php .php
    
    #设置PHP的配置文件
    PHPIniDIR 'd:/wamp/php7.3/php.ini'
    ```

    > php.ini-development：开发阶段的配置文件的模板文件
    >
    > php.ini-production：上线阶段的配置文件的模板文件
    >
    > 将php.ini-development更改为php.ini即可（复制一份）

- 测试：








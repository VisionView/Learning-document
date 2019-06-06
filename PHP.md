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

### 1、Apache安装

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
  
  

## 三、主机的配置（Apache）

### 1、httpd.conf文件详解

httpd.conf是Apache的主配置文件

- ServerRoot "D:/wamp/Apache2.4"：Apache的安装位置。

- Listen 80：Apache的监听端口号

- ServerAdmin XXX@XX.com：用于设置管理员邮箱

- ServerName localhost:80    ：域名设置和端口号

- DocumentRoot "D:/wamp/Apache2.4/htdocs"：用于设置文档(或站点)的根目录

  > 说明：DocumentRoot是与ServerName 对应的，当外部通过域名来访问Apache服务器时，Apache会到这个域名对应的DocumentRoot指定的目录中找文件，找到就返回，找不到就报错。

- Directory配置段，有开始结束

  主要用于对站点根目录的特性的设置，配置格式如下：

  ```conf
  <Directory "D:/wamp/Apache2.4/htdocs">
  
  	# [1]
      Directoryindex index.html
      
      # Possible values for the Options directive are "None", "All",
      # or any combination of:
      #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
      #
      # Note that "MultiViews" must be named *explicitly* --- "Options All"
      # doesn't give it to you.
      #
      # The Options directive is both complicated and important.  Please see
      # http://httpd.apache.org/docs/2.4/mod/core.html#options
      # for more information.
      #
      
      # [2]
      Options Indexes FollowSymLinks
      # Options Indexes FollowSymLinks
      #
      # AllowOverride controls what directives may be placed in .htaccess files.
      # It can be "All", "None", or any combination of the keywords:
      #   AllowOverride FileInfo AuthConfig Limit
      #
      # [3]
      # AllowOverride None
  	# [4]
  	# Order  deny,allow
      #
      # Controls who can get stuff from this server.
      #
      # [5]
      Require all granted
  </Directory>
  ```

  > 说明：
  >
  > - Directoryindex：用于设置默认首页，当仅指定了域名，没有指定具体的文本时，Apache会将此项设置的文件返回给用户。
  > - Options Indexes  是否列出目录结构，当请求的文件不存在时会将站点的目录结构显示出来。提示：怎么关掉：注释掉那句话。在开发阶段，要么运行列出目录结构，要么设置默认首页。
  > - AllowOverride None或All  ：用于配置是否开启外部配置文件
  > - Order 配置项 ：用于配置此目录的访问权限，①：Order  deny,allow：如果没有明确的拒绝，则全部允许。deny from IP地址或all。②：Order  allow,deny：如果没有明确的允许，则全部拒绝。allow from IP地址或all
  > - Require all granted：控制所有的请求都需要授权认证。

### 2、主机的配置

业务场景：httpd.conf文件

​			域名：www.php9.com

​			站点根目录：D:\wamp\php9

​			默认首页：index.html

​			允许列出目录结构

​			不允许110.110.110.110这个IP访问，其他的都允许。

```
# httpd.conf文件
# 配置域名
ServerName www.php9.com
# 配置域名对用的站点根目录
DocumentRoot "D:\wamp\php9"

# 在<Directory "D:/wamp/php9">中
# 配置默认首页
DirectoryIndex index.html
# 或者 index.php home.html home.php
# 允许列出目录结构
Options Indexes FollowSymLinks
# 是否开启外部配置文件
AllowOverride None
# 配置访问权限
Order deny,allow
deny from 110.110.110.110
allow from all
```

> 在host文件中配置域名与IP地址的对应关系
>
> 在C:\Windows\System32\drivers\etc下的hosts文件中

### 3、httpd.exe的作用

httpd.exe位于bin目录中。作用：

- Apache服务的维护。httpd.exe文件可以进行Apache服务的启动、停止、重新启动。语法：

  httpd.exe  -k  stop      停止Apache服务

  httpd.exe  -k  start      启动Apache服务

  httpd.exe  -k   restart  重启Apache服务

  > 注意： 如果提示错误，请用管理员方式打开

  







## 四、PHP的安装

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








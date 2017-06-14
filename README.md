# rails 在线实验环境

## 软件简介

Rails是一个运行在Ruby编程语言上的开源Web应用程序框架。它是一个完整的堆栈框架。这意味着“开箱即用”，Rails可以创建从Web服务器收集信息，谈话或查询数据库以及呈现模板的页面和应用程序。因此，Rails具有独立于Web服务器的路由系统

所属类别是web开发

License: MIT License

特点：

1.全栈式的MVC框架

2.约定优于配置

3.更少的代码

4.生成器

5.零周转时间

6.支架系统

7.指导原则

## 软件官网

https://en.wikipedia.org/wiki/Ruby_on_Rails

## Dockerfile 使用方法

### 如何使用
Dockerfile在您的Rails应用程序项目中创建
```
FROM rails:onbuild
```
将此文件放在您的应用程序的根目录旁边Gemfile。

该图像包括多个ONBUILD触发器，应覆盖大多数应用程序。构建将COPY . /usr/src/app，，RUN bundle install和EXPOSE 3000，并设置默认命令rails server。

然后，您可以构建并运行Docker映像：
```
$ docker build -t my-rails-app .
$ docker run --name some-rails-app -d my-rails-app
```
您可以通过访问http://container-ip:3000浏览器进行测试，或者如果您需要在主机之外访问，请在端口8080上进行测试：
```
$ docker run --name some-rails-app -p 8080:3000 -d my-rails-app
```
然后，您可以访问http://localhost:8080或http://host-ip:8080浏览器。

### 生成一个 Gemfile.lock
该onbuild标签需要Gemfile.lock在您的应用程序目录中。这docker run将帮助您生成一个。在您的应用程序的根目录中运行它，旁边是Gemfile：
```
$ docker run --rm -v "$PWD":/usr/src/app -w /usr/src/app ruby:2.1 bundle install
```
### 引导一个新的Rails应用程序
如果要为新的Rails项目生成脚手架，可以执行以下操作：
```
$ docker run -it --rm --user "$(id -u):$(id -g)" -v "$PWD":/usr/src/app -w /usr/src/app rails rails new --skip-bundle webapp
```
这将创建一个名为webapp当前目录中的子目录。

## 资源链接

- https://en.wikipedia.org/wiki/Ruby_on_Rails
- https://github.com/rails/rails#license

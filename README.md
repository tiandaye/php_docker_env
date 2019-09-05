**参考**

https://github.com/goozp/zPhal-dockerfiles

# 搭建php开发环境

## 使用搭建好的环境

- 首先，进入项目dockerfiles的目录下，这里是files目录：

```
cd php_docker_env/files

wget https://pecl.php.net/get/redis-3.1.6.tgz -O php/pkg/redis.tgz
wget https://codeload.github.com/phalcon/cphalcon/tar.gz/v3.3.1 -O php/pkg/cphalcon.tar.gz
```

然后下载我们会用到的PHP拓展包。

- 执行命令：

```
docker-compose up
```

docker会自动通过编写好的docker-compose.yml内容构建镜像，并且启动容器。
如果没问题，下次启动时可以以守护模式启用，所有容器将后台运行：

```
docker-compose up -d
```


- 关闭容器

```
docker-compose down
```

## 问题

**Docker LNMP搭建报错 Depends: zlib1g-dev but it is not going to be installed or libz-dev**

following packages have unmet dependencies:
 libfreetype6-dev : Depends: zlib1g-dev but it is not going to be installed or libz-dev
 libpng12-dev : Depends: zlib1g-dev but it is not going to be installed

**解决方案：使用中科大源**

deb http://mirrors.ustc.edu.cn/debian stable main contrib non-free 
deb-src http://mirrors.ustc.edu.cn/debian stable main contrib non-free 
deb http://mirrors.ustc.edu.cn/debian stable-proposed-updates main contrib non-free 
deb-src http://mirrors.ustc.edu.cn/debian stable-proposed-updates main contrib non-free


## 使用 Composer

当我们要使用composer时怎么做呢？ 我们已经在php\-fpm里安装了composer。

用 docker\-compose 进行操作：

```
docker-compose run --rm -w /data/www/tian php-fpm composer update
```

`-w /data/www/tian`为在php\-fpm的工作区域，tian项目也是挂载在里面，所有我们可以直接在容器里运行composer。

或者进入宿主机app目录下用docker命令：

```
cd php_docker_env/app

docker run -it --rm -v `pwd`:/data/www/ -w /data/www/tian files_php-fpm composer update

```

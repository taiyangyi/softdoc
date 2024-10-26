# Git 工具安装

`Git` 是一个免费开源的分布式版本控制系统，是开发人员必不可缺少的工具之一，其广泛应用于软件开发及其他行业需要版本控制的领域。

**官方文档**：https://git-scm.com/

## 1、Linux

在 Linux 系统中安装 `Git` 可以通过多种方式来实现，主要是包管理器安装和源代码编译安装。

### 1.1 CentOS

#### 方式一：通过包管理器安装

```
# CentOS 7及以下
yum install git

# CentOS 8 及以上
dnf install git
```

#### 方式二：通过源码编译安装

如果需要安装特定版本或者自定义配置，推荐使用源码编译安装。

**1、准备 Git 安装包**

- [Git 官网]("https://git-scm.com/downloads/linux") 或者 [其他站点]("https://www.kernel.org/pub/software/scm/git/") 下载 Git 源代码包
- 使用 wget 命令直接从命令行下载源码包

Git 官网，版本根据个人喜好选择，下载安装包，这里选择的是 2.39.5 版本，将下载好的安装包上传至 `Linux` 服务器的 `root` 目录下，然后将其解压得到 `git-2.39.5`目录，或者进入服务器使用 `wget` 命令通过链接直接下载，这里的 请将 * 替换为具体的版本号。

```
# 使用 wget
wget https://www.kernel.org/pub/software/scm/git/git-*.tar.gz

wget https://www.kernel.org/pub/software/scm/git/git-2.39.5.tar.gz
```

解压下载的源码包：

```
tar -zxvf git-2.39.5.tar.gz
```

**2、提前安装编译依赖k**

使用包管理器安装编译 Git 所需的依赖项。具体依赖项可能因 Linux 发行版而异，但通常包括 `curl`、`expat`、`gettext`、`openssl`、`zlib` 等库的开发文件以及 `gcc` 编译器。

```
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel libcurl-devel autoconf perl-ExtUtils-MakeMaker gcc
```

**3、编译安装 Git**

进入解压后的 Git 源代码目录中，执⾏配置、编译、安装命令即可，如下所示：

```

[root@iZbp1d8rn0652ia3bzzmioZ ~]# cd git-2.39.5/
[root@iZbp1d8rn0652ia3bzzmioZ git-2.39.5]# pwd
/root/git-2.39.5
[root@iZbp1d8rn0652ia3bzzmioZ git-2.39.5]# make configure
    GEN configure
[root@iZbp1d8rn0652ia3bzzmioZ git-2.39.5]# ./configure --prefix=/usr/local/git
...
...
...
[root@iZbp1d8rn0652ia3bzzmioZ git-2.39.5]# make install
...
...
...


```

> **备注：**

```
In file included from /usr/include/curl/curl.h:2251:0,
                 from git-curl-compat.h:3,
                 from http.c:4:
http.c: 在函数‘set_proxyauth_name_password’中:
http.c:655:28: 错误：‘CURLOPT_PROXYHEADER’未声明(在此函数内第一次使用)
   curl_easy_setopt(result, CURLOPT_PROXYHEADER,
                            ^
http.c:655:28: 附注：每个未声明的标识符在其出现的函数内只报告一次

# --prefix=/root/git-2.39.5 这里是解压后安装包的目录
# 执行
whereis curl; ./configure --prefix=/root/git-2.39.5 --with-curl=/usr/bin/curl; make; make install;
```


**4、将 Git 加入环境变量**

编辑 `/etc/profile` 文件或用户的 `~/.bashrc` 文件，添加 Git 的安装目录到 PATH 环境变量中：

```
vim /etc/profile

底部加入 Git 的 bin 路径配置
export GIT_HOME=/usr/local/git
export PATH=$PATH:$GIT_HOME/bin

```

执行，source 使其环境变量生效。

```
source /etc/profile
```

**5、查看安装是否成功**

执行 `git --version` 查看安装是否成功

```
[root@iZbp1d8rn0652ia3bzzmioZ git-2.39.5]# git --version
git version 1.8.3.1

```

#### 卸载

```
yum remove git
```






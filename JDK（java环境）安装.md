# Linux/CentOS

## JDK 介绍

JDK(Java Development Kit) 是 Java 语言的软件开发工具包；

SE(JavaSE)，standard edition，标准版，是我们通常用的一个版本，从JDK 5.0开始，改名为Java SE；

EE(JavaEE)，enterprise edition，企业版，使用这种JDK开发J2EE应用程序，从JDK 5.0开始，改名为Java EE。从2018年2月26日开始，J2EE改名为Jakarta EE；

ME(J2ME)，micro edition，主要用于移动设备、嵌入式设备上的java应用程序，从JDK 5.0开始，改名为Java ME；

## JDK 安装包

[官网下载]("https://www.oracle.com/java/technologies/downloads/archive/") 选择我们需要安装的 JDK 版本，这里以jdk8为例，下载 Linux 版本，并将其安装包放到 root 目录下。

关于 Oracle 账户，方便下载，这里我引用了 [账户详情]("https://www.jianshu.com/p/14f37bcd807c")

```
# 提醒：为了大伙的方便，请不要随便用该邮箱重新注册Oracle账号！
账号：yawoniu@163.com
密码：Oracle.123
```

## 卸载已有的 OpenJDK

如果系统自带有 OpenJDK，可以按照如下步骤提前卸载掉。

```
rpm -qa|grep java
```

如果存在，将其 java 开头的安装包均卸载掉即可：

```
yum -y remove java-*

...省略...
```

## 创建目录并解压

1、在 `/usr/local/` 下创建 `java` 文件夹。

```
cd /usr/local
mkdir java
cd javva
```

2、将 `root` 目录下的 JDk 安装包解压到 `/usr/local/java` 目录下，解压完之后，`/usr/local/java` 目录下会出现一个 `jdk1.8.0_421` 的目录。

```
tar -zxvf /root/jdk-8u421-linux-x64.tar.gz -C /usr/local/java/
```

## 配置 JDK 环境变量

编辑 `/etc/profile` 文件，在文件底部位置加入 JDk 的安装目录到 PATH 环境变量中：

```
vim /etc/profile

JAVA_HOME=/usr/local/java/jdk1.8.0_421
CLASSPATH=$JAVA_HOME/lib/
PATH=$PATH:$JAVA_HOME/bin
export PATH JAVA_HOME CLASSPATH
```

然后执行，source 使其环境变量生效。

```
source /etc/profile
```

## 验证 JDK 安装结果

```
java -version

java version "1.8.0_421"

输出版本信息，表明成功；
```






# 在Mac OS系统上搭建开发环境

本节主要介绍如何搭建一个基于Mac OS系统的Zehpyr开发环境。

在完成本节的所有步骤之后，你能够在以下版本的Mac OS系统上编译和运行自己的Zephyr应用：

* Mac OS X 10.11 (El Capitan)


## 更新你的操作系统统

在开始搭建开发环境前，确保你的操作系统已经被更新。

## 安装必须的软件和依赖软件

为了在Mac OS系统上安装构建Zephyr内核所需的软件工具，你需要构建目标设备所需的交叉编译器，同时还要安装开发系统所需的工具。

> 注意：对于以下列举的所需软件包，最小版本号的不同并不会映像软件的使用。

> 特别注意：在安装下列软件包前，请建超你的防火墙和代理配置来确认英特网访问是可以的。

首先，安装Homebre（The missing package manager for OS X）。Homebrew是一个自由并且开源的软件包管理系统，它的目的在于简化在苹果的Mac OS X操作系统上安装软件的过程。

安装Homebrew，访问[Homebrew主页](http://brew.sh/)，按照页面上的说明进行安装。

为了完成Homebrew的安装，你可能会被要求安装某些缺失的依赖软件。如果遇到缺失的依赖软件，根据提供的安装说明进行安装。

当Homebrew成功安装后，使用命令行安装如下的工具：

```
$ brew install gettext qemu help2man mpfr gmp coreutils wget
$ brew tap homebrew/dupes
$ brew install grep --default-names
```

```
$ brew install crosstool-ng
```

你可以选择使用源码编译安装最新的`crosstool-ng`。从[crosstool-ng网站](http://crosstool-ng.org/)下载最新的代码。通常最新的版本的crosstool-ng会支持最新的编译器。

```
$ wget
http://crosstool-ng.org/download/crosstool-ng/crosstool-ng-1.22.0.tar.bz2
$ tar xvf crosstool-ng-1.22.0.tar.bz2
$ cd crosstool-ng/
$ ./configure
$ make
$ make install
```

## 配置工具链

### 创建一个大小写敏感的文件系统

在Zephyr内核源码树中，我们为ARM和X86平台提供了两种配置方案用以提前确定在编译工具链时的可选项。配置文件能在`$ZEPHYR_BASE/scripts/cross_compiler/`中找到。

```
$ cp ${ZEPHYR_BASE}/scripts/cross_compiler/x86.config .config
```

使用配置菜单可，用户可以自定义已存在的配置或创建新的配置。

```
$ ct-ng menuconfig
```

### 验证工具链的配置

在开始构建工具链之前，我们建议进行一个快速的工具链配置验证。

1. 打开生成的`.config`文件。
2. 确保以下内容在配置文件中存在，假设镜像挂载点为`/Volumes/CrossToolNG`：

```
...
CT_LOCAL_TARBALLS_DIR="/Volumes/CrossToolNG/src"
# CT_SAVE_TARBALLS is not set
CT_WORK_DIR="${CT_TOP_DIR}/.build"
CT_PREFIX_DIR="/Volumes/CrossToolNG/x-tools/${CT_TARGET}"
CT_INSTALL_DIR="${CT_PREFIX_DIR}"
...
```

### 构建工具链

输入以下命令开始构建工具链：

```
$ ct-ng build
```

上述指令的执行可能会花费一些时间。当执行结束时，你可以在`/Volumes/CrossToolNG/x-tools`目录下找到构建完成的工具链。如果你需要支持不同架构的工具链，为所有的架构重复执行上述命令。

为了使用Zephy工具链，需要设置如下的环境变量，并且使用安装位置的工具链：

```
$ export ZEPHYR_GCC_VARIANT=xtools
$ export ZEPHYR_SDK_INSTALL_DIR=/Volumes/CrossToolNG/x-tools
```

如果要在未来的会话中使用相同的工具链，可以在文件`$HOME/.zephyrrc`中设置环境变量，例如：

```
$ cat <<EOF > ~/.zephyrrc
export ZEPHYR_SDK_INSTALL_DIR=/Volumes/CrossToolNG/x-tools
export ZEPHYR_GCC_VARIANT=xtools
EOF
```


# 在Linux系统上搭建开发环境

本节主要介绍如何搭建一个基于Linux系统的Zehpyr开发环境。

在完成本节的所有步骤之后，你能够在以下系统上编译和运行自己的Zephyr应用：

* Ubuntu 14.04 LTS 64 bit
* Fedora 22 64 bit

当需要时，针对Ubuntu和Fedora的不同安装指令会被特别说明。

## 安装宿主机操作系统

我们已经在Ubuntu和Fedora系统上成功的构建了包括内核在内的Zephyr项目所有组件。如何安装Ubuntu和Fedora系统已经超出了本文档的讨论范围。

## 更新你的操作系统

在开始搭建开发环境之前，确保你的系统软件库已被更新。

对于Ubuntu系统：

```
$ sudo apt-get update
```

对于Fedora系统：

```
$ sudo dnf update
```

## 配置网络和代理

构建Zephyr的内核需要`git`，`ssh`，`wget`，`curl`命令行工具，确保这些命令行工具能够在普通用户和root用户权限下运行并不被防火墙阻碍能够访问英特网。

如果你的网络访问需要通过代理服务，请按照你所在网络的安全策略配置网络使得`git`，`ssh`，`wget`能够访问网络。

## 安装必须的软件和依赖软件

使用`apt-get`或`dnf`工具来安装以下软件。

> 注意：对于以下列举的所需软件包，最小版本号的不同并不会映像软件的使用。

> 特别注意：在安装下列软件包前，请建超你的防火墙和代理配置来确认英特网访问是可以的。

在Ubuntu系统主机上安装所需软件包：

```
$ sudo apt-get install git make gcc gcc-multilib g++ libc6-dev-i386 \
  g++-multilib
```

在Fedora系统主机上安装所需软件包：

```
$ sudo dnf group install "Development Tools"
$ sudo dnf install git make gcc glib-devel.i686 glib2-devel.i686 \
  glibc-static libstdc++-static glibc-devel.i686
```

> 重要信息：请确保至少有32位版本的软件包被安装。理想情况下，64位和32位软件包都需要被安装。

### 设置项目的环境变量

1) 进入到项目的主目录：

```
$ cd zephyr-project
```

2) 使用Source命令载入项目的环境变量文件到系统：

```
$ source zephyr-env.sh
```

### 安装Zephyr的软件开发工具包（SDK）

Zephyr项目的SDK包括了在所有不同硬件架构平台上构建内核所需的工具和交叉编译器。此外，该SDK还包括了开发主机工具，例如一个定制的QEMU和为了构建开发主机工具所需要的编译器。该SDK支持一下硬件架构：

* IA-32
* ARM
* ARC

按照一下步骤在Linux开发主机上安装SDK。

1) 下载[SDK自解压二进制文件](https://nexus.zephyrproject.org/content/repositories/releases/org/zephyrproject/zephyr-sdk/0.7.2-i686/zephyr-sdk-0.7.2-i686-setup.run)

> Hint：访问[Zephyr SDK archive](https://nexus.zephyrproject.org/content/repositories/releases/org/zephyrproject/zephyr-sdk/) 查看所有可用版本列表。

```
$ wget https://nexus.zephyrproject.org/content/repositories/releases/org/zephyrproject/zephyr-sdk/0.7.2-i686/zephyr-sdk-0.7.2-i686-setup.run
```

2) 运行安装二进制文件，执行：

```
$ chmod +x zephyr-sdk-0.7.2-i686-setup.run
$ sudo ./zephyr-sdk-0.7.2-i686-setup.run
```

> 注意：如果SDK是安装到当前用户的Home文件夹中，则不需要使用`sudo`来运行。

3) 根据屏幕上的安装说明进行安装。工具链的默认安装位置是：`/opt/zephyr-sdk/`。

```
Verifying archive integrity... All good.
Uncompressing SDK for Zephyr  100%
Enter target directory for SDK (default: /opt/zephyr-sdk/):
```

4) 如果不想安装在默认目录，则输入新的安装位置，否则按回车进行默认位置安装。

```
Installing SDK to /opt/zephyr-sdk/
Creating directory /opt/zephyr-sdk/
Success
[*] Installing x86 tools...
[*] Installing arm tools...
[*] Installing arc tools...
...
[*] Installing additional host tools...
Success installing SDK. SDK is ready to be used.
```
5) 使用Zephyr的SDK，需要导出以下的环境变量到系统，其中SDK目录环境变量为你设置的环境变量：

```
$ export ZEPHYR_GCC_VARIANT=zephyr
$ export ZEPHYR_SDK_INSTALL_DIR=/opt/zephyr-sdk
```

为了将来能在新的会话中使用相同的工具链，可以在文件`$HOME/.zephyrrc`设置这些环境变量，例如：

```
$ cat <<EOF > ~/.zephyrrc
export ZEPHYR_GCC_VARIANT=zephyr
export ZEPHYR_SDK_INSTALL_DIR=/opt/zephyr-sdk
EOF
```


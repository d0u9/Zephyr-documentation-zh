# 搭建和配置Zephyr开发环境

搭建和配置Zephyr开发环境需要两个步骤来完成：

1. 下载代码
2. 配置开发环境

## 下载代码

Zehpyr代码由Linux基金会托管，使用Gerrit作为后端的托管平台支持使用GIT进行匿名克隆。

### Checkout源码

1) 克隆代码仓库：

```
$ git clone https://gerrit.zephyrproject.org/r/zephyr zephyr-project
```

执行完上一条命令后，代码就已经成功的克隆至本地计算机上了。

> 注意：一旦你准备开始贡献代码，首先应注册Linux基金会账号，注册步骤见[该页](https://www.zephyrproject.org/doc/collaboration/code/gerrit_accounts.html#gerrit-accounts)。

> 重要提示：Linux用户需要在成功克隆完代码后，下载Zephyr SDK。该SDK包含了许多非Zephyr项目的包。查看[安装Zephyr软件开发包](https://www.zephyrproject.org/doc/getting_started/installation_linux.html#zephyr-sdk)获取详细信息。

## 配置开发环境

Zephyr项目的开发环境支持一下系统：

1. Linux
2. Mac OS

根据你的开发系统选择以下合适的步骤来配置开发环境。

用下面的配置步骤来搭建一个全新的开发环境。鉴于文件层次结构可能会随着版本的发布而改变，本配置说明对已有的开发环境可能并不适用。

根据你的开发系统逐条的按照一下步骤搭建开发环境：

* [在Linux系统上搭建开发环境](development_environment_setup_on_linux.md)
    * [安装宿主机操作系统](development_environment_setup_on_linux.md#安装宿主机操作系统)
    * [更新你的操作系统](development_environment_setup_on_linux.md#更新你的操作系统)
    * [配置网络和代理](development_environment_setup_on_linux.md#配置网络和代理)
    * [安装必须的软件和依赖软件](development_environment_setup_on_linux.md#安装必须的软件和依赖软件)


* [在Mac OS系统上搭建开发环境](development_environment_setup_on_mac_os.md)
    * [更新你的操作系统](development_environment_setup_on_mac_os.md#更新你的操作系统)
    * [安装必须的软件和依赖软件](development_environment_setup_on_mac_os.md#安装必须的软件和依赖软件)
    * [配置工具链](development_environment_setup_on_mac_os.md#配置工具链)



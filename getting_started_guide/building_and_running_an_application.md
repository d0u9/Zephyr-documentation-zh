# 构建和运行Zephyr应用

恭喜你！你已成功了搭建了自己的Zephyr开发环境并且创建了新的Zephyr应用。本节将会介绍构建和运行一个建包含有应用的内核的所有必要步骤。我们会使用_Hello World_示例应用作为一个例子。构建_Hello World_应用的所有必要步骤与构建其他应用的步骤是完全相同的。

构建和运行一个Zephyr应用的过程与在其他操作系统下构建应用的过程是相同的。然而，在不同的操作系统下构建应用所需的命令却是完全不同的。以下部分使用的命令是基于Linux开发环境的，如果您使用Mac OS，请使用对应的合适命令。

## 构建一个示例应用

使用如下步骤来构建一个示例应用：

1. 切换工作目录为Zephyr工程的根目录。
2. 在每个控制台上设置环境变量，见[设置项目的环境变量](development_environment_setup_on_linux.md#设置项目的环境变量)
3. 使用如下命令构建示例工程：

```
$ cd $ZEPHYR_BASE/samples/hello_world/microkernel
$ make
```
上面的make指令会使用Makefile中的默认设置来构建hello_world示例应用。通过定义**BOARD**变量所支持平台中的某一种来构建针对不同平台的应用，例如：

```
$ make BOARD=minnowboard
``` 
有关支持平台的更多信息，请点击[这里](https://www.zephyrproject.org/doc/board/board.html#board)。此外，在代码的根目录下运行一下代码能够获取特定架构处理器所支持平台的列表：

```
$ make help
```

对于微/纳内核所对应的示例工程代码可以各自在`$ZEPHYR_BASE/samples/microkernel/apps`和`$ZEPHYR_BASE/samples/nanokernel/apps`中找到。在成功构建应用之后，最终生成的应用可以在应用根文件夹下的`outdir`目录中找到。

由构建系统所生成的ELF二进制文件被默认命名为`zephyr.elf`。该文件名能够在Makefile中被改写。构建系统会根据不同硬件之上的不同平台为不同的用例生成不同的文件名。

## 运行示例应用

为了在开发环境中快速的测试你的应用，你可以使用QEMU，前提是你的平台和架构能够被其支持。该过程能够轻松地通过在构建应用时指明一个特殊的生成目标而完成，构建过程结束后就可以调用QEMU进行测试。

1. 使用默认的板卡配置来运行应用，输入：

```
$ make qemu
```

要使用x86模拟板卡配置（qemu_x86）来运行应用，输入：

```
$ make BOARD=qemu_x86 qemu
```

要使用ARM qemu_cortex_m3板卡配置来运行应用，输入：

```
$ make BOARD=qemu_cortex_m3 ARCH=arm qemu
```

QEMU并不支持所有的板卡和平台。有些示例程序和测试应用在模拟器中运行时可能会失败。当为某款制定的目标硬件进行开发时，你应该总在实际的硬件上进行测试并且不应仅仅依靠QEMU模拟器的下的测试结果。



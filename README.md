# Zephyr-documentation-zh

> Zephyr Project is a small, scalable real-time operating system for use on resource-constrained systems supporting multiple architectures.  Developers are able to tailor their optimal solution. As a true open source project, the community can evolve the Zephyr Project to support new hardware, developer tools, sensor and device drivers.  Advancements in security, device management capabilities, connectivity stacks and file systems can be easily implemented.

Zephyr项目是为资源受限的多种计算机架构所设计的一个微型的，可扩展的实时操作系统。开发者能够通过d对其裁剪来为优化解决方案。作为一个真正的开源项目，社区支持能够让Zephyr项目不断迭代从而支持更多的硬件、开发者工具、传感器和设备驱动。在安全性、设备管理兼容性，连接栈和文件系统方面的新技术能够轻松的被实现。

## Zephyr 发布说明

在2016年2月17日，Linux基金会在旧金山宣布了Zephyr项目。该开源项目将通过整个工业界领导企业的联合协作努力，为物联网（IoT）构建一个全新的实时操作系统（RTOS）。

目前Zephyr项目已经获得了英特尔、NXP半导体、Synopsys和UbiquiOS等公司的支持，英特尔子公司Wind River向Zephyr项目捐赠了它的Rocket RTOS内核。

工业级和消费级的IoT设备需要一个可扩展的，安全的，能够无缝连接的软件平台。开发者们同样需要一个高度模块化的平台为他们的创新提供帮助，该平台在能够与各种嵌入式设备相集成的同时，应该是架构无关的。尽管Linux系统对于嵌入式开发来说已经是一个非常成功的操作系统，但部分IoT设备需要一种内存占用非常小的RTOS。这样一个RTOS补充了Linux在硬实时方面的不足，该系统适合于数据采集，工业生产和其它对实时性非常敏感设备。

在构建该嵌入式IoT设备系统时，模块化和安全性是重要的考虑因素。该项目非常重视系统的安全性，为此成立了专门的安全工作组，并委派了专门的负责安全事物的维护着。通信和网络支持同样也得到了解决，项目最初将包括蓝牙，低功耗蓝牙和IEEE 802.15.4，随着时间的推移该项目将会支持更多的通信和网络协议支持。

## 目录

* [前言](README.md)
* [准备开始](getting_started/README.md)
    * [Zephyr项目介绍](getting_started/introduction_to_the_zephyr_project.md)
    * [Zephyr入门指南](getting_started/getting_started_guide/README.md)
        * [搭建和配置Zephyr开发环境](getting_started/getting_started_guide/setting_up_for_zephyr_development.md)
        * [开发Zephyr应用](getting_started/getting_started_guide/developing_zephyr_applications.md)
        * [构建和运行Zephyr应用](getting_started/getting_started_guide/building_and_running_an_application.md)
    * [Zephyr基础](getting_started/zephyr_kernel_primer/README.md)

## 本翻译项目的初衷

IoT技术将会是未来几年的热门，Linux基金会在此时发布Zephyr项目具有深渊的意义。作为一个普通的计算机爱好者，能够看到一款1.0.0系统发布感到非常的开心和兴奋，希望自己能为此贡献出自己的一点点微薄之力。

作为一个技术渣，只能通过这种翻译文档的方式为更多的人造福，让更多的人了解并参与到Zephyr相关的工作中来。

## 许可证

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.


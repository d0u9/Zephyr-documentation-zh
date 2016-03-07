# 内核基础

该部分从高度概括的角度对Zephyr内核的能力和相关概念进行介绍。

## 组织

Zephyr内核的中心元素是它的微内核（microkernel）以及底层的纳内核（nanokernel）。内核还包含大量的辅助子系统，包括一个有关设备驱动和网络软件的库。

Zephyr能够使用微内核和纳内核开发，也可以仅采用纳内核。

纳内核是一个具有基本内核特性的高性能，多线程运行环境。微内核对资源有限系统（内核自身需要至少2K的内存！）或仅仅需要多线程支持系统（例如一组中断处理函数与单一的后台任务）来说是理想的。这类系统的例子有：嵌入式传感器集线器（embedded sensor hub），坏境传感器（environmental sensor），简易可穿戴LED，存储库存标签（store inventory tags）。

微内核为纳内核补充了更加丰富的内核特性支持。微内核适合于那些有较为充足内存（50至900KB）的系统，多通信设备（multiple communication devices）（例如WIFI和低功耗蓝牙）以及包含有数据处理多任务的系统。这类系统的例子有：可穿戴健身设备（fitness wearables），智能手表（smart watches），以及IoT无线网管（IoTwireless gateways）。

相关章节：

* [常用内核服务](common_kernel_services.md)

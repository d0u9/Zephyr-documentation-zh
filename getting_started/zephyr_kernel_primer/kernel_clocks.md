# 内核时钟

## 相关概念

内核支持两种不同的时钟。

- 一个64位的系统时钟（system clock），它是内核中基于时间的相关服务的基础。该时钟是一个计数器用以对滴答数（ticks）计数，并且以应用确定的频率递增。

内核允许通过直接访问定时器来访问该时钟。它同样能够通过使用内核定时器或超时功能来间接访问。

- 一个32位的硬件时钟（hardware clock），它作为系统时钟滴答的来源。该时钟是一个计数器，其计数单位并没有指定（称为周期（cycles）），并且以soc硬件的设定频率来递增。

内核允许通过读取定时器来直接访问该时钟。

内核也提供了许多不同的方法将时钟使用的时间单位转换成标准时间单位（例如：秒，微秒，毫秒等），在不同的两种类型时间单位之间转换。

## 目的

当基于时间的处理不需要较高精度的情况时，使用系统时钟，例如实现时间限制或时间延迟。

当基于时间的处理需要比系统时钟更高精度的情况时，使用硬件时钟，例如高精度时间测量。

> Note：硬件时钟的高频率，计数器的32位限制，意味着当使用高精度时钟对一段时间进行度量时，时钟计数器的回转情况必须被考虑到。

## 使用方法

### 配置内核时钟

使用`SYS_CLOCK_TICKS_PER_SEC`配置选项来指定每秒的滴答数。将该值设置为0会禁用所有的系统时钟和硬件时钟。

> Note：使用更高的系统时钟频率额允许系统时钟提供颗粒更细的时间，但是也同样增加了内核处理滴答数的工作量（由于它们出现的更加频繁）。

### 示例：使用正常精度来计量时间

下面的代码使用系统时钟来确定在一段时间中有多少时钟滴答。

```
int64_t time_stamp;
int64_t ticks_spent;

/* capture initial time stamp */
time_stamp = sys_tick_get();

/* do work for some (extended) period of time */
...

/* compute how long the work took & update time stamp */
ticks_spent = sys_tick_delta(&time_stamp);
```

### 示例：高精度时间计量

下面的代码使用硬件时钟来确定在一段时间中有多少始终滴答。

```
uint32_t start_time;
uint32_t stop_time;
uint32_t cycles_spent;
uint32_t nanoseconds_spent;

/* capture initial time stamp */
start_time = sys_cycle_get_32();

/* do work for some (short) period of time */
...

/* capture final time stamp */
stop_time = sys_cycle_get_32();

/* compute how long the work took (assumes no counter rollover) */
cycles_spent = stop_time - start_time;
nanoseconds_spent = SYS_CLOCK_HW_CYCLES_TO_NS(cycles_spent);
```

## API

下面的内核时钟API在`microkernel.h`头文件中导出：

`sys_tick_get()`，`sys_tick_get_32()`

读取系统时钟。

`sys_tick_delta()`,`sys_tick_delta_32()`

计算从上次读取系统时钟到现在所经过的时间。


下面的内核时钟API由`microkernel.h`和`nanokernel.h`导出：

`sys_tick_get()`，`sys_tick_get_32()`

读取系统时钟。

`sys_tick_delta()`,`sys_tick_delta_32()`

计算从上次读取系统时钟到现在所经过的时间。

`sys_cycle_get_32()`

读取硬件时钟。

下面的内核时钟变量由`microkernel.h`和`nanokernel.h`导出。

`sys_clock_ticks_per_sec`

一秒内的系统时钟滴答数。

`sys_clock_hw_cycles_per_sec`

一秒内的硬件时钟周期数。

`sys_clock_us_per_tick`

一个系统时钟滴答内的微秒数。

`sys_clock_hw_cycles_per_tick`

一个系统时钟滴答内的硬件时钟周期数。



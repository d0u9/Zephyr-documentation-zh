# 执行上下文服务

## 概念

每一个内核执行上下文都会和一种_类型_（type）关联，类型指明了当前的上线文是一个任务（task），一个线（fiber）或者是内核中断处理上下文（kernel's inetrrupt handling context)）。任务和线上下与_内核标识符_（thread identifier）值相关联，用以唯一的确定这些运行的线程。

每一个任务和线都支持32位的_自定义线程数据_（thread custom data）,该数据只能由任务或线自身来访问并应用用以任何目的。任务和线的默认的自定义线程数据值为0。

> Note: 自定义数据不能被运行在共享内核处理上下文中的ISR所访问。

内核允许任务和线通过忙等待（busy wait）的方式将自身延迟一个指定的时间。忙等待能够让任务或线在不通过内核进行上下文切换的情况下进行延迟。而在典型的定时器或超时服务中延时往往伴随着内核上下文的切换。

## 目标

在编写代码时使用内核执行上下文服务需要根据在不同的上线文中的执行来采取不同的操作。

当所需要的延时太短以至于不用进行任务或线的上下文切换时，或者当执行的延时是纳内核后台任务的一部分时（这种情况不允许自愿的放弃CPU）应该采用忙等待延迟方法。

## 使用方法

### 配置自定义数据支持

使用`THREAD_CUSTOM_DATA`配置选项来开启线程自定义数据的支持。默认情况下，自定义数据支持是关闭的。

### 示例：执行上下文特定处理

这段代码中函数使用一个线程的自定义数据用来限制线程能够调用该函数的次数。计数并不会发生在ISR调用该函数的时，在ISR上下文中不存在自定义数据。

> Note：很明显，只能有一个函数采用这种技巧，因为这个函数独占了用户自定数据的使用。

```
#define CALL_LIMIT 7

int call_tracking_routine(void)
{
    uint32_t call_count;

    if (sys_execution_context_type_get() != NANO_CTX_ISR) {
       call_count = (uint32_t)sys_thread_custom_data_get();
       if (call_count == CALL_LIMIT)
      return -1;
  call_count++;
  sys_thread_custom_data_set((void *)call_count);
    }

    /* do rest of routine's processing */
    ...
}
```

## APIs

以下的内核执行上下文API由`microkernel.h`和`nanokernel.h`导出。

```
sys_thread_self_get()
```

获取当前运行任务和线的线程描述符。

```
sys_execution_context_type_get()
```

获取当前执行上线文（任务，线，ISR）的类型。

```
sys_execution_context_type_get()
```

向当前运行任务或线的自定义数据中写。

```
sys_thread_custom_data_get()
```

从当前运行任务或线的自定义数据中读。


# 原子操作服务

## 概念

Zephyr支持一种32位的原子数据类型，既`atomic_t`类型。这种类型的数据能够被任何任务、线或者中断服务以不被打断（原子性）的方式进行读取和修改。这就保证了用户所期望的操作不会因为高优先级任务的调度而被干扰，即使高优先级任务也对同一个数据进行操作。

## 目的

使用原子操作服务来实现对临界区的处理仅需对单独的一个32位数据元素进行操作。

> Note：相比于其他实现临界区的方法，例如使用微内核互斥变量，讲处理卸载至线或锁中断，使用原子变量来实现临界区能够获得更好的信能。

## 使用方法

### 示例：实现一个不会被打断的计数器

下面的代码用来展示了函数如何统计自己已经被调用的次数。由于计数是自动自增的，不存在由于调用相同函数的高优先级任务被调度导致的递增中间被打断的风险。

```
atomic_t call_count;

int call_counting_routine(void)
{
    /* increment invocation counter */
    atomic_inc(&call_count);

    /* do rest of routine's processing */
    ...
}
```

## API

以下的原子操作API在`atomic.h`中导出。

`atomic_get()`

读原子操作变量。

`atomic_set()`

写远在操作变量。

`atomic_clear()`

将原子操作变量清零。

`atomic_add()`

对原子操作变量进行加操作。

`atomic_sub()`

对原子操作变量进行减操作。

`atomic_inc()`

对原子操作变量进行自增1。

`atomic_dec()`

对原子操作变量进行自减1。

`atomic_and()`

对原子操作变量进行与运算。

`atomic_or()`

对原子操作变量进行或运算。

`atomic_xor()`

对原子操作变量进行异或运算。

`atomic_nand()`

对原子操作变量进行与非运算。

`atomic_cas()`

对原子操作变量进行Test-and-Set操作。

`atomic_set_bit()`

将原子操作变量的特定位置1。

`atomic_clear_bit()`

将原子操作变量的特定位置0。

`atomic_test_bit()`

读取原子操作变量的特定位。

`atomic_test_and_set_bit()`

读取原子操作变量的特定位并将其置1。

`atomic_test_and_clear_bit()`

读取原子操作变量的特定位并将其置0。


## Mushroom（蘑菇）：并发B<sup>link</sup>树索引
[English Version of README](./README.en.md)

[![Author](https://img.shields.io/badge/Author-UncP-brightgreen.svg)]()
[![Version](https://img.shields.io/badge/Version-0.6.2-orange.svg)]()
[![Build](https://img.shields.io/badge/Build-Passing-brightgreen.svg)](https://travis-ci.org/UncP/Mushroom)
[![License](https://img.shields.io/badge/License-BSD--3-red.svg)](./LICENSE)

### 警告，Mushroom具有非常强悍的性能！

### Feature
+ 并发B<sup>link</sup>树索引
+ 前缀压缩（懒惰）
+ 二次哈希页面管理器
+ 多线程（锁管理器、线程池、二次映射有界队列）
+ 多进程（共享内存映射）

******

### B<sup>link</sup> Tree BenchFuck
`关键值长度： 16 字节`  
`关键值数量： 1000 万组`  
`总大小：160 M`  
`CPU信息: Intel i3  2.1GHz  4核`

| 版本号 | 多线程 | 多进程 | 排序时间（秒）|           备注             |
|:------:|:-----:|:-----:|:-----------:|:---------------------------:|
| 0.1.0  |  否  |  否  |   16.00    ||
| 0.2.0  |  是  |  否  |   12.32    |         读写锁并发索引          |
| 0.2.1  |  是  |  否  |   11.28    |         锁管理器优化            |
| 0.3.0  |  是  |  否  |   10.94    |前缀压缩，B<sup>link</sup>树占用内存减少约 9.1 %|
| 0.4.0  |  是  |  否  |   11.44    |二次映射多线程工作队列，减少程序使用内存超过 50 %|
| 0.4.1  |  是  |  否  |     \      |合并锁管理器与页面管理器，使每次操作减少1把锁|
| 0.4.2  |  是  |  否  |     \      |修改根节点分裂方式|
| 0.4.3  |  是  |  否  |     \      |增加测试策略，多线程不经过队列直接进行任务|
| 0.4.4  |  是  |  否  |     \      |重构锁管理器|
| 0.5.0  |  是  |  否  |11.70 / 9.00|修复从版本0.4.1到0.4.4一直存在的**bug**（原子操作bug）|
| 0.6.0  |  是  |  是  |     \      |使用共享内存映射支持多进程，修复搜索操作**bug**，完成并发B<sup>link</sup>树的正确实现|
| 0.6.1  |  是  |  否  |18.69 / 13.04|二次哈希页面管理器，实现页面的懒惰分配|
| 0.6.2  |  是  |  否  |11.89 / 8.14|减少对标准库的依赖，加快编译速度，减少程序体积约33%|


### 其他
+ 版本0.6.0是第一个稳定版本
+ 最新测试: 1亿组 16字节 排序用时142.5秒 占用内存约2.7G
+ 你可以在[这里](https://zhuanlan.zhihu.com/p/24800198)找到B<sup>link</sup>树的并发控制协议介绍及证明

# lec6 SPOC思考题

## 与视频相关思考题

### 6.1	非连续内存分配的需求背景
 1. 为什么要设计非连续内存分配机制？

因为连续内存分配机制会产生很多碎片，而非连续内存分配机制可以高效利用内存。

 1. 非连续内存分配中内存分块大小有哪些可能的选择？大小是否可变?

段式大小可变和页式大小不可变。

 1. 为什么在大块时要设计大小可变，而在小块时要设计成固定大小？小块时的固定大小可以提供多种选择吗？

### 6.2	段式存储管理
 1. 什么是段、段基址和段内偏移？

段表示访问方式和存储属性相同的一段空间，段基址是这个段的开头的地址，段内偏移+段机制可以用来寻址。

 1. 段式存储管理机制的地址转换流程是什么？为什么在段式存储管理中，各段的存储位置可以不连续？这种做法有什么好处和麻烦？

段基址+段内偏移

因为段本来就是分开的。。可以通过GDT来访问各个段，没必要连续。

好处：可以不连续；麻烦：地址转换麻烦。

### 6.3	页式存储管理
 1. 什么是页（page）、帧（frame）、页表（page table）、存储管理单元（MMU）、快表（TLB, Translation Lookaside Buffer）和高速缓存（cache）？

页是虚拟内存中的一段大小固定的空间。

帧是物理内存中的页面。

页表是存储页和帧映射的表。

MMU是管理内存的部分。

TLB是页表的Cache。

Cache是内存的缓存。

 1. 页式存储管理机制的地址转换流程是什么？为什么在页式存储管理中，各页的存储位置可以不连续？这种做法有什么好处和麻烦？

 页号+页内偏移。

 因为有页表可以查。

 好处和麻烦和段一样。

### 6.4	页表概述
 1. 每个页表项有些什么内容？有哪些标志位？它们起什么作用？

帧号，标志位。

有存在位，修改位，引用位。作用见名字。。

 1. 页表大小受哪些因素影响？

页的数目、页表项的大小。

### 6.5	快表和多级页表
 1. 快表（TLB）与高速缓存（cache）有什么不同？

TLB缓存的是页表，cache缓存的是数据。

 1. 为什么快表中查找物理地址的速度非常快？它是如何实现的？为什么它的的容量很小？

因为快表在CPU中，应该和Cache的实现一样吧，因为容量大会很贵，而且会变慢。

 1. 什么是多级页表？多级页表中的地址转换流程是什么？多级页表有什么好处和麻烦？

 就是多个级别的页表。

 由虚拟地址找到第一个页表项，然后找到第二个…以此类推。

 好处：存储空间减少。

 麻烦：寻址次数变多。

### 6.6	反置页表
 1. 页寄存器机制的地址转换流程是什么？

逻辑地址进行hash，然后查相应页寄存器。

 1. 反置页表机制的地址转换流程是什么？

逻辑地址和进程号共同进行hash，然后查相应页寄存器。

 1. 反置页表项有些什么内容？

 PID、逻辑页号、标志位。

### 6.7	段页式存储管理
 1. 段页式存储管理机制的地址转换流程是什么？这种做法有什么好处和麻烦？

见上面段/页存储管理机制的地址转换流程。好处：空间利用率高。麻烦：转换麻烦。

 1. 如何实现基于段式存储管理的内存共享？

让两个段指向相同的页表基址。

 1. 如何实现基于页式存储管理的内存共享？

 让两个页指向相同的页表基址/页基址。
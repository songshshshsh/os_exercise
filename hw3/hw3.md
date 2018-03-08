## 第三讲 启动、中断、异常和系统调用-思考题

## 3.1 BIOS
-  BIOS从磁盘读入的第一个扇区是是什么内容？为什么没有直接读入操作系统内核映像？
- 比较UEFI和BIOS的区别。

读入的第一个扇区是MBR，没有直接读入的原因是操作系统内核映像太大，而且直接从BIOS读入操作系统就会不得不把操作系统写死在内存中，这不利于兼容各种操作系统。

UEFI可以切换到BIOS，但BIOS不能切换到UEFI。BIOS能用U盘启动而UEFI不能。

UEFI相比BIOS的优势：

1、通过保护预启动或预引导进程，抵御bootkit攻击，从而提高安全性。

2、缩短了启动时间和从休眠状态恢复的时间。

3、支持容量超过2.2 TB的驱动器。

4、支持64位的现代固件设备驱动程序，系统在启动过程中可以使用它们来对超过172亿GB的内存进行寻址。

5、UEFI硬件可与BIOS结合使用。


## 3.2 系统启动流程

- 分区引导扇区的结束标志是什么？

0x55AA。

- 在UEFI中的可信启动有什么作用？

通过启动前的数字签名检查来保证启动介质的安全性

## 3.3 中断、异常和系统调用比较
- 什么是中断、异常和系统调用？

中断：对外部设备的响应。

异常：指令发生错误。

系统调用：应用程序请求系统服务。

-  中断、异常和系统调用的处理流程有什么异同？

中断：由外设产生，异步处理，对用户透明。

异常：由程序产生，同步处理，系统杀死异常程序。

系统调用：由应用程序产生，同步或异步处理，系统进入内核态后提供相关服务后返回用户态。

- 以ucore lab8的answer为例，uCore的系统调用有哪些？大致的功能分类有哪些？

进程管理：包括 fork/exit/wait/exec/yield/kill/getpid/sleep

文件操作：包括 open/close/read/write/seek/fstat/fsync/getcwd/getdirentry/dup

内存管理：pgdir命令

外设输出：putc命令

## 3.4 linux系统调用分析
-  通过分析[lab1_ex0](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex0.md)了解Linux应用的系统调用编写和含义。(仅实践，不用回答)
- 通过调试[lab1_ex1](https://github.com/chyyuu/ucore_lab/blob/master/related_info/lab1/lab1-ex1.md)了解Linux应用的系统调用执行过程。(仅实践，不用回答)


## 3.5 ucore系统调用分析 （扩展练习，可选）
-  基于实验八的代码分析ucore的系统调用实现，说明指定系统调用的参数和返回值的传递方式和存放位置信息，以及内核中的系统调用功能实现函数。
- 以ucore lab8的answer为例，分析ucore 应用的系统调用编写和含义。
- 以ucore lab8的answer为例，尝试修改并运行ucore OS kernel代码，使其具有类似Linux应用工具`strace`的功能，即能够显示出应用程序发出的系统调用，从而可以分析ucore应用的系统调用执行过程。

 
## 3.6 请分析函数调用和系统调用的区别
- 系统调用与函数调用的区别是什么？

系统调用进入内核态，函数调用在用户态。

系统调用会用新的栈，函数调用不会用新栈。

系统调用使用int和iret，函数调用使用call和ret。

- 通过分析`int`、`iret`、`call`和`ret`的指令准确功能和调用代码，比较函数调用与系统调用的堆栈操作有什么不同？

在系统调用时，由于会用到新的栈，所以会保存现场和保存ss,esp寄存器，但是函数调用的时候就不会，就直接用原有的栈，保存栈底和栈顶就行。


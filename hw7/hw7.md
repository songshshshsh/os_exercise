## 第七讲视频相关思考题

### 7.1 了解x86保护模式中的特权级

1. X86有几个特权级？

4个。

2. 不同特权级有什么区别？

不同特权级对段、页访问的权限不一样，且特权指令只能在内核态使用。

3. 请说明CPL、DPL和RPL在中断响应、函数调用和指令执行时的作用。

访问门时：从低优先级代码访问高优先级服务

访问段时：从高优先级代码访问低优先级数据

### 7.2 了解特权级切换过程

1. 一条指令在执行时会有哪些可能的特权级判断？

执行特权指令，中断，访问数据段。

2. 在什么情况下会出现特权级切换？

系统调用，中断。

3. int指令在ring0和ring3的执行行为有什么不同？

ring3要切换堆栈，还要将ss,esp压栈。

4. 如何利用int和iret指令完成不同特权级的切换？

用int把中断时的寄存器保存，iret恢复。

5. TSS和Task Register的作用是什么？

 > [Task state segment](https://en.wikipedia.org/wiki/Task_state_segment)

 > Reference: [Intel® 64 and IA-32 Architectures Software Developer Manuals](http://os.cs.tsinghua.edu.cn/oscourse/OS2017spring/lecture04?action=AttachFile&do=view&target=325462-sdm-vol-1-2abcd-3abcd.pdf) Page 2897/4684: 7.2.1 Task-State Segment (TSS)

### 7.3 了解段/页表

1. 一条指令执行时最多会出现多少次地址转换？

如果是段的话最多是2次，是页的话由页表级数决定。

2. 描述X86-32的MMU地址转换过程；

先确定段基址，然后加上偏移量算出真实地址。

### 7.4 了解UCORE建立段/页表

1. 分析MMU的使能过程，尽可能详细地分析在执行进入保护械的代码“movl %eax, %cr0 ; ljmp $CODE_SEL, $0x0”时，CPU的状态和寄存器内容的变化。

2. 分析页表的建立过程；



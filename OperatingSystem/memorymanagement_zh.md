操作系统的内存管理非常重要，主要负责下面这些事情：

- **内存的分配与回收**：对进程所需的内存进行分配和释放，malloc 函数：申请内存，free 函数：释放内存。
- **地址转换**：将程序中的虚拟地址转换成内存中的物理地址。
- **内存扩充**：当系统没有足够的内存时，利用虚拟内存技术或自动覆盖技术，从逻辑上扩充内存。
- **内存映射**：将一个文件直接映射到进程的进程空间中，这样可以通过内存指针用读写内存的办法直接存取文件内容，速度更快。
- **内存优化**：通过调整内存分配策略和回收算法来优化内存使用效率。
- **内存安全**：保证进程之间使用内存互不干扰，避免一些恶意程序通过修改内存来破坏系统的安全性。

#### [非连续内存管理](#非连续内存管理)

非连续内存管理存在下面 3 种方式：

- **段式管理**：以段(—段连续的物理内存)的形式管理/分配物理内存。应用程序的虚拟地址空间被分为大小不等的段，段是有实际意义的，每个段定义了一组逻辑信息，例如有主程序段 MAIN、子程序段 X、数据段 D 及栈段 S 等。
- **页式管理**：把物理内存分为连续等长的物理页，应用程序的虚拟地址空间也被划分为连续等长的虚拟页，是现代操作系统广泛使用的一种内存管理方式。
- **段页式管理机制**：结合了段式管理和页式管理的一种内存管理机制，把物理内存先分成若干段，每个段又继续分成若干大小相等的页

#### [单级页表有什么问题？为什么需要多级页表？](#单级页表有什么问题-为什么需要多级页表)

以 32 位的环境为例，虚拟地址空间范围共有 2^32（4G）。假设 一个页的大小是 2^12（4KB），那页表项共有 4G / 4K = 2^20 个。每个页表项为一个地址，占用 4 字节，`2^20 * 2^2 / 1024 * 1024= 4MB`。也就是说一个程序啥都不干，页表大小就得占用 4M。

系统运行的应用程序多起来的话，页表的开销还是非常大的。而且，绝大部分应用程序可能只能用到页表中的几项，其他的白白浪费了。

为了解决这个问题，操作系统引入了 **多级页表** ，多级页表对应多个页表，每个页表也前一个页表相关联。32 位系统一般为二级页表，64 位系统一般为四级页表。

这里以二级页表为例进行介绍：二级列表分为一级页表和二级页表。一级页表共有 1024 个页表项，一级页表又关联二级页表，二级页表同样共有 1024 个页表项。二级页表中的一级页表项是一对多的关系，二级页表按需加载（只会用到很少一部分二级页表），进而节省空间占用。

假设只需要 2 个二级页表，那两级页表的内存占用情况为: 4KB（一级页表占用） + 4KB * 2（二级页表占用） = 12 KB。





Real, or physical, memory exists on RAM chips inside the computer. Virtual memory, as its name suggests, doesn’t physically exist on a memory chip. It is an optimization *technique* and is implemented by the operating system in order to give an application program the impression that it has more memory than actually exists. Virtual memory is implemented by various operating systems such as Windows, Mac OS X, and Linux.





A ***page fault\*** occurs when a program tries to access a page that is mapped in address space, but not loaded in the physical memory (the RAM). In other words, a page fault occurs when a program can not find a page that it’s looking for in the physical memory, which means that the program would have to access the paging file (which resides on the hard disk) to retrieve the desired page.

The term page fault is a bit misleading as it implies that something went seriously wrong. Although page faults are undesirable – as they result in slow accesses to the hard disk – they are quite common in any operating system that uses virtual memory.

TLB 页表cache



[How Virtual Memory Works - Programmer and Software Interview Questions and Answers (programmerinterview.com)](https://www.programmerinterview.com/operating-systems/how-virtual-memory-works/)
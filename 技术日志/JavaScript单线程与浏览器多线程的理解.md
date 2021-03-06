JavaScript单线程与浏览器多线程的理解.md

进程与线程的概念
进程和线程都是操作系统的概念。进程是应用的执行实例，每一个进程都是由私有的虚拟地址空间、代码、数据和其他系统资源所组成；进程在运行的过程中能够申请和使用系统资源（比如独立的内存区域），这些资源会随进程的终止而销毁。而线程是进程内的独立执行单元，在不同的线程之间是可以共享进程资源的，所以在多线程的情况下，需要特别注意对临界资源的访问控制。在系统创建进程之后就开始启动执行进程的主线程，而进程的生命周期和这个主线程的生命周期一致，主线程的退出也就意味着进程的终止和销毁。主线程是由系统进程所创建的，同时用户也可以自主创建其它线程，这一系列的线程都会并发地运行于同一个进程中。

多线程的优势
在多线程操作的情况下可以实现应用的并行处理，而提高整个应用程序的性能和吞吐量，更大粒度的榨取本机的CPU利用率，特别是现代很多语言都支持了多核并行处理技术。

为什么JavaScript还是单线程
因为JavaScript这门脚本语言诞生的使命所致：JavaScript为处理页面中用户的交互，以及操作DOM树、CSS样式树来给用户呈现一份动态而丰富的交互体验和服务器逻辑的交互处理。如果JavaScript是多线程的方式来操作这些UI DOM，则可能出现UI操作的冲突；在多线程的交互下，处于UI中的DOM节点就可能成为一个临界资源，假设存在两个线程同时操作一个DOM，而线程1要求浏览器删除DOM节点，线程2却希望修改这个节点的某些样式风格。这个时候浏览器就无法裁决采用哪一种策略了。当然我们可以为浏览器引入“排它锁”或者是“乐观锁”来解决这些冲突，但为了避免引入了更大的复杂性，所以JavaScript从诞生开始就选择了单线程执行。

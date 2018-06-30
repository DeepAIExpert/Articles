在java和c#里，数据类型(value types)是存储在栈(stack)上的，引用类型(reference types)是存储在堆(heap)上。c++标准里是没有指定什么类型存储在堆(heap)或者栈(stack)上，但是给出了 automatic storage duration (在代码的scope结束的时候自动回收变量所占内存空间)和 dynamic storage duration(用户手动管理变量内存的分配和回收，分配过的内存未手动回收会造成内存泄露)这两个概念。局部变量(local variable) 属于automatic storage duration内存管理类型，编译器会把他们存储在栈上面。用new创建的对象属于dynamic memory allocation，存储在堆上。

![stack_heap](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/stack%26heap.png)


我们应该什么情况下为对象分配一个栈空间呢? 先来理解栈是什么，栈是由一个个栈帧(stack frame)组成。栈帧在运行时候用来存储函数调用的所有数据：调用参数、返回地址、局部变量(local variables)。 那么我们理解来栈帧，就可以明白什么栈是什么，用来做什么来。

在IA32(32 bits Intel Architecture)程序需要用栈来传递参数、存储返回信息、存储结束调用的时候需要恢复的寄存器的值、局部变量等，这是实现函数调用必不可少的环节。负责单个函数调用的那一段栈，称为这个函数调用的栈帧。最顶层的栈帧是被 %ebp和%esp两个指针分隔的那段栈。以下是栈帧的示意图：

![stack_frame](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/stackframe.png)

函数调用过程中的栈的变化，大概就是这样：
![top_most_stack_frame](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/top_most_stack_frame.png)

以上就是关于栈是什么和栈的作用的相关介绍，接下来看看什么堆，以及什么时候使用堆来存储对象。上面提到栈的使命是辅助实现函数调用，而堆的定位是额外的存储空间。它的存储空间没有特定的结构，供程序在运行期间动态的申请存储空间。需要手动去管理申请的那块内存空间，未释放会造成内存泄露。

以上关于栈 & 栈帧的部分内容 参考了：[Computer Systems: A Programmer’s Perspective (3rd Edition)](https://www.amazon.com/gp/product/013409266X/?tag=fhinkel-20)
![computer_system](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/computer_systems.jpg)



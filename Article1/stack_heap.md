在java和c#里，数据类型(value types)是存储在栈(stack)上的，引用类型(reference types)是存储在堆(heap)上。c++标准里是没有指定什么类型存储在堆(heap)或者栈(stack)上，但是给出了 automatic storage duration (在代码的scope结束的时候自动回收变量所占内存空间)和 dynamic storage duration(用户手动管理变量内存的分配和回收，分配过的内存未手动回收会造成内存泄露)这两个概念。局部变量(local variable) 属于automatic storage duration内存管理类型，编译器会把他们存储在栈上面。用new创建的对象属于dynamic memory allocation，存储在堆上。

![stack_heap](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/stack%26heap.png)

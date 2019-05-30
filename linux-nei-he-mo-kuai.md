# Linux 内核模块

## 哈哈，Hello World 内核模块

我们学习 C 语言的时候，我们会写一个 Hello World 来证明一下自己，然后我们学习 C++ 的时候，我们也会写一个 Hello World 来证明一下自己，然后我们会学习 java、python、还有其他很多很多的编程语言，但是最开始，你总是写一个 Hello World 来证明一下自己。

我也很想知道为什么我们跟 Hello World 那么过不去，来个比喻，这就像我们习惯了喝热水一样，如果仔细去追究，好像喝热水并不能如何如何，为什么我们习惯喝热水，很大的原因是因为我们的妈妈想让我们喝热水，因为我们的妈妈觉得喝热水是一个好习惯，喝热水是可以强身健体的，再反回来看我们为什么会在刚开始学习一个东西的时候喜欢去写 Hello World ，因为你接触的很多人告诉你这样做，如果可以，你明明是不需要些 Hello World 的，而是写 Hello You 或者 Hello 个其他什么东西的。

所以，我们还是要写一个 Hello World 来让自己入个门，进入那个深不可测的世界，聆听 Linux 给我们带来的快感。

## Hello World 内核模块代码

```c
#include <linux/init.h>
#include <linux/module.h>
MODULE_LICENSE("Dual BSD/GPL");
static int hello_init(void)
{
printk(KERN_ALERT "Hello, world\n");
return 0;
}
static void hello_exit(void)
{
printk(KERN_ALERT "Goodbye, cruel world\n");
}
module_init(hello_init);
module_exit(hello_exit);
```

就是这简单的几行代码，我们来简单的分析一下，前面两行是包含头文件，这个跟我们学习 C 语言没有什么区别，有了头文件才能调用函数，就是这么简单。

第三行，MODULE\_LICENSE 这个是声明模块的许可证说明的，比喻一下，我们开车，就必须有一个驾驶证，如果我们没有驾驶证，就会被交警叔叔给抓住，模块代码也一样，如果没有许可证声明，就会被内核给抓住。

模块的许可证声明 从 **2.4.10** 内核版本开始，模块必须通过 MODULE\_LICENSE 宏声明此模块的许可证，否则在加载此模块时，会收到内核被污染 “kernel tainted” 的警告。从 linux/module.h 文件中可以看到，被内核接受的有意义的许可证有 “GPL”，“GPL v2”，“GPL and additional rights”，“Dual BSD/GPL”，“Dual MPL/GPL”，“Proprietary”。

在同时支持2.4与2.6内核的设备驱动中，模块可按如下方式声明自己的许可证。

```c
MODULE_LICENSE(“GPL”);
```

然后下面就是声明的两个函数，函数里面调用了 printk 来打印内容，后面再有一个 module\_init 和 module\_exit ，望文生义，我们可以知道这两行代码是用来说明模块初始化的时候调用的函数和模块退出的时候调用的函数的。

## printk

内核里面是没有 C 库的，大家刚开始学习 C 语言的时候，知道一个函数叫做 printf ，这个也是一个打印函数，但是这个打印函数需要 C 库的帮忙，内核里面需要自己的打印函数，这个函数就叫做 printk。

KERN\_ALERT 这个是一个宏定义，用来控制内核打印的等级，等级很重要，通过控制等级可以动态的控制日志的输出，printk 经久不衰的原因也是因为有这么多优良的基因。














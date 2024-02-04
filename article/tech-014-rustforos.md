
# rust for os dever

https://rcore-os.cn/rCore-Tutorial-Book-v3/

目前MoeOS要做的工作很多，我也会在学习和工作之余继续完善MoeOS

https://rustmagazine.github.io/rust_magazine_2021/chapter_12/lets-make-os.html


### 使用ubuntu的gnome桌面时，偶尔会出现桌面卡死的情况。即鼠标可以正常移动，但是点击任何程序都是没有反应的。

解决方法有以下几种：

重启gnome桌面
直接alt+f2，会弹出个输入框。输入小写的r，回车，即可重启你的gnome-shell桌面环境。

Ctrl+Alt+F3 进入黑白屏的终端环境，top查看gnome的进程以及PID，使用kill -9 PID杀死gnome进程。此时系统会自动重启gnome桌面，可稍等一会。之后再Ctrl+Alt+F进入正常登录界面即可。

通过SysRq进行重启，这种方式的重启对正在编辑的数据可以起到一定的保护作用。

Github： 
https://github.com/plctlab/riscv-operating-system-mooc 
https://github.com/unicornx/riscv-operating-system-mooc 
Gitee： 
https://gitee.com/unicornx/riscv-operating-system-mooc


在线环境：

https://studious-space-waffle-g96gv7v9j9jfvw9x.github.dev/



### .cargo/config

```
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"

```

![应用程序从指令集到标准库的执行逻辑](image-67.png)


我们在 main.rs 的开头加上一行 #![no_std] 来告诉 Rust 编译器不使用 Rust 标准库 std 转而使用核心库 core（core库不需要操作系统的支持）。编译器报出如下错误：


使用动态链接可以显著缩减可执行文件的容量，并使得程序不必在函数库更新后重新链接依然可用。

为了保护我们的批处理操作系统不受到出错应用程序的影响并全程稳定工作，单凭软件实现是很难做到的，而是需要 CPU 提供一种特权级隔离机制，使 CPU 在执行应用程序和操作系统内核的指令时处于不同的特权级。本节主要介绍了特权级机制的软硬件设计思路，以及 RISC-V 的特权级架构，包括特权指令的描述。



sphinx作用，专注写文档，而不用关注渲染，程序员更好的写文档！

晶振是什么？

与 Trap 切换不同，它不涉及特权级切换；

与 Trap 切换不同，它的一部分是由编译器帮忙完成的；

与 Trap 切换相同，它对应用是透明的。


https://easychuan.cn/

https://asterinas.github.io/book/





# risc-v（代表第五代精简指令集）不是x86，arm,等
作用：硬件和机器语言的约定！
![os storage](image-68.png)


指令集（isa(instrction set architecture)）
学习：

https://github.com/unicornx/riscv-operating-system-mooc 
Gitee： 
https://gitee.com/unicornx/riscv-operating-system-mooc



rust语言的前途：
解决老板的问题，得到资本的支持，因为从内存上保证了，未来的可能的程序的安全！





---
layout: post
title:  "Exploring the Linux Kernel"
date:   2025-01-10 16:09:08 -0700
categories: operating-systems linux
---

I'm currently taking CMPUT379 - Introduction to Operating Systems, and the assigned textbook is Operating Systems: Three Easy Pieces by Remzi H. Arpaci-Dusseau and Andrea C. Arpaci-Dusseau. I want to see how the concepts discussed in the book are implemented in the Linux kernel. It may be more efficient to read a book about the Linux kernel, but exploring the codebase would be good practice.

### Process

The OSTEP book describes a process as an abstraction of a running program. The contents of memory in a program's address space, the contents of the CPU registers, and the state of I/O devices are sufficient to summarize a process. When the operating system switches context (pausing one process and running another), it must save the above information and load the state of the other process. OSTEP uses xv6 kernel as an example of how the operating system stores the state of a process. There are two structs, `context` and `proc`.

{% highlight C %}
struct context {
    int eip;
    int esp;
    int ebx;
    int ecx;
    int edx;
    int esi;
    int edi;
    int ebp;
};

struct proc {
    char *mem;
    uint sz;
    char *kstack;

    enum proc_state state;
    int pid;
    struct proc *parent;
    void *chan;
    int killed;
    struct file *ofile[NOFILE];
    struct inode *cwd;
    struct context context;
    struct trapframe *tf;
};

{% endhighlight %}

To find a similar struct in the Linux kernel, I search for any file named process. What I find is that there are multiple `process.h` and `process.c` files, each for a different instruction set architecture. It makes sense why this is the case; each architecture has a different set of registers. I pick the `process.c` that corresponds to RISC-V, since that is the ISA I'm most familiar with. Something to note is that there is no `process.h` file in the RISC-V section, and only the x86 and m68k sections have a `process.h` file.

There's a struct called `pt_regs` that seems to store the RISC-V registers. Though its definition is not in the file, there are a few functions that take the struct as an argument. These functions are `show_regs`, `__show_regs`, `start_thread`, and `copy_thread`. What is a thread? What is the difference between a thread and a process?


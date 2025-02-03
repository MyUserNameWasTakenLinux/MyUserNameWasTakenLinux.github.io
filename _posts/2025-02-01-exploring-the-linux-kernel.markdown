---
layout: post
title:  "Exploring the Linux Kernel"
date:   2025-02-01 12:09:08 -0700
categories: operating-systems linux
---

While reading John Madieu's *Linux Device Driver Development*, I came across spinlocks. According
to the book, a spinlock disables the scheduler on the local CPU, and so the currently running task on the CPU cannot be descheduled. The book also mentions that preemption is a per-CPU variable, the value of which determines whether or not preemption is enabled.

The file `include/linux/sched.h` contains the definition of task_struct. The task_struct has thread_info as one of its members. The thread_info struct is not defined within `include/linux/thread_info.h`, but rather in the architecture-specific section of the kernel. Different architectures implement the thread_info struct differently. While both the arm and risc-v version have preempt_count in their respective thread_info definitions, that is not the case for x86. In x86, preempt_count seems to have been abstracted away into macros: `preempt_count()`, `preempt_disable()`, and `preempt_enable()`.

A spinlock is held by the CPU, while a mutex is held by a task. With a spinlock, the CPU will be performing a certain number of
nops. With a mutex, the CPU is free to execute other tasks.
---
layout: post
title:  "Exploring the Linux Kernel"
date:   2025-01-19 12:09:08 -0700
categories: operating-systems linux
---

The definition of `task_struct` is in the file `include/linux/sched.h`. The `task_struct`, I assume, is the `proc` struct mentioned in the OSTEP book. The `task_struct` contains many members; the struct definition, including spaces and comments, is about 800 lines!

```c
...
unsigned int __state;

void *stack;
refcount_t usage;

int prio;

unsigned int policy;

const cpumask_t *cpus_ptr;
cpumask_t *user_cpus_ptr;
cpumask_t cpus_mask;

struct mm_struct *mm;
struct mm_struct *active_mm;
struct address_space *faults_disabled_mapping;

pid_t pid;
pid_t tgid;

struct fs_struct *fs;
struct files_struct *files;
...

```

I've listed above some of the important members that are not within an `#ifdef` block. For some of the members, I can guess their purpose from their name. For example, `stack` is a pointer to a process' stack. Both `mm` and `active_mm` must have something to do with the heap, if I had to guess. But what is `faults_disabled_mapping`? Also, heap memory may not be contiguous, so there must be multiple structs keeping track of a chunk of the heap. Is that within the definition of `mm_struct`?

I wonder why the task_struct needs to keep track of cpus and why there are three variables dedicated towards that purpose: cpus_ptr, user_cpus_ptr, cpus_mask.

I did not see anything about scheduling policy in `include/linux/sched.h`. Though, there is another file named `sched.h` in a different folder (`kernel/sched/sched.h`). Scheduling policies are mentioned in `include/uapi/linux/sched.h`, where the following constants are defined.

```c
#define SCHED_NORMAL		0
#define SCHED_FIFO		1
#define SCHED_RR		2
#define SCHED_BATCH		3
/* SCHED_ISO: reserved but not implemented yet */
#define SCHED_IDLE		5
#define SCHED_DEADLINE		6
#define SCHED_EXT		7
```

What would I need to do if I wanted to add a new scheduling policy?
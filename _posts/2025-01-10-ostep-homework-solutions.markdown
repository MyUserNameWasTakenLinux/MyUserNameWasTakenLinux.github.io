---
layout: post
title:  "OSTEP Homework Solutions"
date:   2024-11-19 23:09:08 -0700
categories: operating-systems
---

### CPU Intro

1. The CPU utilization will be 100%, since all the instructions are CPU instructions.

2. Going by how scheduling seems to work in the previous examples, it will take 4 cycles to complete the first process, and then 3 cycles to complete the second process: one cycle for running the io request, one cycle to block, and one cycle for io done. Both processes will complete in 7 cycles.

3. The first process blocks after initiating the io request and the second process starts running. While the first process is blocked, the second process runs. The first process is blocked for 5 cycles, and the second process finishes in 4 cycles. There's one last block cycle and then a io done cycle. That's a total of 6 cycles. The order switching matters because of the scheduling policy (run a process to completion if there are no io requests).

4. The first process will run for 7 cycles; the second state is going to be in a ready state during those cycles. After the first processes is finished running, the second process is going to run for 4 cycles. In total, it takes 11 cycles for the two processes to reach completion.
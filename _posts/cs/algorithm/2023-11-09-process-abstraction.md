---
title: "[OS] Process Abstraction"
date: 2023-11-09
categories: [CS, Algorithm]
tags: [Algorithm]
---

## What is a Process?

A *process* is a <span style="font-weight: bold; color: orange;">running program</span> in a computer. 

## Process - Address Space

Each *process* has its own address space. The address space consists of <span style="font-weight: bold; color: orange;">4 main parts</span>.

1. **Stack:** Stores local variables, arguments to be passed to a function, return address.
2. **Heap:** Stores dynamically allocated memory.
3. **Data:** Stores static and global variables.
4. **Code:** Stoes the code of the program.

## Process - Process States

There are <span style="font-weight: bold; color: orange;">5 essential</span> process states in a process execution life cycle.

1. **Initial:** process is created and memory is allocated.
2. **Ready:** process is in the ready queue waiting to be executed.
3. **Running:** process is being executed by cpu.
4. **Blocked:** process is waiting for an I/O operation to finish.
5. **Terminated (Zombie):** process has finsihed execution, but waiting for parent process to read the returned code.

## Process Control Block (PCB)

In order for the OS to control each process, it needs a <span style="font-weight: bold; color: orange;">process control block</span> to maintain infomration about a *process*.

Below are some **important** parts that the PCB includes:

1. **Process Id (PID):** Unique Id is assigned to each process.
2. **Program Counter:** Pointer pointing to the next instruction (address) that needs to be executed.
3. **Process State:** The current state of the process.
4. **Register Context:** Stores the content of the latest executed code before being moved out from running state.
5. **Scheduling Information:** Process priority, pointers to scheduling queues.

## Process Table

The OS needs a *process table* to manage all the PCB. The *process table* is a hash table where the key is the PID and the value is a pointer pointing to the PCB for that key. When a process finish execution, the PCB for that process will be removed from the *process table*.

## Process List Structures

The OS also has a *ready queue* and *block queue* that stores the processes that are waiting to be executed.

## Process Creation

In general, a *parent process* <span style="font-weight: bold; color: orange;">spawns</span> a *new process*. This *new process* is called a <span style="font-weight: bold; color: orange;">child process</span> and it can also create a new process, thus forming a tree.

In modern operating systems, when a *parent process* is terminated, the *child process* can proceed independently of the terminated parent process.

Here are the specific steps:

1. Assign a unique **PID** and **allocate memory**.
2. Put the process in the **ready queue**.
3. Initialize the **process control block**.
4. Put the process in the **ready queue**.

## Process Termination

A *process* can be terminated <span style="font-weight: bold; color: orange;">involuntarily:</span>

- *Parent process* terminates *child process*.
- A number of **error and faults** leading to termination of *process*.

After termination, the *child process* returns the <span style="font-weight: bold; color: orange;">termination status</span> to its *parent process*. The terminated process' resources are **de-allocated** afterwards.

## Zombie Process

A *process* that has terminated but the OS keeps the PCB for that *process*, so that the *parent process* can read information later. We call this a <span style="font-weight: bold; color: orange;">zombie process</span>.

## Suspending a Process

Unlike *blocking* where the process is **blocked** by <span style="font-weight: bold; color: orange;">internal activity</span> of a process, *suspending* comes from <span style="font-weight: bold; color: orange;">external activity</span>.

Suspending occurs to a process when:

1. User request.
2. Request by parent process.
3. OS suspends a **blocked process** to free up memory for another ready process.

## Signals

*Signals* also known as <span style="font-weight: bold; color: orange;">software interrupt</span> is used to notify a process that some event has occured.

1. **Synchronous Signal:** Triggered by current running process.
   - Illegal memory access, division by zero
2. **Asynchronous Signal:** Trigeered by external events.
   - Timer interrupt, parent process killing the child process
  
A *process* can decide whether to **catch**, **ignore**, and **mask** a signal.

1. **Catch:** Use OS's default action to handle the signal.
2. **Ignore:** Inform OS that it does not want to handle the signal.
3. **Masking:** Instruct the OS not to deliver signals of that type until the process clears the signal mask.

To respond to a particular signal, a process' PCB contains a pointer to a <span style="font-weight: bold; color: orange;">vector of signal handlers</span>. Each entry corresponds to the handler function for that **signal**.

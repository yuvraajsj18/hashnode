## Processes | Operating Systems

This article is an extension of [this article - what happens when you run a program](https://blog.yuvv.xyz/what-happens-when-you-run-a-computer-program), I suggest you read that first.

## Process Concept

- Process - a program in execution.

- A process is not just *program code*(AKA text section), it also includes:

  - the current activity represented by - 
    - Program Counter Value
    - Content of processor registers
  - Process stack (function parameters, local variables, and return address)
  - Data section(global variables)
  - Heap - Memory that is dynamically allocated during process run time. 

- *Program* is a **passive** entity, whereas a *process* is an **active** entity.

- If a user(multiple or single) invokes the same copy of the browser, these will be separate processes, despite belonging to the same passive entity.

  - Although the text segment of the processes of the same program is equivalent, the data, heap, and stack sections are different.

- **Summary**:

  **A program is not a process**; a *program* is a *passive* entity, such as a file containing a list of instructions stored on a disk(executable file), whereas a *process* is an *active* entity, with a *program counter* specifying the next instruction to *execute* and a set of *associated resources*.

  A *program becomes a process* when an executable file is *loaded into memory* either by double-clicking or writing a command.

  ![Process in memory](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/3_01_Process_Memory.jpg)

  ​															A Process in Memory

## Process State

- As a process executes, it changes **state** -
- *The state of a process is defined in part by the current activity of the process*.
- Each process may be in one of the following states:
  - **New** - The process is being created.
  - **Running** - Instructions are being executed.
    - At one moment, only one process can be in running state.
  - **Waiting** - The process is waiting for some event to occur. (such as an I/O completion or reception of a signal).
  - **Ready** - The process is waiting to be assigned to a processor.
  - **Terminated**: The process has finished execution.
- The states name are arbitrary and vary across OS, but the state they represent are found on all systems.
- **Many processes can be in the ready and waiting state.**

![Diagram of process state](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/3_02_ProcessState.jpg)



## Process Control Block

- Each process is represented in the OS by a Process Control Block(PCB) - also known as a task control block.
- It contains information associated with a specific process.
- Information Stored:
  - **Process State**: new, ready, running, waiting, terminated.
  - **Program counter**: address of next instruction to be executed.
  - **CPU registers**: Content of all CPU centric registers like accumulators, index register, stack pointers, etc must be saved when an interrupt occurs, to allow the process to be continued correctly afterward.
  - **CPU Scheduling Information**: This information includes process priority, scheduling queue pointers, and other scheduling parameters.
  - **Memory management information**: Information about the memory allocated to the process.
  - **Accounting information**: CPU used, clock time elapsed since the start, time limits.
  - **I/O status information**: I/O devices allocated to process, list of open files.

![image-20200830153603631](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/image-20200830153603631.png)

## Process Scheduling

- Maximize CPU use, quickly switch processes onto CPU for time-sharing.

- **Process scheduler** selects among available processes for the next execution on CPU.

- Maintains **scheduling queues** of processes

  - **Job queue** - set of all processes in the system.

  - **Ready queue** - set of all processes residing in main memory, ready and waiting to execute.

  - **Device queue** - set of all processes waiting for an I/O device. Each device has a device queue.

  - Process Migrate among the various queues.

  - These queues are generally stored as a *linked list*.

    - A ready queue header contains pointers to the first and final PCB on the list.
    - Each PCB includes a pointer field that points to the next PCB in the ready queue.

    ![image-20200830160739887](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/image-20200830160739887.png)

    - **Queueing Diagram**

      ![image-20200830161453407](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/image-20200830161453407.png)

      A new process is initially put in the ready queue. It waits there until it is selected for execution, or is **dispatched**. Once the process is allocated the CPU and is executing, one of the several events could occur:

      - The process could issue an I/O request and then be placed in an I/O queue.
      - The process could create a new subprocess and wait for the subprocess's termination.
      - The process could be removed forcibly from the CPU as a result of an interrupt, and be put back in the ready queue.
      - On termination, the process is removed from all queues and PCB and resources are deallocated.

### Schedulers

- **Short-term scheduler(or CPU scheduler)** - selects which process should be executed next and allocates CPU.

  - Sometimes the only scheduler in a system.
  - Short term scheduler is invoked **frequently** (milliseconds) => (must be fast)

- **Long-term scheduler(or job scheduler)** - selects which processes should be brought into the ready queue.

  - Long term scheduler is invoked infrequently (seconds, minutes) => (may be slow)
  - The long term scheduler controls the **degree of multiprogramming**(the number of processes in the main memory).

- Processes can be described as either:

  - **I/O bound process**: spends more time doing I/O than computation, many short CPU bursts.
  - **CPU bound process**: spends more time doing computations, few very long CPU bursts.

- *Long term scheduler strives for good process mix(there should be both I/O bound and CPU bound processes)*

- **Medium Term Scheduler** - It is required when long term scheduler did not bring a good mix of CPU and IO bound processes.

  - It decreases the degree of multiprogramming.
  - Removes process from memory, store on disk, bring back in from disk to continue execution: **swapping**.

  ![image-20200830203549955](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/image-20200830203549955.png)

### Context Switch

Switching the CPU to another process requires performing a state save of the current process and a state restore of a different process. This task is known as a **context switch**. 

When a context switch occurs, the kernel saves the context of the old process in its PCB and loads the saved context of the new process scheduled to run.

*Context switch time is pure overhead*: because the system does no useful work while switching.

The speed of context switch varies from machine to machine depending on memory speed, the number of registers, etc.

The more complex the OS, the more work must be done during a context switch.

![image-20200830204405120](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/image-20200830204405120.png)

## Operation on Processes

Systems must provide a mechanism for process creation and termination.

### Process Creation

- A process can create several new processes, via a **create process system call**, during execution.

  - The creating process is called a **parent** process.
  - The new processes are called the **children** processes.
  - Children's processes can create other processes forming a **tree** of processes.

- Processes are identified using a unique identifier integer number known as **process identifier(PID)**.

  - You can get a list of all processes by using the `ps -el` command on UNIX systems.
  - A tree of processes on a typical Solaris system - 

  ![Tree of processes](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/image-20200906115053765.png)

- A process needs certain resources(CPU time, memory, files, I/O devices) to do its task. When a process creates a subprocess, It will also need such resources.

  **Resource sharing options**:

  - Parent and children share all resources.
  - Children share a subset of parent's resources.
    - Parent have to partition its resources among its children.
    - Prevents any process from overloading the system by creating too many subprocesses.
  - Parent and child share no resources.
    - Subprocess obtains its resources directly from the Operating Systems.

- **Execution Options** when a subprocess is created:

  - Parent and children execute concurrently.
  - Parent waits until children terminate.

- **Address Space Options** for the new process:

  - The child process is a duplicate of the parent process. This means they have the same program and data as the parent).
  - The child process has a new program loaded into it.

#### Creating a new process in a UNIX OS

- A new process in UNIX is created using the `fork()` system call.
-  The new process consists of a copy of the **address space** of the original process.
- Both parent and child continue execution after fork() call with one difference - 
  - **The return code for fork() is 0 for the new child process.**
  - **The return code for fork() is the PID of the child for the parent process.**
- You can use the `exec()` system call after `fork()` to replace the process's memory space with a new program.
  - The `exec()` system call loads a binary file into memory(destroying the memory image of the program containing the exec()) and starts its execution.
- A parent can issue a `wait()` system call to move itself off the ready queue until the termination of the child.
  - `wait()` blocks the termination of the parent until one of the children terminates.

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main()
{
    pid_t pid = fork();

    if (pid < 0)    // error check
    {
        fprintf(stderr, "Fork failed\n");
        return 1;
    }

    if (pid == 0)   // child process
    {
        execlp("/mnt/DC84407A844058E2/CS/learn_cs/OS/workspace/practicals/processes/helloworld", "helloworld", NULL);
    }
    else
    {
        wait(NULL);
        printf("Child Complete\n");
    }
    

    return 0;
}
```

![image-20200906134749294](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/image-20200906134749294.png)

- To get the process id of a process or its parent you can use:
  - `getpid()`: returns PID of current process.
  - `getppid()`: returns PID of parent process.
- A process can execute multiple `fork()` call, in that case, the number of the process will be 2<sup>n</sup>. where n is the number of fork() calls. This count will also include the first parent process.
- The following example shows the creation of a process when three fork() calls are made.

![image-20200906140805022](https://github.com/yuvraajsj18/Operating-Systems/raw/master/notes/processes/processes.assets/image-20200906140805022.png)

### Process Termination

- The process executes the last statement and then asks the operating system to delete it using the `exit()` system call.

  - Returns **status data** from child to parent via `wait()`.
  - Process resources are deallocated by OS.

- The parent may terminate the execution of children processes using the `abort()` system call. Some reasons for doing so:

  - The child has exceeded allocated resources.
  - The task assigned to the child is no longer required.
  - The parent is exiting and the OS does not allow a child to continue if its parent terminates.

- Some OS does not allow a child to exists if its parent has terminated. If a process terminates, then all its children must also be terminated. This is known as **cascading termination.**

  - Termination is initiated by the OS.

- The parent process may wait for the termination of a child process by using the wait() system call. The call returns status information and the PID of the terminated process.

  ```c
  pid_t pid = wait(&status);
  ```

- If no parent is waiting (did not invoke `wait()` ) the process is a **zombie**.

- If the parent terminated without invoking `wait()`, the process is an **orphan.**

  - orphan processes are adopted by the `init` process.



---

Thanks


# Operating System — Concepts Q&A (Study Guide)
 
---
 
## 1. What is an Operating System (OS)?
 
**Q: What is an Operating System?**
An Operating System is system software that acts as an **intermediary between the user (or application programs) and the computer hardware**. It manages hardware resources (CPU, memory, I/O devices, storage) and provides a convenient, efficient environment for running programs.
 
Think of it as a **resource manager + traffic controller**: it decides who gets the CPU, how memory is allocated, and how I/O requests are handled — all while hiding the hardware complexity from the user.
 
---
 
## 2. Functions of OS
 
**Q: What are the main functions of an Operating System?**
 
1. **Process Management** — creating, scheduling, and terminating processes.
2. **Memory Management** — allocating/deallocating memory space as needed.
3. **File Management** — creating, deleting, reading, writing files; organizing directory structure.
4. **Device Management** — managing I/O devices via drivers, handling interrupts.
5. **Security & Protection** — preventing unauthorized access to resources.
6. **User Interface** — providing CLI or GUI for user interaction.
7. **Error Detection & Handling** — monitoring system for errors and handling them gracefully.
8. **Resource Allocation** — deciding how CPU, memory, and devices are shared among multiple processes.
---
 
## 3. Objectives of OS
 
**Q: What are the objectives of an Operating System?**
 
1. **Convenience** — make the computer easier to use for the end user.
2. **Efficiency** — ensure system resources are utilized optimally.
3. **Ability to Evolve** — allow new features to be added without disrupting services.
4. **Throughput** — maximize the number of processes completed per unit time.
*(Simple way to remember: an OS balances being User-friendly, Resource-efficient, and Scalable.)*
 
---
 
## 4. Operating System Structure
 
**Q: What are the different types of OS structures?**
 
| Structure | Description |
|---|---|
| **Simple/Monolithic Structure** | Entire OS runs as a single program in kernel mode; no strict internal structure (e.g., early MS-DOS). Fast but hard to maintain. |
| **Layered Structure** | OS divided into layers, each built on top of the lower one. Each layer only uses functions of the layer below it. Easier debugging, but slower due to layer-to-layer calls. |
| **Microkernel Structure** | Only essential functions (process/memory management, IPC) stay in the kernel; everything else (file systems, drivers) runs as user-space services. More secure and modular, but more overhead due to message passing. |
| **Modular / Loadable Kernel Modules** | Kernel has a core set of components, and other services are added as loadable modules at runtime (e.g., modern Linux, macOS). Flexible and efficient. |
| **Client-Server (Microkernel-based) Model** | Kernel acts as a message-passer between client processes and server processes providing services. |
 
---
 
## 5. System Call
 
**Q: What is a system call?**
A system call is the **programming interface** through which a user program requests a service from the OS kernel — e.g., reading a file, creating a process, or allocating memory.
 
**Q: Why are system calls needed?**
Because user programs run in **user mode** (restricted) and cannot directly access hardware resources for safety/security reasons. A system call causes a **mode switch from user mode to kernel mode**, allowing the OS to safely perform the privileged operation on behalf of the program.
 
**Common categories:**
- Process control (`fork()`, `exit()`)
- File management (`open()`, `read()`, `write()`)
- Device management (`ioctl()`)
- Information maintenance (`getpid()`, `time()`)
- Communication (`pipe()`, `send()`, `recv()`)
---
 
## 6. Process
 
**Q: What is a process?**
A process is a **program in execution** — it includes the program code, current activity (represented by the value of the Program Counter), stack, data section, and heap.
 
**Q: What are the states of a process?**
1. **New** — process is being created.
2. **Ready** — waiting to be assigned to a processor.
3. **Running** — instructions are being executed.
4. **Waiting/Blocked** — waiting for some event (like I/O completion).
5. **Terminated** — finished execution.
```
New → Ready → Running → Terminated
              ↕
           Waiting
```
 
---
 
## 7. Context Switching
 
**Q: What is context switching?**
Context switching is the process of **saving the state (context) of a currently running process** and **loading the saved state of another process** so the CPU can switch execution between them.
 
**Q: What does "context" include?**
- Program Counter (PC)
- CPU registers
- Process state
- Memory management info (page tables etc.)
**Q: Why does it matter?**
Context switching enables **multitasking**, but it has **overhead** — no useful work is done during the switch itself, since the CPU is just saving/restoring states. Too many context switches can hurt performance ("thrashing" of the CPU between tasks).
 
---
 
## 8. PCB (Process Control Block)
 
**Q: What is a PCB and what does it contain?**
A PCB is a data structure maintained by the OS for **every process**, storing all the information needed to manage and resume that process.
 
**Contents of PCB:**
- Process ID (PID)
- Process State (new, ready, running, waiting, terminated)
- Program Counter
- CPU Registers
- CPU Scheduling info (priority, pointers to scheduling queues)
- Memory Management info (base/limit registers, page tables)
- I/O status info (list of I/O devices allocated)
- Accounting info (CPU used, time limits)
Think of the PCB as the process's **"identity card"** — the OS uses it to know exactly where to resume the process after a context switch.
 
---
 
## 9. Starvation
 
**Q: What is starvation in OS?**
Starvation occurs when a process is **perpetually denied the resources it needs** to proceed — usually because other higher-priority processes keep getting scheduled ahead of it.
 
**Example:** In Priority Scheduling, a low-priority process may never get the CPU if higher-priority processes keep arriving continuously.
 
---
 
## 10. Aging
 
**Q: What is aging, and how does it solve starvation?**
Aging is a technique where the **priority of a waiting process is gradually increased** the longer it waits. Eventually, its priority becomes high enough that it gets scheduled — preventing indefinite starvation.
 
*(Simple analogy: the longer you wait in line, the more "VIP" you become, until you're guaranteed to be served.)*
 
---
 
## 11. CPU Scheduling Algorithms (Conceptual Overview)
 
**Q: What is CPU Scheduling?**
CPU scheduling is the process by which the OS decides **which process in the ready queue gets the CPU next**.
 
| Algorithm | Type | Key Idea |
|---|---|---|
| **FCFS (First Come First Serve)** | Non-preemptive | Processes are executed strictly in order of arrival. Simple but can cause the "convoy effect" (short processes wait behind long ones). |
| **SJF (Shortest Job First)** | Non-preemptive | Picks the process with the smallest burst time next. Minimizes average waiting time, but requires knowing burst times in advance; can starve long processes. |
| **SRTF (Shortest Remaining Time First)** | Preemptive version of SJF | If a new process arrives with a shorter remaining time than the current one, it preempts. More optimal but higher overhead (frequent switching) and can starve long processes even more. |
| **Round Robin (RR)** | Preemptive | Each process gets a fixed time quantum in turn; if not finished, it goes to the back of the queue. Fair and good for time-sharing systems, but performance depends heavily on quantum size (too small → high overhead; too large → behaves like FCFS). |
| **Priority Scheduling** | Preemptive or Non-preemptive | Each process is assigned a priority; higher priority runs first. Can cause **starvation** for low-priority processes (fixed with **aging**). |
 
**Q: Which algorithm minimizes average waiting time?**
SJF/SRTF theoretically gives the minimum average waiting time among non-preemptive/preemptive algorithms respectively — but at the cost of needing to predict burst times and potential starvation of longer jobs.
 
---
 
## 12. Multiprogramming
 
**Q: What is multiprogramming?**
Multiprogramming is when **multiple programs reside in memory at the same time**, and the CPU switches between them so that it's never idle — whenever one process is waiting for I/O, the CPU picks up another ready process.
 
**Goal:** Maximize CPU utilization.
 
---
 
## 13. Multitasking
 
**Q: What is multitasking, and how is it different from multiprogramming?**
Multitasking extends multiprogramming by adding **time-sharing** — the CPU switches between tasks so fast (using small time slices) that it *appears* multiple tasks are running simultaneously from the user's perspective.
 
| | Multiprogramming | Multitasking |
|---|---|---|
| Focus | Maximize CPU utilization | Provide fast response time to users |
| Switching | Happens when a process needs I/O | Happens after a fixed time quantum, even if the process could keep running |
| User experience | User may not perceive true "parallelism" | Feels like simultaneous execution |
 
---
 
## 14. Basic Architecture of Computer System / OS
 
**Q: What are the main hardware components an OS manages?**
 
```
 ┌─────────────────────────────────────────┐
 │                  USERS                   │
 └───────────────────┬───────────────────────┘
                      │
 ┌────────────────────▼───────────────────────┐
 │        Application Programs (Software)      │
 └────────────────────┬───────────────────────┘
                      │  System Calls
 ┌────────────────────▼───────────────────────┐
 │             OPERATING SYSTEM                 │
 │  (Process Mgmt | Memory Mgmt | File Mgmt |   │
 │   Device Mgmt | Security)                    │
 └────────────────────┬───────────────────────┘
                      │
 ┌────────────────────▼───────────────────────┐
 │         COMPUTER HARDWARE                     │
 │  (CPU | Memory | I/O Devices | Storage)      │
 └───────────────────────────────────────────────┘
```
 
**Layers explained:**
- **Hardware** — CPU, RAM, disk, I/O devices — the physical resources.
- **Operating System** — sits directly above hardware, manages and abstracts it.
- **System Call Interface** — the boundary/API through which application programs request OS services.
- **Application Programs** — user-facing software (browsers, editors, games) that use OS services indirectly.
- **Users** — interact with applications, not hardware directly.
---
 
## 15. IPC (Inter-Process Communication)
 
**Q: What is IPC, and why is it needed?**
IPC refers to the mechanisms an OS provides that allow **processes to communicate and synchronize their actions**, whether they're running on the same machine or across a network.
 
**Q: Why is IPC needed?**
1. **Information sharing** — multiple processes may need access to the same piece of data.
2. **Computation speedup** — breaking a task into sub-tasks (parallel processes) that run faster together, but they need to coordinate.
3. **Modularity** — dividing system functions into separate processes that communicate as needed, rather than one giant process.
4. **Convenience** — a user may want to perform many tasks at once (edit, print, compile) that need to coordinate or share resources.
**Common IPC mechanisms:**
- **Shared Memory** — processes read/write to a common memory region (fast, but needs synchronization).
- **Message Passing** — processes exchange messages via the OS (slower, but no need for shared address space; safer for distributed systems).
- Pipes, sockets, signals are also used.
---
 
## 16. Race Condition
 
**Q: What is a race condition?**
A race condition occurs when **two or more processes/threads access shared data concurrently**, and the final outcome **depends on the timing/order of execution** — leading to unpredictable or incorrect results.
 
**Example of a race condition:**
 
Imagine two threads incrementing a shared variable `count = 5`:
 
```c
// Shared variable
int count = 5;
 
// Thread A                  // Thread B
temp = count;   // temp = 5  temp = count;   // temp = 5
temp = temp+1;  // temp = 6  temp = temp+1;  // temp = 6
count = temp;   // count=6   count = temp;   // count=6
```
 
If both threads read `count` **before** either writes it back, both compute `6`, and the final value is `6` — even though two increments happened. The correct answer should have been `7`. This lost update is the race condition.
 
**How to minimize/avoid race conditions:**
1. **Mutual Exclusion (Locks/Mutexes)** — only one process/thread can enter the critical section at a time.
2. **Semaphores** — counting or binary signaling mechanism to control access.
3. **Atomic Operations** — hardware-supported instructions (like `test-and-set` or `compare-and-swap`) that complete without interruption.
4. **Monitors** — high-level synchronization construct that combines mutual exclusion with condition variables.
**Example fix using a mutex (pseudocode):**
 
```c
mutex lock;
 
// Thread A and Thread B both do:
lock.acquire();
count = count + 1;   // now safe, no other thread can interleave here
lock.release();
```
 
---
 
## 17. Busy Waiting
 
**Q: What is busy waiting?**
Busy waiting (or "spinning") is when a process **repeatedly checks a condition in a loop** while waiting for it to become true, instead of being put to sleep — wasting CPU cycles the whole time.
 
```c
while (lock == 1) {
    // do nothing, just keep checking (busy wait)
}
lock = 1;
// enter critical section
```
 
**Why it's a problem:** The CPU is kept "busy" doing nothing useful, which is wasteful — especially in a single-CPU system where the waiting process is preventing other useful work.
 
**Alternative:** Use **blocking synchronization primitives** (like semaphores with sleep/wakeup) so the waiting process is put to sleep and the CPU is freed for other work until it's woken up.
 
---
 
## 18. Critical Section
 
**Q: What is a critical section?**
A critical section is a segment of code where a process **accesses shared resources** (like shared variables, files, or data structures) that **must not be concurrently accessed by more than one process** at a time, to avoid inconsistent results.
 
**Q: What are the requirements for a correct critical-section solution?**
1. **Mutual Exclusion** — only one process may execute in its critical section at a time.
2. **Progress** — if no process is in the critical section, one of the processes waiting to enter must be allowed to proceed (no indefinite postponement).
3. **Bounded Waiting** — there must be a limit on how many times other processes can enter their critical section before a waiting process gets its turn (prevents starvation).
**General structure of critical-section handling:**
```c
// entry section
acquire_lock();
 
// critical section
// (access shared resource)
 
// exit section
release_lock();
 
// remainder section
```
 
---
 
## Quick Revision Table
 
| Term | One-Line Definition |
|---|---|
| OS | Software that manages hardware and provides services to programs |
| System Call | Interface for programs to request OS services |
| Process | A program in execution |
| PCB | Data structure holding all info about a process |
| Context Switch | Saving/restoring process state to switch CPU between processes |
| Starvation | A process indefinitely denied resources |
| Aging | Gradually increasing priority to prevent starvation |
| Multiprogramming | Multiple programs in memory to keep CPU busy |
| Multitasking | Rapid switching to give illusion of simultaneous execution |
| IPC | Mechanisms for processes to communicate/synchronize |
| Race Condition | Outcome depends on timing of concurrent access to shared data |
| Busy Waiting | Repeatedly checking a condition in a loop, wasting CPU |
| Critical Section | Code segment accessing shared resources, needs exclusive access |
 
---
 
*Tip for exams: for any definition-based question, try to give (1) a one-line definition, (2) a real example, and (3) why it matters/what problem it solves. That structure covers full marks in most OS theory questions.*

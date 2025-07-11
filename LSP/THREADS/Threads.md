# Introduction
### Process:
A process is an independent program in execution, with its own address space, code, data, and system resources. 
It's managed by the operating system throw PCB, and assigns a Process ID (PID) and isolates it from other processes to ensure memory safety and stability

### Thread:
A thread is the smallest unit of execution within a process. Threads share the same memory of Code Segment, Heap Memory, Global/Static Varibles and FD table space but run independently, its has own stack memory, Entry point, context info, CPU time and registers.

### Multi-threading:
Multipull threads run under a single process is called as multi-threading. They share memory of Code Segment, Heap Memory, Global/Static Varibles and File Descripter and have seprate Stack Merory & Registers, execute independently and  This enables efficient communication and resource sharing compared to multiprocessing

![image](https://github.com/user-attachments/assets/3130b776-e385-4678-b418-f9c223c85440)

```
Q 1) What is the Differance between Thread and a process?
Q 2) How do threads share memory? 
Q 3) What are the difference between child process and thread?
Q 4) What are the commands use to see the threads?
A. ps -eLf                // Shows threads per process
   ps -ef		  // To see kernel threads
   top -H                 // Displays threads in real-time
   cat /proc/<pid>/task/  // Lists thread IDs for a process
```
### Supporting Languages
1) C/C++: Provides low-level threading capabilities through libraries POSIX threads(pthreads)

2) Python: Offers by the threading module, It provides a higher‑level, object‑oriented interface over the lower‑level _thread module

3) Java: Java treats every concurrent task as a Thread (or indirectly via Runnable/Callable),
```
Q 5) How Python threads Differ from C threads?
A)# 🧵 Python Threads vs C Threads
## 🐍 Python Threads
- Uses the built-in threading module.
- Limited true parallelism due to the Global Interpreter Lock (GIL).
- More suitable for I/O-bound tasks.
## C Threads (POSIX Threads)
- Uses pthread library for low-level thread creation.
- Supports true parallelism across CPU cores.
- Ideal for CPU-bound tasks and systems programming.

Q 6) How C++ threads Differ from C threads?
A)##Key differance:
- C threads require manual handling via platform-dependent APIs (e.g., POSIX), while C++ threads are part of the language standard.
- C++ threads are object-oriented and easier to manage with RAII principles.
- C++ offers higher-level utilities like std::mutex, std::lock_guard, and std::async.

***C Threads***
- C uses POSIX threads (pthreads), which are low-level APIs providing direct control over thread behavior.
- Requires manual management of thread creation, joining, and synchronization.
- Provides flexibility but is more verbose and error-prone

***C++ Threads***
- Introduced with C++11 via the <thread> header, offering a high-level and object-oriented abstraction.
- Simplifies thread management using RAII principles (Resource Acquisition Is Initialization). 
- Integrates well with C++ standard library features like std::mutex, std::future, and std::async.

```
# Use of Multithreading
- Parallel Processing
- Faster Execution on Multi-core Systems
- Efficient Resource Utilization
- Speed up I/O-bound programs (e.g., file reading, network requests)
- Improve responsiveness

```
Q 7) How Multithreading help in fast Execution?
```
# Applications
- Web servers (e.g., handling multiple client requests simultaneously)

- Video games (e.g., separate threads for rendering, physics, and input)

- Download managers (e.g., splitting files into parts to download in parallel)

- Banking systems (e.g., processing concurrent transactions safely)

- Machine learning/data processing (e.g., processing data batches in parallel)

```
Q 8) How Threads use in Web pages?
A. Threads are essential for enabling concurrency in both backend and frontend web applications.
They allow servers to handle multiple client requests efficiently and browsers to offload intensive tasks,
 keeping the UI smooth. This concurrency model is fundamental to building scalable and responsive systems.

```

# Creation of thread
## Create function: 
1) pthread_t:
- To create a thread 1st insilize a thread variable with **pthread_t**,
- pthread_t is a data type of **typedef unsigned long int** (typedef unsigned long int pthread_t), its actual layout is hidden. It may be an integer, pointer, structure, or union depending on the system(Linux, windows).
- The size of pthread_t is platform dependent, On 64-bit Linux systems, pthread_t is often 8 bytes and in 32-bit systems, it might be 4 bytes.
- Inshaly pthread_t variable contains garbage, it contains a valid information when pthread_create exeguate sucessfull.
- The pthread_t varable uses in subsequances opearations,
```
Q 9) can we use thread varable as *p insted of p?
A.If p is an uninitialized pointer, then *p doesn’t point to valid memory. When pthread_create() tries to write the
thread ID into *p, it causes undefined behavior—typically a segmentation fault—because the destination is invalid.
 Always ensure that p points to a valid pthread_t variable before dereferencing.
```
examples
```c
pthread_t *p;  
pthread_create(p, NULL, thread_func, NULL);  // ❌ Leads to crash  
```
```c
pthread_t t1;  
pthread_t *p = &t1;  
pthread_create(p, NULL, thread_func, NULL);  // ✅ Safe, valid pointer
```

2) pthread_create():
- For creation of thread use pthread_create() libeary function,
- pthread_create() is a data typpe of **int**
- pthread_create()  used to create a new thread, It allows program to run multiple tasks concurrently by launching a
new thread that executes a specified  function, 
- when pthread_create() invock it overwrites a valid address to the thread varable, and tells the system to create new
thread and write its unique ID into the memory location and make entry in thread table,
- after invock of pthread_create( ) a thread will create and next controle goes to pthread_join()

```c
 int pthread_create(pthread_t *thread, const pthread_attr_t *attr, void *(*start_routine)(void *), void *arg);
```

```
🧩 Arguments Explained:-

| Argument          | Description | 
|-------------------|-------------|
| pthread_t *thread | Pointer to a pthread_t variable where the ID of the new thread will be stored. | 
| const pthread_attr_t *attr | Specifies thread attributes like stack size, scheduling, etc. Use NULL for default attributes. | 
| void *(*start_routine)(void *) | Pointer to the function the thread should execute. The function should take a void* argument and return a void*. | 
| void *arg | Argument passed to the start_routine function. Can be a pointer to any data structure or NULL. | 

✅ Return Value
- Returns 0 on success.
- On failure, returns an error number (non-zero) indicating what went wrong.

🧩 Thread Table:
The thread table is a data structure maintained by the operating system kernel to keep track of all active threads in the system. Think of it as a registry or ledger where each thread gets a row with its vital stats.
Each entry typically includes:
- Thread ID (pthread_t)
- Program counter
- Stack pointer
- Register set
- Thread state (ready, running, blocked, etc.)
- Scheduling info (priority, CPU affinity)
- Parent process ID

 When Does the Thread Table Get Filled?
- At thread creation: When you call pthread_create(), the kernel allocates a new entry in the thread table for that thread.
- During system boot: Some threads (like kernel threads or background daemons) are registered early.
- As new threads spawn: Each new thread gets its own entry until the system hits a limit (like ulimit -u in Linux).

🧠 Why Is the Thread Table Useful?
| Purpose | Benefit | 
|---------|---------|
| Scheduling | Helps the OS decide which thread to run next | 
| Resource management | Tracks memory, CPU usage, and stack allocation | 
| Debugging | Tools like GDB or top use it to show thread info | 
| Synchronization | Enables locking, signaling, and coordination between threads | 
| Cleanup | Ensures proper termination and resource release when threads exit | 
```
3 ) Thread function:
A thread function (also known as start_routine) is the entry point your new thread runs when created with pthread_create()
Function syntax:
```c
	void* fun_name(void* args)
```
- void *arg: Accepts a generic pointer accepts any data into the thread. pass a pointer to a struct or variable,
- void * return: Thread return any pointer-sized result. If don't need a return value, can return NULL.
- return valu will refer to the pthead_join().


4 ) pthread_join():
- pthread_join() is used to wait for a specific thread to finish before the calling thread continues. It’s a synchronization tool that ensures orderly execution in multithreaded programs.

```c
      int pthread_join(pthread_t thread, void **retval);
```
- - thread: The thread ID you want to wait for (usually returned by pthread_create()).
- retval: A pointer to a void* where the thread’s return value will be stored. You can pass NULL if you don’t care about the return value.

Working: 
- You create a thread using pthread_create().
- The thread starts executing its function.
- Meanwhile, the main thread calls pthread_join() with the thread’s ID.
- The main thread blocks—it pauses until the target thread finishes.
- Once the target thread exits, pthread_join() returns, optionally giving you the thread’s return value.

 pthread_join() Return Value
- Returns 0 on success.
- Non-zero error code on failure (e.g., ESRCH, EINVAL, EDEADLK).
  
The conditions for failure of pthread_joinn():
- Non-zero → Error code:
- ESRCH: No thread with the given ID.
- EINVAL: Thread is not joinable or already joined.
- EDEADLK: Deadlock detected (e.g., a thread trying to join itself). wxplain this part clearly
```
Q 10)  can we use sleep() instead of pthead_join()?
A. No we can't use sleep() in place of pthread_join(), for small applications sleep() may wrok but it not good for real time applications because
- The thread might take longer than expected, and sleep() will end too early.
- Or the thread might finish quickly, and sleep() wastes time unnecessarily.
- You risk resource leaks if the thread isn’t joined properly.
- In complex programs, this leads to race conditions, zombie threads, or undefined behavior
```

```c
Exaple code:
#include <stdio.h>
#include <pthread.h>
int counter = 0;
void* increment(void* arg) {
    for (int i = 0; i < 5; i++) {
        counter++;
        printf("Thread %d: Counter = %d\n", *(int*)arg, counter);
    }
    return NULL;
}
int main() {
    pthread_t t1;
    int id1 = 1;
    pthread_create(&t1, NULL, increment, &id1);

    pthread_join(t1, NULL);
    printf("Final Counter Value: %d\n", counter);
    return 0;
}
```
# Exeguation 
## 1. Thread Creation Process
- When a thread is created using 'pthread_create()', it internally invokes the 'clone()' system call to create a new thread that shares resources with the main process.
- This newly created thread operates independently, with its own stack memory and registers, but within the same virtual address space.
- The 'pthread_create()' function initializes the thread variable by replacing its default garbage value with a valid memory address pointing to the newly created thread's metadata.

## 2. Thread Variable and Thread Table
- Once a valid thread is created, the system maintains its metadata in a thread table, which contains details like thread ID, state, resources, and execution context.
- This table allows the kernel to manage thread resources and monitor thread lifecycles.

## 3. Thread Execution Flow
- The thread begins executing its task independently in its own stack space.
- After finishing its task, the thread returns a result or NULL to the calling thread (usually the main thread).

## 4. Synchronizing with pthread_join()
- To ensure that the main thread waits for a worker thread to complete before proceeding, we use the pthread_join() function.
- pthread_join() blocks the execution of the main thread until the specified child thread has finished execution

## 5. Termination Behavior
- If the main thread completes before the other threads, it leads to premature termination of remaining threads.
- This happens because thread stack regions are cleaned up when the entire application exits.
- Hence, to avoid unexpected thread termination, we use pthread_join() on each worker thread that must finish before the program exits
```
Q 11) What is clone() system call ?
A. The clone() system call is used to create a new task—either a thread or a process—depending on the flags passed.
Unlike fork(), which creates a completely separate process, clone() allows the child to share parts of its execution context with the parent.

Q 12) How clone() related to pthread_create() ?
A. When you use pthread_create(), it internally wraps around clone() with flags like: CLONE_VM, CLONE_FS, CLONE_FILES,
CLONE_SIGHAND, CLONE_THREAD.
- CLONE_VM: Share memory space with parent,
- CLONE_FS: Share filesystem info,
- CLONE_FILES: Share file descriptors,
-  CLONE_SIGHAND: Share signal handlers,
- CLONE_THREAD: Group child into the same thread group,
This creates a thread that shares memory and resources with the main thread, allowing concurrent execution in the same address space.
Q 13) Do threads use CPSR/SPSR Registers?
A) CPSR/SPSR are essential for low-level thread context switching
In user-space threading (e.g., pthreads), CPSR and SPSR are not directly accessed or modified. These registers are privileged and relate to
processor-specific state, which is managed entirely by the operating system through system calls and context switching mechanisms that are
abstracted from the user. Since user-space threads run in User mode, they cannot access these registers due to security restrictions.
However, in kernel-space threads — such as those in an RTOS or during low-level OS context switches — CPSR and SPSR are essential. They are
used to save and restore the processor state during context switches, interrupt handling, and mode transitions (e.g., from IRQ to Supervisor mode).
This ensures that each thread or process resumes with the correct flags, mode, and interrupt state


Q 14) Is thare any other way or system call to create thread insted of using pthread_create() ?
A. Yes, in C, while pthread_create() is the standard POSIX way to create threads, there are a few
lower-level or alternative approaches depending on your system-level.
# 🧵 Alternatives to `pthread_create()` in C

## 1. `clone()` System Call
- Directly used by `pthread_create()` under the hood.
- Offers fine-grained control over what resources are shared (e.g., memory, file descriptors).
- Requires manual stack allocation and careful setup.
- Ideal for custom thread libraries or container runtimes.

## 2. `vfork()` or `fork()` + Shared Memory
- Not true threading but can mimic concurrent behavior.
- Processes created with `fork()` are isolated, but can communicate using shared memory mechanisms (`mmap`, `shmget`, etc.).
- Useful in embedded systems where POSIX threads may not be available.

## 3. Third-Party Thread Libraries
- Some embedded platforms or real-time operating systems (RTOS) offer their own threading APIs.
- **Examples:**
  - FreeRTOS : use xTaskCreate()
  - Zephyr threads: uses k_thread_create() for dynamic and K_THREAD_DEFINE() for static
  - CMSIS-RTOS for ARM Cortex systems: osThreadNew() (CMSIS-RTOS v2)

## 4. Custom Thread Abstractions
- Build your own lightweight threading system using `clone()` with custom signal handling.
- Suitable for educational purposes or highly specialized systems.

```
# Considerations Issues
1. ***Global data corruption:*** When two or more threads access and modify global data at the same time, and the access is not controlled properly (no lock, mutex, etc.), the data can get corrupted

2. ***Race conditions:*** A race condition occurs when two or more threads (or processes) access shared data at the same time, and the final result depends on the timing or order of execution.
Because the threads are "racing" to read or write the same data, the outcome becomes unpredictable and may lead to bugs, crashes, or corrupted data

3. ***Deadlocks:*** A deadlock occurs when two or more threads (or processes) are waiting for each other to release resources, and none of them can proceed.

4. ***LiveLock:*** A livelock is a situation in concurrent programming where two or more threads keep changing their state in response to each other, but fail to make any actual progress. Unlike a deadlock, where threads are stuck waiting, in a livelock, threads are actively running, but constantly yielding or retrying, which prevents them from completing their tasks.
```
Q 15) What are Simial Problems in Threads and process ?
A. Similar Problems in Threads and Processes are: 
- Deadlocks – Both can get stuck waiting for resources held by each other.
- Race Conditions – Unsynchronized access to shared resources leads to unpredictable behavior.
- Resource Leaks – Improper cleanup of memory, file descriptors, or handles.
- Priority Inversion – Lower-priority tasks block higher-priority ones due to resource dependencies.
- Starvation – Some tasks may never get CPU time due to scheduling policies.
- Improper Synchronization – Missing or incorrect use of locks, semaphores, or signals.
- Context Switching Overhead – Frequent switching can degrade performance.
- Signal Handling Conflicts – Misrouted or mishandled signals can disrupt execution.
- Stack Overflow – Deep recursion or large local variables can crash execution.
- Termination Issues – Improper exit handling can leave zombie threads or processes.

```
# Synchronization and locking mechanism
1. ***Mutexes:*** A mutex, short for mutual exclusion, is a synchronization primitive used to protect shared resources in a multithreaded environment. It ensures that only one thread at a time can access a critical section of code. When a thread locks a mutex, any other thread that tries to lock it will be blocked until the mutex is released. 
This prevents race conditions and data corruption when multiple threads interact with shared data

2. ***Semaphores:*** A semaphore is a synchronization tool used to control access  to a shared resource by multiple threads. It works using a counter that represents the number of available resources or permits. 

3. ***Condition Variable:***  A Condition Variable is a synchronization primitive that allows threads to wait for certain conditions to become true, while releasing the associated lock during the wait.
It’s commonly used when a thread needs to pause until a specific condition is met, such as waiting for a shared resource to become available or for a queue to be non-empty.

4. ***Spinlocks:*** A spinlock is a type of lock used in multithreading to protect shared resources. Unlike regular locks where a thread might go to sleep if it can't acquire the lock, a spinlock “spins” in a loop, continuously checking if the lock is available.
This means the thread stays active and consumes CPU cycles while waiting. Spinlocks are generally used in low-level systems programming or in situations where the lock is expected to be held for a very short time, because avoiding context switching can make things faster. However, they can be inefficient on single-core systems or when the lock is held too long, as they waste CPU time by busy-waiting.

5. ***TryLock:*** A TryLock is a non-blocking version of a lock. When a thread attempts to acquire a lock using TryLock, it tries once and immediately returns with either success or failure, instead of waiting if the lock is already held by another thread. This is useful in situations where a thread should not be blocked and instead wants to perform other tasks or retry later if the resource is not immediately available.
   
6. ***Read-copy-update(RCU):*** Read-Copy-Update (RCU) is a high-performance synchronization mechanism used primarily in multithreaded environments like the Linux kernel. It’s designed to allow multiple readers to access shared data concurrently without blocking, while still enabling safe updates by writers

7. ***Atomic operations:*** Atomic operations in threads are indivisible actions that ensure safe access to shared data without interference from other threads. They're a cornerstone of thread-safe programming, especially in concurrent environments like embedded systems or kernel-level code.


# For destroy:
 destroy() functions in the pthreads family are use to relise the resourace if block at any thread and destroy function is use at the end of the exeguation its not a mandatory function to use
 
-> pthread_mutex_destroy() : - It destroys a mutex object (pthread_mutex_t) and releases any system resources associated with it.
	- After destruction, the mutex becomes uninitialized and must not be used unless reinitialized with pthread_mutex_init().
	- The mutex must be unlocked and not in use by any thread when you destroy it.
	- Destroying a locked or referenced mutex leads to undefined behavior.
	- After destruction, using the mutex without reinitializing it is also undefined
  	- Returns 0 on success.
	- Returns EINVAL if the mutex is invalid.
	- Returns EBUSY if the mutex is still locked or in use.

```c
pthread_mutex_destroy(pthread_mutex_t *mutex)
```
-> pthread_cond_destroy() :- It destroys a condition variable (pthread_cond_t) and releases any resources allocated to it by the system.
	- After destruction, the condition variable becomes uninitialized and must not be used unless reinitialized with pthread_cond_init()
	- You must ensure no threads are waiting on the condition variable (via pthread_cond_wait() or pthread_cond_timedwait()) when you destroy it.
	- Destroying a condition variable that’s still in use leads to undefined behavior
	- Returns 0 on success.
	- Returns EINVAL if cond is invalid or uninitialized.
	- Returns EBUSY if threads are still blocked on the condition variable.

 ```c
	 pthread_cond_destroy(pthread_cond_t *cond)
```
-> pthread_rwlock_destroy(): Destroys a read-write lock 
	 - After destruction, the lock becomes invalid and must not be used unless reinitialized with pthread_rwlock_init().
	- Must not be held by any thread (neither read nor write locked) when destroyed.
	- Must be initialized before destruction—either dynamically via pthread_rwlock_init() or statically with PTHREAD_RWLOCK_INITIALIZER.
	- Undefined behavior occurs if you destroy a lock that’s still in use or uninitialized.
	- Returns 0 on success.
	- Returns error codes like EBUSY or EINVAL on failure.
syntax:
```c
pthread_rwlock_destroy(pthread_rwlock_t *rwlock)
```
-> pthread_attr_destroy(): - It’s used to destroy a thread attribute object (pthread_attr_t) that was previously initialized with pthread_attr_init().
	- This function frees any resources allocated for the attribute object.
	- It does not affect any threads that were created using that attribute object
 	- After calling pthread_attr_destroy(), the attr object becomes invalid.
	- You must not reuse it unless you reinitialize it with pthread_attr_init().
	- Destroying the attribute object is safe even after threads are created with it—it doesn’t affect those threads
 	- Returns 0 on success.
	- Returns EINVAL if attr is invalid or uninitialized.
syntax:
```c
pthread_attr_destroy(pthread_attr_t *attr)
```
-> pthread_barrier_destroy():- It destroys a barrier object (pthread_barrier_t) and frees any system resources allocated to it.
	- After destruction, the barrier becomes invalid and must not be used unless reinitialized with pthread_barrier_init().
	- No thread should be waiting at the barrier (i.e., inside pthread_barrier_wait()) when you call pthread_barrier_destroy().
	- Destroying a barrier that’s still in use leads to undefined behavior.
	- Once destroyed, the barrier must not be reused unless reinitialized.
	- Returns 0 on success.
	- Returns EINVAL if the barrier is invalid or uninitialized.
	- Returns EBUSY if threads are still blocked on the barrier.
```c
pthread_barrier_destroy(pthread_barrier_t *barrier)
```

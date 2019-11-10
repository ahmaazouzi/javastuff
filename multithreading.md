## Intro:
- There are two types of multitasking, *process-based*, and *thread-based.* Multi-processing allows an operating system to run multiple programs concurrently, while multi-threading allows a single program to have multiple paths of execution. The *thread* is the smallest unit of dispatchable code. Multi-processing is slow and chunky, while multi-threading flies and is easy on the available resources.
- The basic premise of multi-threading is its magic ability to minimize idle time. I/O is much slower than the processing power of modern computers. Instead of halting altogether while waiting for slow I/O operations, a program can have some threads wait for the data while others process other tasks.

## Java Threads:
- *Event-looping* with *polling* is the alternative to mult
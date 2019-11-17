## Intro:
- There are two types of multitasking, *process-based*, and *thread-based.* Multi-processing allows an operating system to run multiple programs concurrently, while multi-threading allows a single program to have multiple paths of execution. The *thread* is the smallest unit of dispatchable code. Multi-processing is slow and chunky, while multi-threading flies and is easy on the available resources.
- The basic premise of multi-threading is its magic ability to minimize idle time. I/O is much slower than the processing power of modern computers. Instead of halting altogether while waiting for slow I/O operations, a program can have some threads wait for the data while others process other tasks.

## Java Threads:
- **Event-looping** with **polling** is the alternative to multi-threading. A single thread of control runs in an infinite loop checking an event queue. When this thread is busy with a certain action, it blocks. The whole system has to wait to do anything. *(I know, terrible English).* In a multi-threaded environment the system doesn't have to wait for a single thread to **unblock.** Idle time is kept to  a minimum so the system doesn't have to wait for I/O operations.
- Java threads can run in both a single-core and multi-core CPU's. Even though multiple threads don't run simultaneously, switching between threads eliminates most idle time. In multi-core systems, multiple threads run simultaneously in different cores in what is known as *parallel programming.* The **Fork/Join** framework in java automatically makes best use of multi-threading in a multi-core system.
- A thread can be **running** or **ready to run**. A running thread can be **suspended**i.e. temporarily halted. A suspended thread can be **resumed** i.e. made to start where it was halted. When a thread is waiting for a resource, it's **blocked**. When a thread is **terminated**, it stop executing and can't be resumed.

### Thread Priorities: 
- Priorities are integers that decide when to switch from one thread to another (so called **context switching**). Two rules determine context switching:
	1. **A thread can voluntarily allow control to be taken by another thread**: When a thread is sleeping or blocked, it voluntarily and **explicitly** gives control to the highest priority thread.
	2. **A thread can be preempted by a higher priority thread:** a lower priority thread that doesn't give control is forced by  a higher priority thread to do so.
- When two threads with the same priority compete for CPU time, the OS decides what to do!

### Synchronization:
- Multi-threading introduces asynchronicity. This is especially a thorny problem when, for example, two threads share some resource. It's bad for a thread to read a piece of data while another is writing it.
- To enforce synchronicity to eliminate such problems, java uses the **monitor**. When a thread enters the monitor, all other threads are halted until this thread exits the monitor. This prevents more than one thread from manipulating shared data at the same time.
- When an objects synchronized method is called, the object automatically enters the monitor
### [How is synchronization done? WHO KNOWS!!?](#how-synchronization-is-done).

### Messaging:
- Communication between threads in other languages is controlled by the OS, but java defines its own inter-thread messaging mechanism which is done through calls to methods that all objects have. 

### `Thread` and `Runnable`:
- Managing threads can be done with either the `Thread` class or the `Runnable` interface. The `Thread` has the following methods which are used to manipulate the behavior of a thread:

| Method | Meaning
| --- | --- |
| `getName` | Get thread name |
| `getPriority`|  |
| `isAlive`| Find if thread is still running |
| `join`| Wait for a thread to terminate |
| `run`| Entry point for a thread |
| `sleep`| Suspend a thread for a period of time |
| `start`| start a thread by calling its `run` method |

### The Main Thread:
- When a program starts executing the **main thread** starts immediately. This is a very important thread because child threads are spawned from it. It must also often be the last one to stop running to do several shutdown operations.
- The main thread is started automatically. To get a reference to it, `currentThread()` must be called. It's a static method of `Thread`. E.g.:
```java
Thread thread = Thread.currentThread();
```

## Creating a Thread:
- A thread can be created either by implementing the **`Runnable`** interface or extending the **`Thread`** class.

### Runnable:
- The easiest way to create a new thread is through implementing the `Runnable` interface. 
- implementing `Runnable` requires the implementation of the `run()` method. The code to construct a new thread is done inside the `run()` method. It is the entry point to the new thread. 
-  Inside the class implementing `Runnable` an object of type Thread is constructed in the following way:
```java
Thread(Runnable PlasticGorilla, String name);
```
- In this example, `PlasticGorilla` is an instance of the class that implements `Runnable`, while name is the name you give to this thread.
- This thread doesn't start until you call the method `start()` which calls `run()`.
- A good example illustrating how different threads execute is based on loops on multiple threads where loops are delayed a certain amount of time as in:
```java
public class PlasticGorilla{
	public static void main(String[] args) {
		new ChildThread();
		
		try {
			for (int j = 0; j < 5; j++) {
				System.out.println("Plastic gorilla thread: " + j);
				Thread.sleep(1000);
			}
			
		} catch (InterruptedException e) {
			System.out.println("Plastic gorilla interrupted");
		}
		System.out.println("Plastic gorilla thread exiting");
	}
}

class ChildThread implements Runnable{
	
	Thread thread;
	
	public ChildThread() {
		thread = new Thread(this, "Child Thread");
		thread.start();
	};

	@Override
	public void run() {
		try {
			for (int i = 0; i < 5; i++) {
				System.out.println("Child thread: " + i);
				Thread.sleep(500);
			}
		} catch (InterruptedException e) {
			System.out.println("Child thread interrupted");
		}
		System.out.println("Child thread exiting");
		
	}
	
}
```
- This program prints the following output:
```
Plastic gorilla thread: 0
Child thread: 0
Child thread: 1
Plastic gorilla thread: 1
Child thread: 2
Child thread: 3
Plastic gorilla thread: 2
Child thread: 4
Child thread exiting
Plastic gorilla thread: 3
Plastic gorilla thread: 4
Child thread exiting
```

### Thread:
- Extending the `Thread` class is almost identical to implementing the the Runnable interface except that the class `Thread` is extended instead of the `Runnable` interface getting implemented. 

### Runnable or Thread:
- The class `Thread` includes several methods that can be overridden by your class. If you don't feel the need to override such methods you can simply use `Runnable` instead. 
- Choosing `Runnable` has the adventage of allowing a class to not be tied to the `Thread` class. implementing `Runnable` allows you to effectively inherit from another class or implement multiple interfaces.

## Creating multiple Threads

## How Synchronization is done:


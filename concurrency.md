# Multithreading:
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
- More on synchronization can be found [here](#how-synchronization-is-done).

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
- Choosing `Runnable` has the advantage of allowing a class to not be tied to the `Thread` class. implementing `Runnable` allows you to effectively inherit from another class or implement multiple interfaces.

## Creating multiple Threads
- Multiple child threads that execute the same actions can be spawned dynamically with just a little change to the constructor of the newly created class as in:
```java
...
class ChildThread extends Thread{
	
	Thread thread;
	String name;
	
	public ChildThread(String threadName) {
		name = threadName;
		thread = new Thread(this, name);
		thread.start();
	};
...
```
- This constructor allows the creation of different threads that bear different name, though they do the same actions. This can be seen by how these threads are instantiated as in:
```java
new ChildThread("firstChild");
new ChildThread("secondChild");
new ChildThread("thirdChild");
```

## `isAlive()` and `join()`:
- a call to the method `isAlive()` returns a boolean informing you if a thread is still running.
- The method `join()` allows you to make a thread wait until another finishes executing. For example, the main thread should not exit until all its child threads exit. Instead of waiting for a specified time period, `join` automatically keep the main thread waiting for the child threads to finish first before it exits itself.

## Thread Priorities:
- `setPriority()` allows you define the priority of a thread. Higher priority threads get more and priority access to the CPU. When multiple threads have the same priority, there can be problems so it's safer to use threads that willingly yield control so other threads can also run.
- Threads that yield control willingly are safer and more portable than preemptive threads. 

## How Synchronization is Done:
- **Synchronization** allows you to ensure such restrictions as allowing only one thread at a time to access a shared resource.
- Java uses the **monitor** as a lock that can only be owned by a single thread at a time. No other thread can *enter* the monitor while it's *owned* by another one. They must *wait*. A thread that owns the monitor can *reenter* it.
- There are two ways code can be synchronized:
	**1. Synchronized Methods:**
- A method is called with the modifier `synchronized`. That automatically makes it synchronized (no way?!!).
- When a thread is inside a synchronized method it *enters the object's monitor, so any other thread that tries to call it has to wait* (This is a little voodooish).
- The following example shows how the `synchronized` keyword keeps each pair of numbers together, while not using results in a jumbled mess.

```java
class Num {
	synchronized void call(int nums[]) {
		System.out.print("[" + nums[0]);
		
		try {
			Thread.sleep(500);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		
		System.out.println(nums[1] + "]");
	}
}

class Nummer implements Runnable{
	Num target;
	int[] msg;
	Thread thread;
	
	public Nummer(Num targ, int[] s) {
		target = targ;;
		msg = s;
		thread = new Thread(this);
		thread.start();
	}

	@Override
	public void run() {
		target.call(msg);
	}
}

public class Synchro {
	public static void main(String[] args) {
		Num target = new Num();
		
		Nummer ob1 = new Nummer(target,new int[] {1,2}) ;
		Nummer ob2 = new Nummer(target,new int[] {3,4});
		Nummer ob3 = new Nummer(target,new int[] {5,6});
		Nummer ob4 = new Nummer(target,new int[] {7,8});
		
		try {
			ob1.thread.join();
			ob2.thread.join();
			ob3.thread.join();
			ob4.thread.join();
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
}
```
```
- unsynchronized output (I have no idea why they aren't in order):
[12]
[78]
[56]
[34]

- synchronized output
[1[7[5[38]
4]
6]
2]
```
- When `sleep()` is called, another thread jumps in to execute the method `call()`. The lack of synchronization results in a ***race condition***. All 3 threads can access the same method on the same object at the same time. Race conditions are a hard problem because they are unpredictable and give right results in some cases and wrong results in others. They can also be hard to debug.
- By preceding a method's definition by `synchronized`, you *serialize* access to it i.e. only one thread can access it at a time.
- **IMPORTANT:** once a thread enters a synchronized method on an instance, no other thread can enter any synchronized method on that instance. Non-synchronized methods on that same object can still be callable by other threads.
	**2. Synchronized Statements:** 
- When you have predefined classes with non-synchronized methods, you can synchronize them by putting calls to their methods in synchronized blocks.
- The following example similar to the one above shows the syntax of block synchronization:
```java
package exerc;
class Num {
	void call(int nums[]) {
		System.out.print("[" + nums[0]);
		
		try {
			Thread.sleep(500);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		
		System.out.println(nums[1] + "]");
	}
}

class Nummer implements Runnable{
	Num target;
	int[] msg;
	Thread thread;
	
	public Nummer(Num targ, int[] s) {
		target = targ;;
		msg = s;
		thread = new Thread(this);
		thread.start();
	}

	@Override
	public void run() {
		// This is where synchronization is done!
		synchronized (target) {
			target.call(msg);
		}
		
	}
}

public class Synchro {
	public static void main(String[] args) {
		Num target = new Num();
		
		Nummer ob1 = new Nummer(target,new int[] {1,2}) ;
		Nummer ob2 = new Nummer(target,new int[] {3,4});
		Nummer ob3 = new Nummer(target,new int[] {5,6});
		Nummer ob4 = new Nummer(target,new int[] {7,8});
		
		try {
			ob1.thread.join();
			ob2.thread.join();
			ob3.thread.join();
			ob4.thread.join();
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}
}
```

## Interthread Communication:
- The use of the `synchronized` keyword allows you to stop all other threads from accessing synchronized methods of an object, but you can have more granular control through interthread communication which is done through the following methods:
	- **`wait()`**: Tells the thread to sleep until another thread enters the same monitor and calls `notify()` or `notifyAll()`. This method also allows a specified waiting time period.
	- **`notify()`**: wakes up a thread that called `wait()` on the same object.
	- **`notifyAll()`**: wakes up all the threads that called `wait()` on the same object.
- Java oh Java. Rarely a thread can wake up for no freaking reason (though no call was made to `notify()` or `notifyAll()`. It's recommended that calls to `wait()` should be put "inside a loop that check the condition on which the thread is waiting." The book illustrate the benefits of interthread communication nicely in the  (in)famous producer/consumer problem which I will not copy here.
- *The example provided in the book makes the queue's put and get methods wait each until their action is finished before they hand control to the other. This is done inside a loop inside each method and assisted by booleans that switch based on which method owns the monitor* (bad English).

### Deadlock:
- A **deadlocks** occurs when two threads have a circular dependency on two synchronized objects.
If thread **a** enters object **A** and thread **b** enters object **B**. If **a** tries to call a synchronized method in object **B** it blocks because it can't have it until **b** releases it. If **b** also tries to called a synchronized method in **A** it will wait forever. Like race conditions, it occurs rarely only when all conditions are met and it might involve much more than two threads.
- If a multithreaded program hangs, a deadlock should be one of the first possible causes to consider.

## Suspending, Stopping and Resuming Threads:
- The methods `suspend()`, `stop()`, `resume()` are deprecated and they can cause serious problems. For example, when a thread is suspended with the method `suspend()` it doesn't relinquish locks to resources it owns. Other threads waiting for those resources will be deadlocked. `stop()` might stop a thread in the middle of writing data and locks are released so the corrupted data gets used by other threads. 
- Instead of using these deprecated methods, the `run()` method itself should be used to suspend, restart and stop threads. This is a done through a combination of suspend, resume and stop flags and the `wait()` and `notify()` methods.

## Accessing A Thread's State:
- `getState()` allows you to get a thread's state which if of type **`Thread.State`**. **State** is an enumeration with the following values:
	- **BLOCKED:** suspended because waiting to get a lock.
	- **NEW:** hasn't begun execution et.
	- **RUNNABLE:** is running or will run as soon as it has access to CPU.
	- **TERMINATED:** Completed execution.
	- **TIMED_WAITING:** suspended for a specified time as in `sleep()` or timed `join()` and `wait()`.
	- **WAITING:** suspended because it's waiting for something to happen. Happens after calls to `join()` and `wait()`.
- A thread might change state immediately after calling `getState()`, that's why this method is used mainly for debugging and profiling purposes.

## Conclusion:
- To make best use of multithreading think concurrently rather than serially.
- Too many threads can be bad as more resources will be spent on context-switching.
- The **Fork/Join framework** is best and easiest way to make great use of multi-core systems capabilities.
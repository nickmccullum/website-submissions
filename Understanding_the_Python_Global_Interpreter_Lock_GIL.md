# Understanding the Python Global Interpreter Lock (GIL)

  

1.  ## Introduction
    
Python is an interpreter language. It is in Python’s traits that the interpreter compiles the code to bytecode and then is executed via the Python virtual machine? This is the standard process with the reference implementation of Python, CPython. What if there were multiple threads that are to be executed by the interpreter simultaneously? By default, Python has not made it possible by using a mechanism called Global Interpreter Lock. This Global Interpreter Lock can be identified as a mechanism like mutex that exerts constraints on the Python code limiting the number of threads in the state of execution to one. In Layman’s terms, this means only one thread can be executed at any given time in Python using the standard interpreter.

2.  ## Prerequisite Concepts
    

1.  ### Race Condition
    
From a thread synchronization standpoint, a critical section of a program can be identified as a space or a resource that is potentially being accessed by processes that run concurrently. The race condition phenomenon can occur when multiple threads are trying to access a shared resource which is also known as a critical section. Since it is not generally known how the scheduling algorithm has scheduled threads to be executed at a given time, the order or the priority of execution is unknown. This may result in a racing condition making multiple threads race for the same resource.

2.  ### Mutex
    
In order to prevent any unpredictable consequences of race conditions, various thread synchronization mechanisms are used to control and limit access to this critical section forcing the threads or the processes to wait until the occupied thread is complete. There are many thread synchronization mechanisms such as mutex, conditions, semaphores to be employed in such scenarios.

A mutex, also known as mutual exclusion, can be defined as a mutually exclusive flag that keeps an eye out for the critical section in a code. The threads that are attempting to access this critical section are supposed to acquire a lock on this section preventing any race conditions.

3.  ### Deadlock
    
This is a phenomenon that can occur when two or more processes are constrained from accessing a common resource while waiting on another critical location that has been acquired by another process. From a two-process standpoint, a deadlock can occur when two resources have been acquired by two processes and both of them are waiting on each other to release their current resource in order to acquire the resource the other process is currently acquiring.

3.  ## What Exactly is GIL?
    
Before we learn what GIL is, we need to understand one big fundamental behind why we really need the Global Interpreter Lock.

1.  ### Python Reference Count
    
It is a trait of Python that it keeps track of the number of references for memory management purposes. In simple terms, there is a reference number attribute associated with the objects that have been created in the Python program that says the number of references that have been pointed to the respective object. It is when this number becomes zero that the memory space that was allocated for the object is freed.

Let’s take a look at this Python interactive shell example.

```
>>> import sys
>>> my_text = "Hello World"
>>> your_text = my_text
>>> common_text = your_text
>>> sys.getrefcount(my_text)
4
```

We have created an object that contains the string “Hello World”. Then we have created another object pointing to the original object. Then we have created another object pointing to this newly created object. Then finally we have our original object as an argument inside the sys.getrefcount() method. That is how we have ended up with the output 4.

```
>>> del your_text
>>> del common_text
>>> sys.getrefcount(my_text)
2
```
In the above, we are deleting two of the objects that point to the original object. When we run the same method, this time it outputs 2. This is taking the original object itself and the argument we are passing to the method above into consideration.

2.  ### What does GIL do?
    
The issue associated with this reference count attribute is that it should be safeguarded from potential race conditions that might arise from multiple threads attempting to change its values. In the event this happens, there could be lots of unpredictable problems happening such as memory leaks and other issues that may lead to the object pointing out to nothing. As we already understand, this issue can be eliminated by using some sort of resource locking mechanism as we do with thread synchronization. However, even the addition of locks may sometimes lead to deadlock scenarios.

This is the issue the Global Interpreter Lock of Python beautifully addresses. It is a mutually exclusive lock on the Python interpreter that enforces a constraint on the threads to refrain from executing themselves through the interpreter without a lock. Since there is only one GIL, deadlock scenarios are also off the table. Moreover, it does not necessarily demand lots of performance. However, the big downside is that it limits the Python program to be single-threaded. Although as opposed to the GIL, there are other solutions such as garbage collection used by languages like Java to accommodate related issues. However, Python comes from an era before the concepts of multiple threads were not as prominent as they are today.

The core idea behind Python was that it could make coding faster and easier. As we already know, the standard interpreter is CPython and it is based on C as its name suggests. The inclusion of the Global Interpreter Lock happened with the roots of CPython. At such a time, GIL was a practical approach to accommodate the faster coding Python provided. It persisted through the years without any issue until multi-threaded programs became popular.

4.  ## Downside to Multi-Threaded Programs
    
It is now our understanding what GIL is and why it was introduced to Python. As we already know, the GIL puts limitations on threads preventing them from accessing the Python interpreter simultaneously. Although GIL has little to zero visible impact on single-threaded codes and programs, when it comes to multi-threaded codes, it really can be a constriction obstructing the performance of the whole program provided that it is CPU bound.

The idea behind CPU bound programs is that as opposed to the I/O bound programs that wait generally on external triggers or signals, CPU bound programs directly consume the processing power of CPU for logical and arithmetic related tasks. These may include tasks such as adding numbers or even searching through a video frame looking for certain objects. When it comes to tasks like these, the Global Interpreter Lock really plays a big role in prohibiting any multiple threads being executed simultaneously.

We will look at an example now.

```python
import time

def count(n):
	for i in range(0,n):
		i=i+1

start = time.time()
count(100000000)

print('Time Elapsed', time.time() - start)

```
In this example, we are counting from 0 to 10<sup>8</sup> using a for loop. As it can be seen, we are doing it in a single thread.

This program would output,

```
Time Elapsed 3.995725631713867
```

Let’s now count from 0 to 10<sup>8</sup>/2 using two threads. Since we are using two threads, we are altogether counting 10<sup>8</sup> times as before. From a logical standpoint, this threaded operation should roughly reduce the time by half.

```python
import time
from threading import Thread

def count(n):
	for i in range(0,n):
		i=i+1

thread_1 = Thread(target=count, args=(50000000,))
thread_2 = Thread(target=count, args=(50000000,))

start = time.time()

thread_1.start()
thread_2.start()
thread_1.join()
thread_2.join()

print('Time Elapsed', time.time() - start)
```

The above would output,

```
Time Elapsed 4.146818161010742
```

Surprisingly, the time has not been reduced by half. In fact, it also has consumed a little bit of more time than with the single-threaded program.

This is since the Global Interpreter Lock was in the way of threads running simultaneously in this CPU bound program. Moreover, the increase in the time can be identified as a consequence of the overheads that come with acquiring and releasing the lock multiple times.

Due to these issues, one may suggest that it is best that GIL is removed from Python. However, it has been the practice of Python developers not to introduce considerable changes to the language inside the same version. in this particular case, it is even more difficult to remove GIL from Python due to issues that will be introduced related to backward compatibility, optimization, and performance.

5.  ## GIL and Python Versions
    
When Python 3 was first released in 2008, there was a chance for the developers to remove GIL from the big version update. However, this would have resulted in a version of Python that was far slower than its predecessor in terms of single-threaded and CPU bound programs. However, there were certain performance optimizations introduced to the language.

For instance, let’s take a look at this Python 2 shell output.

```
Python 2.7.12 (default, Apr 15 2020, 17:07:12)
[GCC 5.4.0 20160609] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.getcheckinterval()
100
```

It is our understanding that the GIL would affect CPU bound programs much more compared to I/O bound programs. However, when it comes to programs that are both CPU bound and I/O bound, the Global Interpreter Lock would not allow threads that are I/O bound to acquire the lock from threads that are CPU bound. This was due to one of GIL’s mechanism that had only allocated a fixed amount of time for a thread to use the interpreter. After this time was reached, it had to release it and could only acquire it if the lock was not acquired by another thread.

In Python 3, this issue was eliminated by including a much sophisticated mechanism that would consider the number of requests related to getting a Global Interpreter Lock.

Although it cannot be said for sure, it can be expected that the issues posed by GIL will further be mitigated in the future versions of Python.

6.  ## Workarounds
    
A majority of the Python users write single-threaded applications. Therefore, they should not be running into any issues related to the GIL. However, should one write a multi-threaded application, there is a module called ``multiprocessing`` that can be used for the same task while making GIL least of the worries.

Let’s write the same code again using this ``multiprocessing`` module and count 10<sup>8</sup> times.

```python
import time
from multiprocessing import Pool

def count(n):
	for i in range(0,n):
		i=i+1

if __name__ == '__main__':
	process_pool = Pool(2)
	
	start = time.time()

	process_1 = process_pool.apply_async(count, [100000000//2])
	process_1 = process_pool.apply_async(count, [100000000//2])
	process_pool.close()
	process_pool.join()
	
	print('Time Elapsed', time.time() - start)
```

This would output,

```
Time Elapsed 2.1988918781280518
```

As we can see, the time has been reduced by approximately half of the previous times. Due to the existence of overheads even in this case, the number is not exactly half or less.

As we already know, the issues associated with the Global Interpreter Lock only comes in the standard interpreter, CPython. However, there are other Python interpreters that do not have this same issue. To make the situation better. there are many available interpreters that have been written in many languages such as Java, C#, C.

Moreover, the community is working on removing the persisting issues for multi-threaded applications via approaches such as [Gilectomy](https://pythoncapi.readthedocs.io/gilectomy.html). In addition to that, we can also hope that the issues caused by GIL will further be eliminated from the future versions of Python.

7.  ## Conclusion
    
Today’s tutorial, the Global Interpreter Lock, was a topic with heavy amounts of theory. However, we believe that it is essential that everyone has an idea about the inherent features as well as issues that are associated with Python. The Global Interpreter Lock is a mechanism that enforces limitations on threads in accessing the interpreter simultaneously. Although it is ideal for single-threaded applications, major performance bottlenecks can be seen in this mechanism when it comes to multi-threaded environments. There are modules such as ‘multiprocessing’ that can be used to lose as little performance and speed as possible in multiprocessor environments.

# Python Sleep

Sleep is one of the most useful functions in programming languages. As the name suggests, sleep function is used to pause the thread being executed and wait for a predefined amount of time. There are numerous use cases for the sleep function, such as simulating a delay in the program, specifying waiting times for request related tasks, maintaining intervals between API calls, and even when accessing a common resource by multiple threads in a program.

In Python, there are many ways to invoke sleep. However, in this tutorial, we will mainly focus on sleep in the time module from the Python standard library. Let us look at a very simple implementation of the `time.sleep` function.
```python
import time
print('In 5 seconds, I will tell my name')
time.sleep(5)
print('Josh')
```
  

Output:
```
In 5 seconds, I will tell my name
Josh
```
  

If you look at the output, it will print the first line as soon as the script is run, and then will print the name Josh after 5 seconds.

  

## Syntax of `time.sleep()` Function

As we understood from the previous example, the syntax of `sleep()` function is as below.

`time.sleep(t)`

  

`t` denotes how long the sleep function persists in terms of seconds. However, instead of seconds, sleep function can work on millisecond scales as well since t parameter can be a float value.
```python
import time
print('Hello')
time.sleep(0.5)
print('World')
```
  

Output:
```
Hello
World
```
  

In this, we are printing "Hello" immediately, and "World" after 500 milliseconds.

Let us now look at a few common use cases of the sleep function.

## Usages of `time.sleep()` Function

### How to Use `time.sleep()` with Threads
    

As you may already know, threads are all about executing multiple instructions concurrently. Threads even enable intercommunication and access to the same resources. Threads are lightweight and inherently do not require a lot of memory resources.

Sleep function really comes in handy when we are dealing with multiple threads. Let us look at an example that prints the current time using two threads.
```python
import time
import _thread
def  print_time(thread_name):
	count = 0
	while count < 5:
		count += 1
		print(thread_name, str(time.ctime(time.time())) )
try:
	_thread.start_new_thread( print_time, ("Thread 1", ) )
	_thread.start_new_thread( print_time, ("Thread 2", ) )
except:
	print ("Error")
```
  
  
  

Output:
```
Thread 1 Wed Jun 17  15:48:10  2020
Thread 2 Wed Jun 17  15:48:10  2020
Thread 1 Wed Jun 17  15:48:10  2020
Thread 1 Wed Jun 17  15:48:12  2020
Thread 2 Wed Jun 17  15:48:14  2020
Thread 1 Wed Jun 17  15:48:14  2020
Thread 1 Wed Jun 17  15:48:16  2020
Thread 2 Wed Jun 17  15:48:18  2020
Thread 2 Wed Jun 17  15:48:22  2020
Thread 2 Wed Jun 17  15:48:26  2020
```
  
  

If you get scrambled outputs, do not mind it. It is because we have not added a Semaphore getting threads exclusive rights to print a message at a given time. However, everything happens so fast that we do not see how it's all printed. We can add a little bit of a delay to the program to slow it down, so that we can see how all the lines are printed.
```python
import _thread
import time
def  print_time(thread_name, sleep_time):
	count = 0
	while count < 5:
		time.sleep(sleep_time)
		count += 1
		print(thread_name, str(time.ctime(time.time())) )
try:
	_thread.start_new_thread( print_time, ("Thread 1", 1.1, ) )
	_thread.start_new_thread( print_time, ("Thread 2", 1, ) )
except:
	print ("Error")
```
  
  

We have modified the `print_time` function to accommodate a delay to get the output in a way we can observe.

The output will be similar to the previous, but this time, most likely, none of the text would be scrambled as well since we are ensuring a little time gap between thread delays.

  

### Sleep Function to Theatrical Outputs
    

Ever wanted to print texts in a theatrical way one letter after another? Try out the following code.
```python
import time
message = "Hello World"
for i in message:
	print(i, end='')
	time.sleep(0.3)
```  
  

Output:
`Hello World`

  

However, the trick is that it will print letter by letter with 0.3-second intervals in between. If you run the code, it will return the output with a beautiful letter animation.

## Sleep Functions from Other Python Libraries

 ### Asyncio  
 
Asyncio is a Python module that can be used to develop concurrently running codes. It is especially used as a foundation for asynchronous frameworks in Python that are focused on network and web connectivity tasks. Asyncio allows the development of snippets that can still perform tasks while not waiting for another task to finish.

Sleep function in asyncio is non-block as opposed to the sleep function of the time module.

Let us see what it means.

Consider the following code. We are defining a greetings function that prints Ahoy and Stranger! with a 5-second duration apart. The main function will invoke the greetings function twice as it can be seen.
```python
import asyncio
import time
async  def  greetings():
	print('Ahoy')
	time.sleep(5)
	print('Stranger!!')
async  def  main():
	await asyncio.gather(greetings(), greetings())
await main()
```
  
  

If you look at line 5, you will see that we have used the `time.sleep` function to invoke a sleep call inside `greetings()` function. If you run this, the output would be,
```
Ahoy
Stranger!
Ahoy
Stranger!
```
  

Moreover, it will print Ahoy first, then wait for another 5 seconds to print Stranger! and only after that, will it print the next batch.

Let us now replace `time.sleep()` with `asyncio.sleep()`.
```python
import asyncio
async  def  greetings():
	print('Ahoy')
	await asyncio.sleep(5)
	print('Stranger!')
async  def  main():
	await asyncio.gather(greetings(), greetings())
await main()
```
  
  

The output of this code would be,
```
Ahoy
Ahoy
Stranger!
Stranger!
```
  

This would print both Ahoy statements first and would wait another 5 seconds and print the last two Stranger! strings. The explanation here is that while `time.sleep()` blocks the entire thread, `asyncio.sleep` instructs the event loop to run all the independent executions while it is waiting until 5 waiting duration is met. This is why `asyncio.sleep` is called non-blocking.

### Pygame.time.wait
    

Pygame is a Python wrapper module for the Simple DirectMedia Layer library. Along with features to acquire library support for multimedia inputs, outputs, and keyboard, mouse, joystick inputs, it has functions such as pause. Although Pygame module is not explicitly used for general programming tasks, we can utilize its functions to facilitate our requirements.

First, let us install Pygame.

`python -m pip install -U pygame --user`

  

Let us consider the following example.
```python
import pygame
pygame.init()
print('Hello')
pygame.time.wait(5000)
print('World!')
```
  

Output:
```
Hello
World!
```
  

The output would be Hello printed, followed by a 5 second delayed print of World!.

If you look at the syntax, it is as below.

`pygame.time.wait(t)`

  

However, `t` in `pygame.time.wait(t)` denotes the number of milliseconds as opposed to seconds in `time.sleep`.

### Pyplot.pause
    

Matplotlib is one of the most sophisticated plotting libraries for Python. It is also embedded with an object-oriented application programming interface for custom applications that use Pythonic GUI toolkits. Therefore, inherently we can expect matplotlib to have a sleep function.

Let's first install matplotlib.

`pip install matplotlib`

  

Let's implement the pause function in `matplotlib.pyplot` as follows.
```python
import matplotlib.pyplot
print('Hello')
matplotlib.pyplot.pause(5)
print('World!')
```
  

Output:
```
Hello
World!
```
  

As in the previous examples, this prints Hello first and then will print World! after five seconds.

The syntax of the pause function of `matplotlib.pyplot` dictates that the sleep duration is to be specified in seconds, just like with `time.sleep()`.

### Tk.after
    

Up to this point in the tutorial, we only worked with command-line programs. However, graphical user interface-based applications are generally even more important than CLI programs. Delays and pauses are a definite part of GUI based applications.

Tkinter is a great library to work with for starters. It is a Python binding of Tk toolkit. Although there are many sophisticated GUI libraries available, Tkinter still is considered to be the standard GUI among the community and is a great starting point for beginner Python developers.

Let us consider the following code.
```python
from tkinter import Tk, mainloop
root = Tk()
print('Hello')
root.after(5000, root.destroy)
mainloop()
print('Goodbye')
```

In this, we are creating a window with line 4 of the code. Then we are printing Hello to the standard output, and we are instructing the program to wait for 5 seconds and perform the task `root.destroy` and then print Goodbye. This is how the output happens when the above code is run.

As opposed to using `time.sleep` in Tkinter applications, `Tk().after` will ensure that other tasks of the application are not halted or stopped while waiting. This feature can come in handy when programs are loading and playing some animation until it is completely initialized.

## Examples of Using `time.sleep()` Function

### Welcome Screen and Processing Screen
    

If you are writing a console application using Python, there are more than a few ways to make it more beautiful and user-friendly. Whilst being able to add colored texts is one of the community favorites, adding slight animations can really enhance the user experience.

Let us build a welcome screen to a program to check if there are any downtimes in a website.

Let’s first create a loading screen.
```python
import time
def  welcome_screen():
	welcome_message = "Welcome to website uptime monitor"
	for i in welcome_message:
		print(i, end='')
		time.sleep(0.3)
	print()
	print('Enter the website you want: https://', end ='')
	web_address = input()
	web_address = 'https://' + web_address
	return web_address
```
  

In this, we are printing the name of our program and getting an input. Now, let us write a processing screen function to check if the website is up.
```python
import time
import urllib.request
import urllib.error
def  uptime_monitor(address):
	while  True:
		try:
			conn = urllib.request.urlopen(address)
		except urllib.error.HTTPError as exep:
			print(f'HTTPError: {exep.code} for {address}')
		except urllib.error.URLError as exep:
			print(f'Website is down: {exep.code} for {address}')
		else:
			print(f'{address} is up')
		time.sleep(30)
```
In this function, we are checking if a website is up with a time interval of 30 seconds that is specified by `time.sleep` function. We do not want to increase the traffic to the website and that is why we are checking with intervals instead of constantly checking its status.

Let's put both the codes together and run
```python
import time
import urllib.request
import urllib.error
def  welcome_screen():
	welcome_message = "Welcome to website uptime monitor"
	for i in welcome_message:
		print(i, end='')
		time.sleep(0.3)
	print()
	print('Enter the website you want: https://', end ='')
	web_address = input()
	web_address = 'https://' + web_address
	return web_address
def  uptime_monitor(address):
	while  True:
		try:
			conn = urllib.request.urlopen(address)
		except urllib.error.HTTPError as exep:
			print(f'HTTPError: {exep.code} for {address}')
		except urllib.error.URLError as exep:
			print(f'Website is down: {exep.code} for {address}')
		else:
			print(f'{address} is up')
		time.sleep(30)
if  __name__ == '__main__':
	address = welcome_screen()
	uptime_monitor(address)
```
  
  

Output:
```
Welcome to website uptime monitor
Enter the website you want: https://
```
  

Let us specify a website.
```
Welcome to website uptime monitor
Enter the website you want: https://youtube.com
```
Output:
`https://youtube.com is up`

### A Digital Clock
    

This is a theatrical example where we can implement a digital clock inside the terminal or the command prompt in one line.

Before we get into the code, let us consider the following.
```python
for i in  range(0,10):
	print(i)
```  
Output:
```
0
1
2
3
4
5
6
7
8
9
```
  

However, instead of printing them one by one, we can print them in the same line replacing the previous number. We only have to slightly modify the print statement and add another print statement to perform a carriage return to get the cursor back to the start of the line. We are using a sleep function to keep each number printed for 1 second since without it, we will not be able to observe any transitions.
```python
import time
for i in  range(0,10):
	print(i, end = '', flush = True)
	print('\r', end ='', flush = True)
	time.sleep(1)
```
  
  

Now that we understand the basics, let us implement our digital clock.
```python
import time
while  True:
	local_time = time.localtime()
	local_time = time.strftime("%I:%M:%S %p", local_time)
	print(local_time, end='', flush=True)
	print("\r", end='', flush=True)
	time.sleep(1)
```
  

Output:

`10:39:01 AM`

  

We will get a digital clock that will keep running on the same line as long as we do not terminate the script.

  

## Conclusion

The Sleep function in programming languages is used to halt or pause the execution momentarily for various uses. In Python, sleep can be implemented using many methods. However, the most fundamental sleep function is the standard `time.sleep()`. The sleep time can be specified in seconds and parsed as a parameter into the function. Although the actual sleep time might be a little different than the expected, in Python, it always ensures that the specified number of seconds are met before waking the thread back up.

# Python Timer Functions in Performance Monitoring

## Python Timers

The Python time module can be used to measure the performance of a pure Python program. This is vital as one of the significant limitations of Python programmes is they are a bit slower compard to some programming languages. In these instances, we can use python timers to identify the performance impact of the code and make the necessary modifications.

## Python Timer Functions

Here are some predefined functions in built-in time module. 

-   perf_counter()
-   monotonic()
-   process_time()
-   time()
    

With Python 3.7, new time functions like tread_time() and nanosecond versions of all the above functions were introduced. For example, perf_counter() function gained a nanosecond counterpart called perf_counter_ns(). All nanosecond functions come with _ns suffix.

## Basic Usage of Timer Function

### perf_counter() and perf_counter_ns() Functions

In this section, we will use perf_counter() and perf_counter_ns() to monitor the execution time of a simple program.

In the following example, we measure the time elapsed to run the print() function.

```python
import time
 
start_time = time.perf_counter()
print("Hello World")
end_time = time.perf_counter()
 
print(f"Start Time : {start_time}")
print(f"End Time : {end_time}")
print(f"Execution Time : {end_time - start_time:0.6f}" )
 
print()
start_time = time.perf_counter_ns()
print("Hello World")
end_time = time.perf_counter_ns()
 
print(f"Start Time : {start_time}")
print(f"End Time : {end_time}")
print(f"Execution Time in Nanoseconds : {end_time - start_time}" )
```

#### RESULT

![](https://lh5.googleusercontent.com/xiha8cON3xGGwcTbZYDjNW5DABWZmARjDek2BKPYpgUXGOR1wy6InxgdQDfGm4-mtoA5NaSn1VjA-P-uE3RSPzbGF-j4-IuoC4_kmYRAqxhmjkWcmBwKRM2zAWxnwc9l0HhsLjcP)

In the next script, we use timers as a function as well as a performance metric. Using the perf_counter() function, we check how long it takes to find the network speed using the “speedtest” module.

```python
import speedtest
import datetime
import time
 
def check_speed_format(): 
    test = speedtest.Speedtest() 
    number_of_times = 0
    while number_of_times < 2:
        # Get Code Block Start Time
        start_time = time.perf_counter()
 
        time_now = datetime.datetime.now().strftime("%H:%M:%S")
        downspeed = round((round(test.download()) / 1048576), 2)
        upspeed = round((round(test.upload()) / 1048576), 2)
        print(f"time: {time_now}, downspeed: {downspeed} Mb/s, upspeed: {upspeed} Mb/s")
 
        # Get Code Block End Time
        end_time = time.perf_counter()
 
        # Print the Execution Time
        print(f"Start Time : {start_time}")
        print(f"End Time : {end_time}")
        print(f"Total Execution Time : {end_time - start_time:0.4f} \n" )
 
        # Using sleep() to pause the program
        time.sleep(60)
        number_of_times += 1
 
if __name__ == "__main__":
    check_speed_format()
```

#### RESULT

![](https://lh5.googleusercontent.com/2Yh84LfnhuLV0J_ZKq0pMmRZiyO6SBhFXTcgusRv1OItfVaLYyhV0Q9t3WP3SSYBO2Fqy6wUB7-6ssnXuI22A9iBuqjgr_uTMXjjGc1KtWahXVJGQ1gN1iFJTWANUy7cRwRdEEdv)

From the result, we can determine that the upload and download speeds of the network take around 20 seconds. Using f-strings we format the total time to a decimal number with 4 decimal points.

As the perf_counter() returns the value of a performance counter in fractional seconds this function is the best choice to deal with shorter periods because it is a clock with the highest available resolution. Using perf_counter functions will lead to a more precise output value.
  
### monotonic() Function

The monotonic() method in the time module is used to get the time value of a monotonic clock. A monotonic clock is a clock, which only runs in a single direction, without the ability to rewind the clock. This method returns a float value, which represents the value of a monotonic clock in fractional seconds. The monotonic method is best suited for capturing time frames larger than a second.

#### Example
```python
import time
 
# Get the value of monotonic clock
# at the start time for the process.
start_time =  time.monotonic()          
 
print("Monotonic clock value at start =  ", start_time)
 
user_input= input("Enter a Number :  ")
print(str(user_input))
 
# Get the value of monotonic clock
# at the end time for the process.
end_time = time.monotonic()       
 
print("Monotonic clock value at end = ", end_time)
print("Time Elapsed = " , (end_time - start_time))
```

#### RESULT
![](https://lh6.googleusercontent.com/l2MaixwOrTDUdUFqmobBtz-dkADnmoy5kC5b4qOKhteSRgCJg7Cf1S9yzWtB1q9mVfAl8JzP7hK_3ZNMbkMXlUEOixc1OvqGTntNTXwjQz60YO3pII9XEOFYd0YZ23pmWUX-a8pf)

### process_time() Function
The process_time function only calculates the system and the CPU time during the process. This will not include sleep time unlike perf_counter(), which calculates time including the sleep time. This function can be used whenever there is a need to calculate the time taken for the CPU to complete a particular process. The following examples demonstrates how process_time() differs from perf_counter()

### process_time()
```python
import time
 
start_time =  time.process_time()       
 
print("Process time at start =  ", start_time)
 
time.sleep(10)
 
x = 0
for x in range(1000000):
    x = x + 1
print(f"The Loop ran {str(x)} times")
 
end_time = time.process_time()       
 
print("Process time at end = ", end_time)
print("Time Elapsed = " , (end_time - start_time))
```
#### RESULT
![](https://lh4.googleusercontent.com/wcpsHE_lmiUCZOv9gdT7iE9W19Cw5MvMv7stDyemEUO9l076NEpfCZBoJpatdWNeS7Y_hVffIpH4EOgM4ePLKYYxPvTOA5VBy5sCpHqAbFxqLkkdV3T8SPgWW7XaanvByNiZYhwd)

### perf_counter()

  
```python
import time
 
start_time =  time.perf_counter()       
 
print("Perf_Counter time at start =  ", start_time)
 
time.sleep(10)
 
x = 0
for x in range(1000000):
    x = x + 1
print(f"The Loop ran {str(x)} times")
 
end_time = time.perf_counter()       
 
print("Perf_Counter time at end = ", end_time)
print("Time Elapsed = " , (end_time - start_time))
```
  

#### RESULT

![](https://lh3.googleusercontent.com/THjFXf6haTumPCArLqGEb4H_FfAa7u85vHya8FsiJVVDpYx17dZDluS2nRZW9IPMMZvsn7SPQHb6EhtlRFXFoawwusVOwvFClWcO705IAkB6B6Tkx0oglPOkW6FwhKt3CwlsfjIo)

As you can see from the results of the above programs, the process_time() method only calculates the time elapsed to run the program logic ignoring the sleep time. The perf_counter() method captures the total time including the sleep time which in this instance is 10 seconds.

### time() Function
The time() function in the time module is used to get the time in seconds since epoch. The epoch is the point where time starts, and it is platform dependent. On Windows and Unix systems, the epoch is 1/1/1970, 00:00:00. Following example demonstrates how to get the epoch time.

Getting the system epoch time example.

```python
import time
 
# Get the system epoch
temp = time.gmtime(0)
epoch = time.asctime(temp)
print("epoch is : ", epoch)
 
# Get the time in seconds since the epoch
time_now = time.time()
print("Time since the epoch in seconds : ", time_now)
```

#### RESULT
![](https://lh4.googleusercontent.com/zyl64PrqTAgs3V7KMLxRCXA5d-fmcWICPobwbKVJF7oXKw_qCj5cRsV_Z7y4Eqc8yOe2ziOWUjb_0XqtNKmXF5E-PoOYtT4Zth7oxsr2X7U_zODC3Deoz1EZ8-pyBVG1eFugeGjd)

## Python Timer Class

Classes are a foundational element in object-oriented programming. A class is a basic template which can be used to create other objects based on that class. A class consists of a collection of properties and behaviours. In python performance monitoring a class can be used to keep track of a particular state of an object.

Benefits of Using a Class

-   Flexibility - The reusability of code increases as the class can be called in multiple instances with a code block.
    
-   Readability - The code becomes more readable and easier to understand.
    
-   Consistency - When properties and behaviours are changed into specific attributes and methods code becomes more consistent.
    

### Creating a Python Timer Class

Following code-block demonstrates how a python class can be created to keep track of when a timer starts and the elapsed time.

```python
import time
 
class Timer:
 
    def __init__(self):
        self._start_time = None        
                                                         
    def start(self):
        # Check if the timer is running
        # If not stat the timer
        if self._start_time is None:                            
            self._start_time = time.perf_counter()              
 
    def stop(self): 
        # Stop the timer then report the elapsed time
        if self._start_time is not None:                                            
            elapsed_time = time.perf_counter() - self._start_time 
            self._start_time = None 
            # Using f-string to format time to four decimals
            print(f"Elapsed time : {elapsed_time:0.4f} seconds")
 
if __name__ == "__main__":
    # Create a new object using Timer Class
    new_timer = Timer()
    new_timer.start()
    time.sleep(10)
    new_timer.stop()
```

#### RESULT

![](https://lh5.googleusercontent.com/JQQLibgqD3j_O1-ZQMmFuJjYOCBN96nejXa7Gggh9B8Y3h4AuQX1e4KYSWZc5wZeRatqytD0YvwDqgqrIE_yzOnAa7oPk7XzJjg7IdreR1JzS92x5tM2amIJnEpbdVKWCFQI3QXY)

A new instance of the Timer class is created called “new_timer” then we call the start function and inform the program to wait for 10 seconds using “time.sleep(10)” and finally call the stop function to stop the time calculation and return the elapsed time.

Because the start() and stop() functions can be called upon multiple times this can lead to unintended consequences. To mitigate this, we modify the code to raise an error if either of the two functions is called multiple times as shown below.

```python
import time
 
class TimerError(Exception):
    """An exception used to report errors in use of Timer class"""
 
class Timer:
 
    def __init__(self):
        self._start_time = None        
                                                         
    def start(self):
        if self._start_time is not None:                            
            raise TimerError(f"Timer is running. Use .stop() to stop it")
        elif self._start_time is None:
            self._start_time = time.perf_counter()                              
 
    def stop(self): 
        # Check if start_time is assigned
        if self._start_time is None:
            raise TimeoutError(f"Timer is not running. Use .start() to start it")
        # Stop the timer then report the elapsed time
        elif self._start_time is not None:                                          
            elapsed_time = time.perf_counter() - self._start_time 
            self._start_time = None 
            # Using f-string to format time to four decimals
            print(f"Elapsed time : {elapsed_time:0.4f} seconds")
```

We test if the TimerError is working by deliberately making incorrect calls to start() and stop() functions in the “__main__” execution block.

### Testing start() Error
```python
if __name__ == "__main__":
    # Create a new object using Timer Class
    new_timer = Timer()
    new_timer.start()
    new_timer.start()
    time.sleep(10)
    new_timer.stop()
```

#### RESULT

  

![](https://lh5.googleusercontent.com/gnQFWCtizn0GH_8z01lYXgvVdsJ1AyPnWgsCBEBIpYZC_o5OU52eBJisXMdEBIYEfiEq8fbTjWPR9F5tuyDDTA-WHgF2fABl3iOhUVi_dXQkb_Vamf1pvlNuyuZH0-qHYVQyT6P8)

### Testing stop() Error
  
```python
if __name__ == "__main__":
    # Create a new object using Timer Class
    new_timer = Timer()
    new_timer.stop()
```

#### RESULT

![](https://lh6.googleusercontent.com/s0wcYz9z_kAgyH63sAvK00JNZP_jXEv0f7zWqOuTumM5WhDROWUPQybiy6qTzWI2OdwVK8txDVBCHuF5M-yULM6Miitb5n1BhQRx7kUJBXuIjNideLMFd-YZsoUjlOkYCB9FMzEc)

We create a new class called “TimerError”, that will be used to capture any errors in start() and stop() functions. As you can see from the above tests both if the start() or the stop() functions are called incorrectly it will generate a “TimerError” and inform the user.

### Improving the Timer Class

### Timer Class variable string output

To make the Timer class more flexible first we will provide the user with the option to determine how the output will be shown. In the previous code-block for Timer Class, we hardcoded the output as follows.

```python
print(f"Elapsed time : {elapsed_time:0.4f} seconds")
```

This wording makes sense if the user wants to find the elapsed time as the output but cannot be used in every scenario. Hence, we can provide the user with the option to set a custom output text so the Timer Class will be more flexible in its use. Below is the improved Timer Class.

```python
import time
import wget
from wget import bar_adaptive
 
class TimerError(Exception):
    """An exception used to report errors in use of Timer class"""
 
class Timer:
 
    def __init__(self, text="Elapsed time: {:0.4f} seconds"):
        self._start_time = None 
        self.text = text       
                                                         
    def start(self):
        if self._start_time is not None:                            
            raise TimerError(f"Timer is running. Use .stop() to stop it")
        elif self._start_time is None:
            self._start_time = time.perf_counter()                              
 
    def stop(self): 
        if self._start_time is None:
            raise TimeoutError(f"Timer is not running. Use .start() to start it")
        # Stop the timer then report the elapsed time
        elif self._start_time is not None:                                          
            elapsed_time = time.perf_counter() - self._start_time 
            self._start_time = None 
            # Use the User provided string as the output string
            print("")
            print(self.text.format(elapsed_time))
 
if __name__ == "__main__":
    # Create a new object using Timer Class
    new_timer = Timer(text="Total Download time is {:0.2f} seconds")
 
    # Find the time required to download the python installer
    new_timer.start()
    download_url = "https://www.python.org/ftp/python/3.9.0/python-3.9.0-amd64.exe"
    wget.download(download_url,bar=bar_adaptive)
    new_timer.stop()
```

#### RESULT

![](https://lh5.googleusercontent.com/ymjKcLcuaaJcAwtf_DiBbduXu88pd8JsE4FxymQwd9jj6Oz0AD5s7S3f20W5YM-I_3eB0ANObU2dg02zv3fbsnT5d39UarB3NEI9q82ZFw4mB5IXaT8KuKVQBdZ_R9xfO976k_rU)

In the above example, we provide the end-user with the choice to define the output string enabling the Timer Class to be used in any situation. In this example, we check for the time it takes to download the python installer. As the output string the user will define “Total Download time is {:0.2f} seconds” to adapt the Timer Class object to this new use case.

### Timer Class with a return value
If we want to save the elapsed time as a value in the code instead of displaying it, we can modify the stop() function in the Timer Class just by adding a return statement as follows:

```python
    def stop(self): 
    
        if self._start_time is None:
            raise TimeoutError(f"Timer is not running. Use .start() to start it")
        # Stop the timer then report the elapsed time
        elif self._start_time is not None:                                          
            elapsed_time = time.perf_counter() - self._start_time 
            self._start_time = None 
            # Use the User provided string as the output string
            print("")
            print(self.text.format(elapsed_time))
            return elapsed_time
```

Then we execute the programme.

```python
if __name__ == "__main__":

    new_timer = Timer(text="Total Download time is {:0.2f} seconds")
 
    # Find the time required to download the python installer
    new_timer.start()
    download_url = "https://www.python.org/ftp/python/3.9.0/python-3.9.0-amd64.exe"
    wget.download(download_url, bar=bar_adaptive)
    total_time = new_timer.stop()
    
    print(str(total_time))
```

#### RESULT

![](https://lh6.googleusercontent.com/dWZ63Q2WOF1lDtcZnQQmlUu-i79uprlx-jcZ0TCLbHg791bDC1vwiRQPrp1MnzVUg48jCRcoLTzhEZB_l4tWlanIMGzTLdAQ4cqoMfZl_YE98BL49mn8_camJ90iH937jYWHYBY8) 

As shown above, we return the elapsed time in the stop() function. When calling the stop() function, we assign the function to a variable called total_time to capture the return value.

### Timer Class to store multiple measurements

To use more than a single timer in a particular code and store the performance metrics obtained by the corresponding timer in an orderly manner, we will implement a dictionary in the Timer class to capture each separate timer object.

```python
import time
 
class TimerError(Exception):
    """An exception used to report errors in use of Timer class"""
 
class Timer:
 
    timers = dict()
 
    def __init__(self, text="Elapsed time: {:0.4f} seconds", name=None):
        self._start_time = None 
        self.name = name
        self.text = text
 
        # Add a new timer to the dictionary
        if name:
            self.timers.setdefault(name, 0)
 
                                                         
    def start(self):
        if self._start_time is not None:                            
            raise TimerError(f"Timer is running. Use .stop() to stop it")
        elif self._start_time is None:
            self._start_time = time.perf_counter()                              
 
    def stop(self): 
        if self._start_time is None:
            raise TimeoutError(f"Timer is not running. Use .start() to start it")
        # Stop the timer then report the elapsed time
        elif self._start_time is not None:                                          
            elapsed_time = time.perf_counter() - self._start_time 
            self._start_time = None 
            # Use the User provided string as the output string
            print("")
            print(self.text.format(elapsed_time))
 
            #Add times measured by the same timers
            if self.name is not None:
                self.timers[self.name] += elapsed_time
 
            return elapsed_time
 
if __name__ == "__main__":
    # Create a new object using Timer Class
    new_timer_one = Timer(name="test_timer_01")
    new_timer_one.start()
    time.sleep(3)
    new_timer_one.stop()
    new_timer_one.start()
    time.sleep(4)
    new_timer_one.stop()
 
    new_timer_two = Timer(name="test_timer_02")
    new_timer_two.start()
    time.sleep(5)
    new_timer_two.stop()
    new_timer_two.start()
    time.sleep(10)
    new_timer_two.stop()
 
    print(Timer.timers)
```

#### RESULT

![](https://lh5.googleusercontent.com/QffbDdNEe1oMy5Hm64HoyKAUCW-S3THtCeNDN2tUTmaUbko651LgrUz212s0VLKoYuk6NpL2z3uF1uwdYtqv4sUl0FV_IeOVf6Tq__9YaUtlp3GFu3Zo2LIUcBX211VXuwZpTWZS)  

As you can see from the results, each separate timer has been captured by the dictionary. Furthermore, the total elapsed time for each timer is calculated and presented as an item. To achieve this, we use the “setdefault()” method to add a new python timer item to the dictionary. From this method, we make sure that the timer value is set to zero only if a new timer is introduced.

The next section will demonstrate how this improved Timer Class can be used to obtain the performance metrics of a program. In the code-block shown below, we define two functions to count prime numbers then use the Timer Class to calculate the elapsed time.

```python
from timer import Timer
 
def count_primes_one(start, end):
    count= 0
    for i in range(start, end+1):
        if i==2:
            count+=1
        else:
            for j in range(2,i):
                if i%j==0:
                    break
                if j== i-1:
                    count+=1                
    return count
 
def count_primes_two(start, end):
    count= 0
    for i in range(start, end+1):
        if i==2:
            count+=1
        else:
            for j in range(2,i):
                if i%j==0:
                    break
                if j>= i/j:
                    count+=1
                    break                
    return count
 
if __name__ == "__main__":
    # Create a new object using Timer Class
    new_timer_one = Timer(name="test_timer_01")
    new_timer_one.start()
    print("")
    print(count_primes_one(1, 1000))    
    new_timer_one.stop()
 
    new_timer_two = Timer(name="test_timer_02")
    new_timer_two.start()
    print("")
    print(count_primes_two(1, 2000))
    new_timer_two.stop()
```


#### RESULT

![](https://lh3.googleusercontent.com/6D-x_eTrmo4OspKjeAhoFHR6IJt___BYk4rdd6-thWAkjkk4p9VNXVn1Vt_qlMcWNrqJS7IhaE5LqLUFKrp1vAFFMKRdfoIBU1M1PCtT50zpAr4N5yhWwL3Q68Xdf871RB5_Ys5v)

As indicated by the result, we successfully used the Timer Class to check the performance of the functions “count_prime_one” and “count_prime_two” and how long it took each function to calculate the prime numbers in the given range.

## Conclusion
In this article, we understood how the performance of programs can be measured using python's built-in functions and how to create a custom python class to measure performance metrics. Identifying and quantifying the performance of a program is crucial in a production environment, as this can help mitigate performance-related issues as well as to reduce the resource usage of a particular program.
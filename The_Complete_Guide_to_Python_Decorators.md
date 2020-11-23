
# The Complete Guide to Python Decorators

## What are Python Decorators?

Python decorators are used in wrapping functions and classes with additional code blocks, essentially adding additional functionality without modifying the underlying function or class.

Python decorator is a function that takes another function as an argument to perform additional functionality and returns the result of the overall code-block. This is possible because in python functions are considered first-class objects enabling the functions to be passed as arguments in other functions. As decorators treat other functions as their data, this programming technique is called metaprogramming.

The following code block demonstrates how the python decorators can be used. In this instance, the function “calculatetotal” is used to calculate the total of two given values. We wrap this function within a function called “checkvalue” to limit the execution of the original function, only if one of the given values are equal or greater than two hundred.

```python
# Original Function
def calculatetotal(val1, val2):
    return val1 + val2
 
def checkvalue(func):
    
    # Inner Function to Validate Values
    def wrapper(val1, val2):
        if val1 >= 200 or val2 >= 200:
            # Call the Original Function
            return func(val1,val2)
    # Return the final result
    return wrapper
 
cal = checkvalue(calculatetotal)
total = cal(210, 10)
print(total)
```

**RESULT**
![](https://lh5.googleusercontent.com/Ghorxrk8rXDTW2EvCUdxKzUASA3YqV_jk7u541Xz6mzXy8eugx1wA0xymI-ruOvKqaThWWJof6a-VI1OuPl-CRKgsjhT0SrqlMC3F7esz49olLMAde0NbJW9N2Am9qLwljjqnqhP)

The “checkvalue” function receives the “calculatetotal” function as the argument while the inner function called “wrapper” will receive the two values which will be passed to the “calculatetotal” function as arguments.

## Why are Decorators used?

Decorators are created because of their modularity and explicit behaviour. Using decorators, additional functionality can be added to any existing function without having to modify the original function. As the user can explicitly apply decorators based on their specific needs, this reduces the repetition of code blocks and leads to reusable and a cleaner code structure.

Decorators are mainly used for the following use-cases.

#### Functional Addons

The main reason for using decorators is to add extra functionality to an existing function without having to do major modifications to the original function and preserving the function as a reusable object.

#### Data Sanitization

In instances where variables and methods can be affected by other functions within a programme, decorators can be placed upon a function to sanitize the data and return the intended output.

#### Function Registration

To allow multiple subsystems to communicate with each other, decorators can be used to register the function so that each subsystem can carry out communications without having to explicitly gather information of each subsystem.

### Built-in Decorators

The Python standard library and other frameworks provide us with built-in decorators that can be used to modify the behaviour of a function. The commonly used built-in decorators are as follows

-   @classmethod / @staticmethod
These decorators are used to create a method without creating a new instance.

-   @mock.path / @ mock.patch_object
Derived from the mock module these decorators are used in unit testing.

-   @login_required
In Django python web framework @login_required is used for setting login privileges

-   @task
In the Celery module, where it is used in distributing tasks across threads and mechanisms @task decorator is used to identify a function as an asynchronous task.

## Decorator Syntax

In python, the symbol @ also called the pie syntax can be used to assign a decorator function to the specified function. The next example is the same code used to filter values which are equal or greater than two hundred but written using the decorator syntax.

```python
def checkvalue(func):
    
    # Inner Function to Validate Values
    def wrapper(val1, val2):
        if val1 >= 200 or val2 >= 200:
            # Call the Original Function
            return func(val1,val2)
    # Return the final result
    return wrapper
 
# Using @ symbol to indicate the decorator
@checkvalue
def calculatetotal(val1, val2):
    return val1 + val2
 
print(calculatetotal(210, 10))
```
**RESULT**

![](https://lh6.googleusercontent.com/8OTljf2IOx-LKCIp-HasbsANQMOZ5mxSWkKU7KGFuojXylHuDBldK9hbmZzJ34nKGF0Vh2r0F-DdJtyoOPAb6pvDuIb4v4QZumV51HZ8YohMx5Frxm_9kiyXm8337vYPcWNci1_W)

We use the @ symbol with the decorator function name, in this case, the “checkvalue” to indicate that the “calculatetotal” will be wrapped using the “checkvalue” function. This enables us to directly call the “calculatetotal” function to get the combined functionality. If the condition within the “checkvalue” function fails, it will result in a None type object returning.

```python
print(calculatetotal(10, 10))
```
  
**RESULT**

![](https://lh4.googleusercontent.com/oBzNEtnZgu-86m9m-XgwTl2JhlikRu6pg_iSQfa_PgrHbpUNM2sw4oXhJLr1vA_leKoms15CV9iBgSi4nwKCxqb_o3fp_c1UsdM-a3XVLLZdKj864FLa13jqm1vGGsNXzBqGG56x)

## Multiple Decorators in a Single Function

In python, multiple decorators can be applied to a single function. The main consideration when applying functions is the order in which the decorators should be assigned. The order in which Python applies decorators is from top to bottom.

Let us see how we can apply multiple decorators to a single function.

```python
def makeupper(func):
    # Function to make message Upper Case
    def wrapper(msg):
        uppermsg = msg
        uppermsg = uppermsg.upper()
        print(f"makeupper decorator conversion -> {uppermsg}")
        return func(uppermsg)
 
    return wrapper
 
def maketitle(func):
    # Function to make message Title Case
    def wrapper(msg):
        titlemsg = msg
        titlemsg = msg.title()
        print(f"maketitle decorator conversion -> {titlemsg}")
        return func(titlemsg)
 
    return wrapper
 
# Assign Multiple Decorators
@makeupper
@maketitle
def printgreeting(message):
    print(f"Final message -> {message}")
 
 
# Call the Function
printgreeting("hello world")
```
  
**RESULT**

![](https://lh6.googleusercontent.com/CpCQt9eWW8552cTD0es-cRWVPeDKrVqo8q_zzXPXY6Y2FHgErdo2QzXxef46LrojaaP_fUMGUrQKxaLwG9fMHEuNTMPEtojHKXNJerLLNYru9pq6Pw5O9enxZnT87CndLQJCSlUA)

In the above example, two decorator functions are created to convert a given string to uppercase, or title case and pass it to the original function. Then the decorators are assigned to the “printgreeting” function.

The execution order of the decorators is determined by the order in which we have defined the decorators. The “makeupper” decorator is called first, then the “maketitle” decorator is called resulting in the final output being in the Title case as it is the last value passed to the original function “printgreeting”.

To reverse the order in which the decorators will be applied, we can simply change the positions of the decorators as below. The result will be an uppercase message as it will be the final decorator that will be called.

```python
# Assign Multiple Decorators
@maketitle
@makeupper
def printgreeting(message):
    print(f"Final message -> {message}")
 
 
# Call the Function
printgreeting("hello world")
```

**RESULT**
![](https://lh4.googleusercontent.com/F1Tu0AOeiYjkMssa5y0u_Svw3nhklIuLauG3nXTFiOBlUQ3gS0zdTVTaBqg8E43TaDtKN_m48H0S1f5gEc8De4molOr0D7lZ8HeQlZRdFGnaHAmzQMWdh0lr_gXCW89CxeaGqaWA)

## Multiple Arguments in Decorator Functions

In the above functions, we have assigned decorators with single and multiple arguments. In addition to explicitly assigning arguments, the Python decorator functions can be defined to accept any number of arguments.

In the following code block, we will define a decorator function to accept any number of integer arguments and call a function to get the squared value of each number.

```python
def getvalues(func):
    def wrapper(*args):
        results = []
        for x in args:
            x = int(x)
            results.append(func(x))      
        return results
    return wrapper
 
 
@getvalues
def makesqure(value):
    value = value**2
    print(value)
 
makesqure(6, 8, 10, 12, 15)
```

**RESULT**
![](https://lh3.googleusercontent.com/V-k85kVpB66Gfb3ptPGm4a4OHKju40SJcuS-fPga6EGz4JKcoGPRRXAaVYKI0lLG7bBUcj_kCPHmqHYqfvEHyP7uDRG0dMBAF4ZdTJdDHJ6hnBC7m8eThNbkOfF5nzVAABROct84)

Using Python decorator function “getvalues”, we are allowing multiple arguments to be passed to the “makesqure” without changing the original “makesqure” function. The *args variable is used to accept any number of arguments, and each value is passed to the “makesqure” function using a for loop.

## Assigning Decorators for Classes

Decorators that can be assigned to Classes as Python Class is a callable object. This allows the programmers to maintain the state of a program while adding additional functionality. The below example will demonstrate how a simple class can be used as a decorator.

```python
class Printcalculation(): 
  
    def __init__(self, func): 
        self.function = func 
  
    def __call__(self, value): 
        if value > 10:
            self.function(value) 
        else:
            print("Enter a value greater than 10.")
  
@Printcalculation
def multiply(value): 
    totalval = value * 50
    print(str(totalval))
  
multiply(15)
```

**RESULT**
![](https://lh5.googleusercontent.com/-NVwFKk1j5CL-cz48rb2N6Gd2dXtgL0hk-l1drIAxNCuv7K07S6pecf0pyfg4R4EP0MmR7Oyf8sF6l5b1y8BUBmUkpwxtEfUj4XuWs30Sgt0P0FfDMw6Yu9OutLR7obJN4_G-Ija)

Tthe class “Printcalculation” is called in as the decorator. The “multiply” function is modified by adding a condition in the decorator class. the “\__call__” function only executes the “multiply” function if the given value is greater than ten. The “\__call__” method is implemented to make the class callable and each time the class is called the code inside the “\__call__” function is executed after the class is initiated.

If the given value is less than 10, it will print the message saying, “Enter a value greater than 10.”. This is demonstrated by calling the multiply function with five (5) as the argument.

```python
@Printcalculation
def multiply(value): 
    totalval = value * 50
    print(str(totalval))
  
multiply(5)
```

**RESULT**

![](https://lh4.googleusercontent.com/S5g150Q_SFxWW1VEVaePyhmprxpm1kcJqSIAZpHJl_gUomWguQnC8JIkyRcZkV_esOfQxe56iVxOeqpXo2bSznQOnCG4H2900DhV28-PK5-U6d3XL29KwQRDh7HzSJQLPa6oPQHP)

Let us look at an advanced decorator example, where we use the Class to maintain the state of a given function.

```python
import functools
import time
 
class Time_difference:
    def __init__(self, func):
        functools.update_wrapper(self, func)
        self.func = func
        self.time_diff = 0
 
    def __call__(self, *args, **kwargs):
        get_time = time.perf_counter()
        time_difference = get_time - self.time_diff 
        self.time_diff = get_time
        print(f"Function waited {time_difference:0.4f} seconds before executing {self.func.__name__!r}")
        return self.func(*args, **kwargs)
 
@time_difference
def printgreeting(name):
    print(str("hello ").upper() + str(name).title())
 
 
printgreeting("barry")
time.sleep(1)
printgreeting("jenifer")
time.sleep(2)
printgreeting("harry")
```

**RESULT**

![](https://lh5.googleusercontent.com/9d5mGb6Jmcq6V31vKQB2RqfgtXmxk8oye8lvN7UvMK94k3Uo4QBpC690F_HgVQj0S32--YeQIp1dWKZESJZkZoiPennnxIbGoWvJT1l1AfLd7gb5V0HvsA0odHN8hvIrcZHoEOK3)

In this programme, we use the “Time_difference” class to calculate the time between each execution of the “printgreeting” function. Using the functools module, we use the “update_wrapper” function to wrap the “printgreeting” function, and return the wrapper. In this instance, the wrapper is the “__call__” method.

In the “Time_differance” class we store the execution time. Each time the function is called the new time will be subtracted from the stored time to get the difference in time between each execution.

## Returning a Class from a Decorated Function

In Python, both class and function are regarded as objects that enable us to return a class in a decorated function. In the below example, we create a code block to multiple all given values by 50.

Let us see how this is implemented. The main class “Multiply” is created with the following functions.

-   multiply_val - to implement functionality within a subclass. The “__call__” method will reference this function when a new instance is created.
-   function_use - describe the function
-   random_number - generate a random number
    

Then the decorator function called “multiply_function” is created. Inside that, we create a subclass of class “Multiply” called “Multiplication_Sub” and create the function “multiply_val” to multiply each given value by 50.

In this instance, when we call “multiply_values” function it will return the created instance of the subclass not the reference.
```python
from random import randint
 
class Multiply: 
    def __call__(self, *args): 
        return self.multiply_val(*args) 
    
    def multiply_val(self, *args): 
        raise NotImplementedError('Subclass must implement `multiply_val`.')
 
    def function_use(self):
        string = "Each given value will be multiplied by 50"
        return string
 
    def random_number(self):
        return randint(1000, 9999)
 
 
def multiply_function(func): 
    class Multiplication_Sub(Multiply): 
        def multiply_val(self, *args): 
            if args:
                results = []
                for x in args:
                    x = int(x)
                    results.append(func(x))      
                return results 
            else: 
                return func(*args)
    return Multiplication_Sub() 
 
@multiply_function
def multiply_values(value=0): 
    if value != 0:
        return value * 50
    elif value == 0:
        return "No Value Provided"
 
 
# Call the function_use function
print(multiply_values.function_use()) 
 
# Call the main function
print(multiply_values(2, 1)) 
print(multiply_values()) 
print(multiply_values(2, 1, 4)) 
 
# Call the random function
print(multiply_values.random_number())
```

**RESULT**
![](https://lh6.googleusercontent.com/TY7SEmGK_HnomUDD7DCdcTE_AOjfPQY8-3_5cxITn9BDjJSZ5xtHNCb41h9yTiAnwANQUUNppdo8eCmIeEAyRFmO2aEmfAnEj7D-r6yim16ogliF9Xkgh97QAT8Hq9ep_Kti4xS_)

Using the result set, we can identify that the returning object is a class. This enables us to call functions within the “Multiply” class, in addition to the main functionality of the function. In the above example, the first function call we are calling “function_use” function within the “Multiply” class. However we are only referencing the “multiply_values” function. The same is true when calling the “random_number” function.

## Python Decorators in Debugging Code

Programmers can use Python decorators as a debugging tool to understand the functionality of a written function. To demonstrate this, we will create a simple programme that converts the given value to a specified temperature unit.

```python
from functools import wraps
 
def debug(func):
    # Copy the original function details
    @wraps(func)
    def wrapper_debug(*args):
        # Create a list of arguments given
        args_list = [repr(a) for a in args]
 
        # Print the Called Function 
        print(f"The Function Called ==> {func.__name__}({args_list})")
        
        # Print Each Argument
        arg_number = 0
        for args_num in args_list:
            print(f"Argument {arg_number} ==> {args_list[arg_number]}")
            arg_number += 1
 
        # Print the output
        value = func(*args)
        print(f"The Function {func.__name__!r} Returned ==> {value!r}")
        return value
    return wrapper_debug
 
@debug
def convert_to_temp(temp, unit):
    unit = str(unit).upper()
    if unit == "C":
        result = int(round((9 * temp) / 5 + 32))
        result = f"{temp} converted to Celsius is {result} C"
    elif unit == "F":
        result = int(round((temp - 32) * 5 / 9))
        result = f"{temp} converted to Fahrenheit is {result} F"
    else:
        result = "Please provide C (Celsius) or F (Fahrenheit) as an option"
    return result
 
 
print(convert_to_temp(5,"C"))
# Create a Line
print(f"\n"+"="*50+"\n")
print(convert_to_temp(5,"F"))
```

**RESULT**
![](https://lh5.googleusercontent.com/TwPFIMBcp7ZIEa5PsEk54tP8KsgXWBJAIG2aUwCNmudz7eVS5xLgGO0shSdNnAp-tU1Wg8ZPRi72DR-LLoDBU_1uIZhTv6nkFQmkxP1UeDYpMwvT7P7MsoZTUZqut08JAz8g4RZi)

In the above example, we use the decorator function debug to deconstruct the “convert_to_temp” function. Using the @wraps decorator from the functools module lets us carry over the original function name, docstring, argument list, etc… Thus, deconstructing each step of the function without modifying the original function allows programmers to better understand their functions and experiment with them.

## Conclusion
In this article, you have gained an understanding of what are Python decorators, when to use decorators and their advantages in writing programmes. Python decorators provide an efficient way to add additional functionality to existing functions while keeping the original function unchanged. Using decorators increases the code readability and increases the overall reusability of code blocks.
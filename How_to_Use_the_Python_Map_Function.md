# How to Use the Python map() Function

## What is the map() Function?

The map() function is a built-in python function that allows you to manipulate items in an iterable without a `for loop`. This is also known as mapping. An iterable is an object that can return its values(members) one at a time, allowing it to be iterated over. The python functions list, tuple, dict (dictionary) and set can be used to create iterable objects.

Following is a basic syntax of the map function.

```python
map(function, iterables)
```

*   _function – Mandatory – The function to be executed upon the object_
*   _iterables – Mandatory – iterator object (list, dict etc…, Can send any number of iterables but each iterable must hold at least a single parameter)_

```python
# Lists
list_a = [10, 20, 30, 40, 50]
list_b = [9, 8, 7, 6, 5]
 
# Function to Calculate two lists
def calculateValues(list_one_value, list_two_value):
    total = list_one_value + list_two_value
    return int(total)
 
# Use the map function to calculate each item in the lists
calculated_value = map(calculateValues, (list_a), (list_b))
print(list(calculated_value))
```

In the above example, it shows how the map function can be used to easily calculate two lists using a predefined function (calculateValues) without having to resort to a `for loop`. This makes the code easier to read and understand. Mapping is an integral part of the functional programming style.

## Link between Python Mapping function and Functional Programming
Functional programming is also known as FP for short. It is a paradigm or style of writing programs that value immutability, modularity, referential transparency, and pure functions. Functional programming evolved from lambda calculus, a mathematical system built around function abstraction and generalization. It also avoids the concepts of shared state, mutable data, which are a core part of object-oriented programming.

Functional programming mainly uses iterable data sets with a combination of various functions. The most used techniques for manipulating or transforming data are.

1. **Mapping**

    This consists of transforming data which is obtained through an iterable object and producing a new item(iterable) by calling a transformation on each item on the iterable object. 

2. **Filtering**

    Filtering out items in an iterable objects to create a new item(iterable)

3. **Reducing**

    This applies a reduction function to an iterable object that will produce a single cumulative value.


We will be looking exclusively at Mapping Function in this tutorial.

## Basic of map() Function

Simplest explanation of the map() function is that it applies a defined function to all the items in a specified iterable. Let us dig into the two main arguments of the map() function.

Function -  map(**_function_**, _iterables_)

The first argument function is a transformation function. Which means this function will apply a transformation to each item in an iterable object and return a new item. This function can be any user function or any inbuilt python callable such as built-in functions, classes, methods, and lambda functions. The function must only be called by name without using the round brackets() even if additional arguments are required.

Iterables-  map(_function_, **_iterables_**)

The second argument of the map() function is an object to be transformed by the defined function. This is an iterable such as list, array, dictionary, etc.  If multiple iterable arguments are passed, the defined function must be capable of taking all the iterables as arguments and apply the desired transformations to all iterables. However, in a case where multiple iterables with different lengths are passed, the map() function will stop when the shorted iterable is completed.

In the following example, we pass a list of numbers with a user defined function called multiply. Multiply function multiplies the given value by five. The map() function will apply this to all the items in the list.

```python
numbers_list = [1, 2, 3, 4, 5]

def multiply(number):
    number = number * 5
    return int(number)

multiplied_list = map(multiply, numbers_list)
print(list(multiplied_list))
```

**RESULT**

```
[5, 10, 15, 20, 25]
```

By using map() function, it eliminates the need to use a “for loop”. Let us look at the same function with a for loop.

```python
numbers_list = [1, 2, 3, 4, 5]
multiplied_list = []

for x in numbers_list:
    x = x * 5
    multiplied_list.append(x)

print(list(multiplied_list))
```

**RESULT**
```
[5, 10, 15, 20, 25]
```

By using map() function we can achieve the following advantages
*   Make the code more concise and easier to comprehend
*   Ability to write unit tests and debug the code easily as there is a clear differentiation between all the functions.
*   Increased reusability of the code as the multiply function can be reused anywhere in the program.
*   Less resource consumption, as any kind of loop can be a drain on system resources while a highly optimized built in function like map() is much more efficient.

These are the basics that we are trying to achieve using a functional programming style.

 
## Using python's built-in functions using a single iterable object

 **Functions to transform a list of integers**
Let's have a look at three functions that transform intergers into differnt numbers.
*   hex() - converts the given value to hexadecimal value
*   float() - converts the given number to decimal value
*   bin() - converts the given number to binary

```python
# Numbers List
numbers_list = [-30 , -10, 20, 35, 60, 101]

# Convert to Hexadecimal
hex_value = map(hex, numbers_list)
print(list(hex_value))

# Convert to Decimal
decimal_value = map(float, numbers_list)
print(list(decimal_value))

#Convert to Binary
binary_value = map(bin, numbers_list)
print(list(binary_value))
```

**RESULT**


```
Hex => 
['-0x1e', '-0xa', '0x14', '0x23', '0x3c', '0x65']
Decimal => 
[-30.0, -10.0, 20.0, 35.0, 60.0, 101.0]
Binary =>
['-0b11110', '-0b1010', '0b10100', '0b100011', '0b111100', '0b1100101']
```

**Functions to transform a list of strings**
This time, we are looking at couple of functions that transform stings.
*   len() - calculate the length of each string
*   hash() - get the hash value of each string (can be used regardless of the data type)

```python
# String List
fruits_list = ['apple', 'orange', 'mango', 'pineapple', 'watermelon']

# Get length of each item
string_length = map(len, fruits_list)
print(list(string_length))

# Get a reversed list
string_reversed = map(hash, fruits_list)
print(list(string_reversed))
```

**RESULT**

```
Length =>
[5, 6, 5, 9, 10]
Hash =>
[1170062481170996404, 4467272556740629919, -2237029943780611011, 412401351258394173, 8830894337672611814]
```

**Using lambda functions with map()**

In map() we can use a lambda function as the first argument.
*   Lambda to multiply the given value by 5

```python
# List
numbers_list = [1, 2, 3, 4, 5, 6]

# Lambda function as first argument (multiply by 5)
multiplied_values = map(lambda num: num * 5, numbers_list)
print(list(multiplied_values))
```

**RESULT**
```
[5, 10, 15, 20, 25, 30]
```

## Using python's built-in functions using a multiple iterable objects

When using multiple iterables, the function passed to the map() function must be able to receive a number of arguments equal to the number of iterables, and the map() function will stop with the end of the shortest iterable.

*   pow() - get the value of x to the power of y. For each item in list_one to the power of each corresponding value in list_two. Ex: list_one value = 2 to the power of list_2 value = 5. (25=32)
*   max() - get the max of the two given values

```python
# Lists
list_one = [1, 2, 3, 4, 5]
list_two = [3, 5, 6, 8, 9]

# Get the power value
power_value = map(pow, list_one, list_two)
print(list(power_value))

# Get the Max value of the given two values from the lists
max_value = map(max, list_one, list_two)
print(list(max_value))
```

**RESULT**
```
Power =>
[1, 32, 729, 65536, 1953125]
Max =>
[3, 5, 6, 8, 9]
```

**Manipulating multiple iterable string objects using a user defined function**

*   The _combinestring _function combines the values from each list and returns a joint string (joint greeting)

```python
# String List
list_one = ['Hi', 'Hello', 'Hey']
list_two = ['Jack', 'Mary', 'Sammy']

# Function to combine two strings
def combinestring(greeting, name):
    full_greeting = greeting + " " + name
    return str(full_greeting)

greeting_list = map(combinestring, list_one, list_two)
print(list(greeting_list))
```

**RESULT**
```
Greetings =>
['Hi Jack', 'Hello Mary', 'Hey Sammy']
```

## Transforming Iterable of Strings

When working with iterable string objects, using the map() function can be useful in easily achieving the desired outcome. The following are some examples of string manipulation using the map() function.

### Using methods of str object

The python str class contains a myriad of ways to manipulate strings such as str.capitalize(), str.lower(), str.swapcase(), str.title(), and str.upper(). These are methods that do not take any additional arguments. These can be implemented, as shown in the below examples.

```python
# String List
string_list = ['new york', 'england', 'paris', 'kuala lumpur', 'tokyo']

# Capitalize
print(list(map(str.capitalize, string_list)))
# Lowercase
print(list(map(str.lower, string_list)))
# Change Case
print(list(map(str.swapcase, string_list)))
# Title Case
print(list(map(str.title, string_list)))
# Uppercase
print(list(map(str.upper, string_list)))
```

**RESULT**
```
Capitalize =>
['New york', 'England', 'Paris', 'Kuala lumpur', 'Tokyo']
Lowercase =>
['new york', 'england', 'paris', 'kuala lumpur', 'tokyo']
Change case =>
['NEW YORK', 'ENGLAND', 'PARIS', 'KUALA LUMPUR', 'TOKYO']
Title Case =>
['New York', 'England', 'Paris', 'Kuala Lumpur', 'Tokyo']
Uppercase =>
['NEW YORK', 'ENGLAND', 'PARIS', 'KUALA LUMPUR', 'TOKYO']
```
Also, we can use methods in string class that take additional arguments such as str.strip(). In these instances, if you directly call the method without any additional arguments, the str.strip() function will take the default value of char. In this state, the function will remove all the white spaces from the string. If you need to change the default, you can use a lambda function to provide the argument.

**Using str.strip() with default char value**

```python
# String List
string_list_spaces = ['    new york', 'england    ', '     paris', '    kuala lumpur', '     tokyo    ']

# Strip all Spaces
print(list(map(str.strip, string_list_spaces)))
```

**RESULT**
```
['new york', 'england', 'paris', 'kuala lumpur', 'tokyo']
```

**Using str.strip() with a lambda function**

```python
# String List
string_list_spaces = ['___new york_', 'england_____', '_____paris', '___kuala _ lumpur', '____tokyo____']

# Strip all Spaces
print(list(map(lambda s: s.strip("_"), string_list_spaces)))
```

**RESULT**
```
['new york', 'england', 'paris', 'kuala _ lumpur', 'tokyo']
```

## Transforming Iterable of Numbers
 The map() function can be used to perform transformations on numerical values such as maths and arithmetic operations, converting string values to integer or floating values. The following samples will help us understand how these transformations are achieved.

**Using Math Operators**
*   Using a user defined function called multiply_multi, we will multiple each item in an iterable by 5 and 10 and return the values

```python
# Numbers List
number_list = [2, 5, 7, 9, 15]

# Function to multiply each value by 5 and 10
def multiply_multi(number):
    multiplication_one = number * 5
    multiplication_two = number * 10
    return multiplication_one, multiplication_two

# Pass each item to multiply_multi function
combined_list = map(multiply_multi, number_list)
print(list(combined_list))
```

**RESULT**
```
[(10, 20), (25, 50), (35, 70), (45, 90), (75, 150)]
```

**Using the methods in Maths module with map()**

*   In addition to user defined functions we can use the python Maths module and associated methods with map(). Below example provides how map() can be used with arithmetic methods sqrt() and factorial().
    *   sqrt() - this calculate the square root of any given number
    *   factorial() - multiple the given number from all the whole numbers down to 1 to obtain the factorial value (Example : 4! => 4 X 3 X 2 X 1 = 24)

```python
#Import Math Module
import math

# List
number_list = [1, 2, 4, 5, 6, 9, 10]

# Find the Square Root
squre_root = map(math.sqrt, number_list)
print(list(squre_root))

# Find the Factorial
factorial = map(math.factorial, number_list)
print(list(factorial))
```

**RESULT**
```
Square Root =>
[1.0, 1.4142135623730951, 2.0, 2.23606797749979, 2.449489742783178, 3.0, 3.1622776601683795]
Factorial =>
[1, 2, 24, 120, 720, 362880, 3628800]
```

**Using map() function to convert between units of measure**

We can use map() to convert values between multiple units of measure. We will look at the following example of converting between different units.

When creating a user-defined function to convert Kilograms to Pounds and vice versa, we assume that 1kg is equal to 2.2.20462262185 pounds(lbs) and 1lbs is equal to 0.45359237 kilograms(kg).

```python
# Function to convert Kg to Pounds
def kgtopounds(value):
    value = value / 0.45359237
    return value

# Function to convert Pounds to Kg
def poundstokg(value):
    value = value * 0.45359237
    return value

# List
values_to_convert = [2, 4, 5, 10, 35]

# Assuming the values in list are in Kilograms (Kg)
converted = map(kgtopounds, values_to_convert)
print(list(converted))

# Assuming the values in list are in Pounds (lbs)
converted = map(poundstokg, values_to_convert)
print(list(converted))
```

**RESULT**
```
Kilograms to Pounds =>
[4.409245243697551, 8.818490487395103, 11.023113109243878, 22.046226218487757, 77.16179176470715]
 
Pounds to Kilograms =>
[0.90718474, 1.81436948, 2.2679618500000003, 4.535923700000001, 15.875732950000002]
```

**Using map() function to convert string values to float and integer respectively**

 By using the inbuilt int() and float() methods we can easily convert string items to integers and floats respectively. The main consideration before using a conversion is to verify that the items in the iterable objects are values that can be converted.

```python
# Lists
float_string_list = ['12.55', '09.00', '45', '-16.65', '5.99']
integer_string_list = ['14', '8', '55', '-34', '2' ]

# Convert to Float
print(list(map(float, float_string_list)))

# Convert to Integer
print(list(map(int, integer_string_list)))
```

**RESULT**
```
To Float =>
[12.55, 9.0, 45.0, -16.65, 5.99]
To Integer =>
[14, 8, 55, -34, 2]
```

In the next example, we will send an unclean set of data to be converted, which will cause an error. The error occurs because we are trying to convert text values “Five” and “Twenty” to an integer. As the integer method does not recognize words, it throws a value error.

```python
# Lists
unclean_data = ['15', '10', '80', 'Five', 'Twenty']

# Unclean Data
print(list(map(int, unclean_data)))
```
**ERROR**
```
---------------------------------------------------------------------------
ValueError                            Traceback (most recent call last)
<ipython-input-56-0fcebcf58a9a> in <module>
      3
      4 # Unclean Data
----> 5 print(list(map(int, unclean_data)))

ValueError: invalid literal for int() with base 10: 'Five'
```

## The map() function with other types of iterable objects

In this section, we will look at how the map() function behaves with other types of iterable objects such as Tuples and Dictionaries. Any supported iterable type can be used in conjunction with any supported function objects.

**Using map() with Tuple**

Tuple is a finite ordered list of items. In python triple objects are defined by items separated by commas and enclosed in round brackets

```python
# Tuple
string_tuple = ('apple', 'orange', 'pineapple', 'banana', 'grape')
integer_tuple = (1, 2, 3, 4, 5)

# Convert String to UPPERCASE
uppercase_list = map(str.upper, string_tuple)
print(list(uppercase_list))

# Add 5 to each item in the tuple using a lambda function
calculated_list = map(lambda x: x + 5, integer_tuple)
print(list(calculated_list))
```

**RESULT**
```
Converted to String =>
['APPLE', 'ORANGE', 'PINEAPPLE', 'BANANA', 'GRAPE']
Added 5 to each item =>
[6, 7, 8, 9, 10]
```

**Using map() with Dictionary**

Dictionaries in python are a list of unordered items that are used to create a map of unique keys to values. Each key is separated from its value by a colon, items separated by commas inside curly brackets. In the below example, we check if the values in the list of the fruits are present in the dictionary keys and prints the value associated with each key.

```python
# Dictionary
fruits_dictionary = { 'apple' : 'fruit1', 'orange': 'fruit2', 'banana' : 'fruit3' }
fruits_list = ['apple', 'orange', 'pineapple', 'banana', 'grape', 'apple']

# Match Values of fruits list with fruits dictionary
match_list = list(map(fruits_dictionary.get, fruits_list))
print(match_list)
```

**RESULT**
```
Matched Result =>
['fruit1', 'fruit2', None, 'fruit3', None, 'fruit1']
```

As we can see from all the above examples, the map() function or mapping in python is a versatile function that can be used in various situations. Mapping can be used simply as a `for loop` replacement or a foundational element in writing programs in function style.

 

---
title: 'Data Types and Type Conversion in Python'
date: 2020-06-9
author: Danish Yasin
layout: post
permalink: /data-types-and-type-conversion/
---


# Data Types and Type Conversion in Python

In this tutorial, you will be learning about the various different data types in Python and how you can perform implicit and explicit type conversion. Each concept will be explained with the help of relevant code examples. 

Every variable you create in Python or any other programming language has a data type, which depends on the kind of data you are storing in that variable. 

Some of the most well-known data types are int, float, bool and string. These data types store numbers, fractional numbers and alphanumeric values respectively. So, the data type that you select has to be according to the value that you intend on storing in the variable. 

Python is a dynamically typed programming language, which gives you the freedom of not having to explicitly declare the data type while creating a variable. The opposite of this is statically typed programming languages like Java. 

The following code block will run seamlessly in Python, but if you try to do something similar in Java, it would give a compilation error that the types have not been defined. 


```python
int_ = 10
string_ = "10"

print(type(int_))
print(type(string_))
```


If you run this code block, you would get: 


```
<class 'int'>
<class 'str'>
```


Python is smart enough to detect whether you have entered an integer or a string and consequently assigns the appropriate data type. This is why the variable `a` is an `int` while `b` is a `string`.

In this tutorial, you will learn all about the use of most famous data types and how to perform type conversion and when it is appropriate to perform it. The agenda of this tutorial will be: 



*   Implicit and Explicit Conversion
*   Primitive and Non-primitive Data Structures 
*   Integer and Float Conversion
*   

Let’s start with the concepts of implicit and explicit conversion, they are pretty simple to understand.


## Implicit and Explicit Type Conversion 

Consider the following code block for example. 


```python
one_int = 5 
one_float = 5.5

result = one_int + one_float

print(type(result), result)
```


If you run this code, you’ll get the following output: 


```
<class 'float'> 10.5
```


Here, you can see that an int `one_int` is added into a float `one_float` and the compiler handles the conversion of data types automatically. This results in the `result` variable having a type of float. 

When data type conversion is taking place during run time or while compilation, similar to above, then this is known as implicit type conversion. 

In the code block, the conversion occurred automatically, without having to explicitly mention the data type in the `result` variable. 

Why did the compiler convert to float and not int? 

If the compiler had assigned the data type int to `result` then this would have led to the removal of the fraction part of the number. This would lead to loss information and consequently, inaccurate storage of data. Therefore, to maintain the accuracy of information, the compiler chooses a data type that protects the integrity of the data. 


### Explicit Conversion 

Let’s take the example described in the earlier section and perform explicit conversion on the variable `result` and observe what happens. Keeping the rest of the code unchanged, just update the following line: 


```python
result = int(one_int + one_float)
```


Running the complete code will output: 


```
<class 'int'> 10
```


As you can see, `result` is now an integer and we have lost the fraction part of `0.5` from the data. 

Explicit conversion is also known as type casting and it occurs when you have clearly defined which data type to convert to. Like, in the above example, `result` is explicitly type casted as an integer. 


## Primitive and Non-Primitive Data Structures 

The basic data types defined earlier in the tutorial are also known as primitive data structures. In Python, there are four primitive data structures, which are: 



1. Integers
2. Floats
3. Strings 
4. Boolean

Non-primitive data structures are the complex data types that do not store just a value, rather store a collection of values. Python has four non-primitive data structures: 



1. Lists
2. Tuples
3. Dictionary
4. Sets

Lists and tuples in Python are almost identical except that tuples are defined by enclosing elements in parenthesis `(2,3,4)`. Whereas, in a list, the values are defined in square brackets `[2,3,4]`. The other major difference is that tuples are immutable, meaning its values cannot be updated. 

Dictionaries store values in key-value pairs and the set is similar to list but the values are immutable and are stored unindexed and in an unordered fashion. 

This was just a brief overview of the non-primitive data structures, you can learn a lot more about how to use them and where to use them. 


## Converting Integers to Float and back

Integers and floats are the primitive data structures in Python that deal with numbers. You can easily convert them into one another by using existing methods in Python. 

The `int()` method was used in the earlier example, let’s see how you can convert from integer to float. 

Here’s the code: 


```python
one_int = 5
two_int = 5 

result = float(one_int + two_int)

print(type(result), result)
```


You can use the `float()` method to convert integer values into a float data type. If you run the code, you’ll get the following output: 


```
<class 'float'> 10.0
```


This is explicit conversion of integer values into float values. Earlier we transformed a float value into an integer value in a similar fashion. 


## Type Conversion with Strings

In python, strings hold alphanumeric values and more than often you will have to convert string to other data types and vice versa. 

Take the following code block for example, where you are printing the total value of a shopping cart. 


```python
soap_int = 2
shampoo_int = 5
cereal_int = 10 

total = soap_int + shampoo_int + cereal_int

print("Your total is: "+ total + "$")
```


Running this code will yield the following error: 


```
    print("Your total is: "+ total + "$")
TypeError: can only concatenate str (not "int") to str
```


The error occurs because you cannot implicitly concatenate integers into string. The compiler does not support this behavior. For this code to work, you have to use the `str()` method that converts a value into a string.

Updating the print statement to include the `str()` method:  


```python
soap_int = 2
shampoo_int = 5
cereal_int = 10 

total = soap_int + shampoo_int + cereal_int

print("Your total is: "+ str(total) + "$")
```


Now run the code and it will yield the following output: 


```
Your total is: 17$
```



### String to Integer

In the aforementioned example, you converted an integer to a string. Now let’s see how to convert a string that holds numeric values into an integer. 


```python
first_num = '55'
second_num = '5'

result = first_num + second_num

print("The result is:" + result)
```


In the code block above, you’re initializing two strings that contain numeric values and adding them up. If you run the code, you’ll get: 


```
The result is: 555
```


This is because the code does not add up the numeric values, rather concatenates the string values. 

To add the numeric values, you have to explicitly convert the string values into integers, like done ahead. 


```python
first_num = '55'
second_num = '5'

result = int(first_num) + int(second_num)

print("The result is:" + str(result))
```


Now if you run the code, you’ll get the output: 


```
The result is: 60
```


Since the `result` is now an integer, you have to convert it back to string while printing it. 

The string to integer conversion only occurs when there are only numeric values in the string. If you try to convert a string containing other characters into an integer, you’ll get an error. 

Let’s see this behavior in the following code block. 


```python
one_string = 'ten'

one_int = int(one_string)
```


Run this code and you’ll get the following error: 


```
    one_int = int(one_string)
ValueError: invalid literal for int() with base 10: 'ten'
```


This is because the compiler does not know that ‘ten’ is equal to ‘10’, therefore, do not try to convert string into integers in such a way. 


## Converting Lists to Tuples 

In Python, lists and tuples are almost similar, with two major differences. First one being the way both are defined, lists use square brackets `[]` while tuples use parenthesis `()`. The other difference is that lists are mutable while tuples are immutable. 

Take for example a tuple that stores the names of the user, now suppose you want to update the usernames. You can’t do so directly, if you try to update the value, like in the code ahead, you’ll get an error, shown below. 


```python
first_tuple = ('john','jean','joe','janice')

first_tuple[0] = 'new John'
```

```
    first_tuple[0] = 'new John'
TypeError: 'tuple' object does not support item assignment
```


To update the tuple, you’ll have to first convert it into a list. Let’s do it right now: 


```python
first_tuple = ('john','jean','joe','janice')

first_list = list(first_tuple)

first_list[0] = "jack"

first_tuple = tuple(first_list)
print(first_tuple)
```


First, you convert the tuple into a list then change the value at the appropriate index. Finally, you convert the list back to a tuple and print it out. You have now successfully updated the value in the tuple. 


```
('jack', 'jean', 'joe', 'janice')
```

Python supports a ton of other type conversion methods, you can convert decimal numbers to binary, octal or hexadecimal numbers. These methods make it easier for you to work with data that involves a lot of different types. This tutorial is limited to what has already been discussed and the rest will be covered in a separate post. 

## Conclusion

Working with Python is fun, the programming language makes it easy for you to work with different data structures. Its inbuilt methods allow for easy conversion and allow you to quickly convert your variables from one type to another. 

However, type conversion should be handled carefully as it can lead to unexpected output if the data is not clearly understood. Moreover, it is always a good approach to explicitly declare your variable types, where possible and have strong exception handling to avoid runaway variables during run time. 

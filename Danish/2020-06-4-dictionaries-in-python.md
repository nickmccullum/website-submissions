---
title: 'Using Dictionaries in Python '
date: 2020-06-4
author: Danish Yasin
layout: post
permalink: /dictionaries-in-python/
---

# Using Dictionaries in Python 

There are four in-built data structures in Python: list, tuple, set and dictionary. Each has its own use case, where list is basically a collection of objects, which can be string, integers or other complex objects. 

Each data structure is best optimized to solve certain problems. In this tutorial, our focus will be on using dictionaries in Python. In lists, elements are extracted with the help of unique indexes that point to each position of the list. 

Dictionaries are .pretty much the same as lists, with one big difference. Values are stored in “key-value” pairs and accessed using the keys instead of the indexes. Each key is unique in a dictionary and this is a more appropriate data structure when dealing with certain issues. 

In this tutorial, you will: 



*   Learn about dictionaries and how to use them 
*   Using dictionary comprehension
*   Using conditional statements in dictionary comprehension
*   Replace lambda functions and loops with dictionary comprehension

Let’s explain how and where you can use dictionaries. 


## What is a Dictionary? 

In simple words, a dictionary in Python is a data structure that stores key-value pairs, where values are accessed using the unique keys instead of indexes. 

It would be easier to understand dictionaries with the help of a real life example. Consider a system where you want to store a list of names of the users and their passwords. You can store it in a list and retrieve the results using the indexes, however, remembering indexes is not that easy. 

A better alternative would be to use the name of the user to extract the relevant password. This can be implemented with the help of dictionaries, you can input the meaningful key to extract values from the list. 

The keys in a dictionary need to be hashable. This means that running the key through a special hash function should return a unique output. Data types such as integers, floats, strings, tuples and frozensets are hashable. Whereas, lists, dictionaries and sets are not hashable. 

In practical terms, this means that you cannot set lists, dictionaries and sets as keys in a dictionary. 

Creating and using dictionaries is pretty straightforward in Python. Look at the following code block: 


```python
user_gender = {'jack':'male','john':'male','jean':'female'}

print(user_gender['jack'])
```


Here, the dictionary `user_gender` is created, which stores three users and their genders. The name of the users act like keys, whereas, their genders are the values stored against the keys. 

Running this code would give the following output: 


```python
Gender of Jack: male
```


Now let’s see what will happen if you try to access the value of jack by using the index instead of the key. 

Change the code to an index like: 


```python
print('Gender of Jack:', user_gender['0'])
```


Run it and it will output the following error: 


```python
Traceback (most recent call last):
  File ".\dict.py", line 5, in <module>
    print('Gender of Jack:', user_gender['0'])
KeyError: '0'
```


`dict.py` is the name of the python file that is being run. You can see that it gives the `KeyError`, which shows that there is no key ‘0’, which is the apparent index of the user Jack in the dictionary.


### What can you store in a dictionary?  

Where keys have to be hashable in a dictionary, there is no such condition on the values. Meaning, you can store almost anything in the values of a dictionary. You can store other dictionaries, lists and other complex data types as values in a dictionary. 

Here’s a complex dictionary that contains mixed data types. 


```python
mixed_dict = {'one':1, 'two':'two', 'three':[4,'four']}

print(mixed_dict)
```


If you run this code, you’ll get the whole dictionary printed out: 


```python
{'one': 1, 'two': 'two', 'three': [4, 'four']}
```


In the third entry, the dictionary contains a list. If you’re wondering how you can access the elements present inside this list, this is how: 


```python
third_elem = mixed_dict['three']

print(third_elem[0])
```


Python makes it pretty simple. You just extract the third element and then access the index of the list. All of this can also be done in a single line by the following command: 


```python
print(mixed_dict['three'][0])
```


Here you are accessing the third element of the dictionary and then accessing the first index of what is stored in the third element, which is a list in this case.  

Python has a lot of inbuilt functions for dictionaries that will help you while you work with them. 

To update the values of a dictionary, simply access them by using their corresponding keys. You can also extract the values and keys of the dictionary by using inbuilt functions. Here’s how you can do all of this:   


```python
print(mixed_dict)
mixed_dict['two'] = 'Three Thousand' 
print(mixed_dict)

keys = mixed_dict.keys()
values = mixed_dict.values()
print('\nAll of keys:',keys)
print('All of values:',values)
```


This will yield the following output: 


```python
{'one': 1, 'two': 'two', 'three': [4, 'four']}
{'one': 1, 'two': 'Three Thousand', 'three': [4, 'four']}

All of keys: dict_keys(['one', 'two', 'three'])
All of values: dict_values([1, 'Three Thousand', [4, 'four']])
```


As you’ll notice, the value corresponding to the key ‘two’ has been updated. 

You can delete specific values or clear the whole dictionary by using the following commands: 


```python
del mixed_dict['one']
print(mixed_dict)

mixed_dict.clear()
print(mixed_dict)
```


The key-value pair of ‘one’ has been deleted by using the first line of the code, whereas, by running the `clear()` command, you can clear the whole dictionary. Running the code will yield the following output: 


```python
{'two': 'two', 'three': [4, 'four']}
{}
```


The empty curly brackets indicate an empty dictionary. 


## Dictionary Comprehension

Python supports dictionary comprehension, which allows developers to create dictionaries in a more intuitive manner. You can create new dictionaries from existing dictionaries or from any other data. 

Dictionary comprehensions can include conditional statements to produce a new dictionary that contains only selective elements from the previous ones. 

Benefit of using dictionary comprehensions is that a well-written dictionary comprehension can replace multiple for loops and lambda functions. It will also increase the readability of the code, making it more expressive and easier to follow through. 

Let’s check out a practical example to understand the benefits of using dictionary comprehension. Take the following code: 


```python
dict_cube = dict()

for i in range(10):
    if(i%3 == 0):
        dict_cube[i] = i**3

print(dict_cube)
```


In this code, a dictionary is being created that stores the cube of all numbers within the range of 10 that are divisible by 3. 

Running this code will yield the following output: 


```python
{0: 0, 3: 27, 6: 216, 9: 729}
```


Now here’s how you can do the same thing by using dictionary comprehensions: 


```python
dict_cube = {num:num**3 for num in range(10) if num%3 == 0}

print(dict_cube)
```


You just turned four lines of code into one very concise and meaningful line of code that is easy to understand and gets the job done. It will print the same output. By using the dictionary comprehensions, you can replace loops like shown in the previous code block. 

You can also replace lambda functions, let’s take a look at the following code block: 


```python
# Points in miles
miles = {'p1':2,'p2':40,'p3':15,'p4':7.5}

# Getting the kilometre values and converting to int
kilometers = list(map(lambda x: int(x*1.60934), miles.values()))

# kilometer dictionary
kilo_dict = dict(zip(miles.keys(),kilometers))

print(kilo_dict)
```


Suppose you have a dictionary that contains four points and their distances in miles. You can convert these distances to kilometers by creating a lambda function shown above that takes the values of the dictionary and converts them to kilometers and stores them as an int. 

Here, `map()` iterates through the values of the dictionary `miles` and for each value the lambda function is employed and the results are eventually stored in a list. The `zip()` function connects the keys to the kilometre values. 

Running this code will yield: 


```python
{'p1': 3, 'p2': 64, 'p3': 24, 'p4': 12}
```


You can do the same thing with the help of dictionary comprehensions and use less code. Here’s how: 


```python
# kilometer dictionary

kilo_dict = {num:int(val*1.60934) for (num,val) in miles.items()}
print(kilo_dict)
```


Using dictionary comprehension, you have managed to significantly reduce the complexity of the code. This code is much easier to understand as compared to the earlier one that had many different concepts such as map and zip merged to perform a simple task. 

You can create nested dictionary comprehensions as well but, they beat the purpose of dictionary comprehension. Nesting them would make it difficult to understand the code, making it unclear what the objective of the dictionary comprehension is. 


## Conclusion 

You just learned everything there is about dictionaries in Python. With the completion of this tutorial, you are one step closer to becoming an expert Python developer. The concepts of data structures is a complicated one and majority lack the detailed understanding that is required to use them effectively in applications. 

This tutorial sheds an in-depth light on one of the important data structures of Python, which is dictionaries. You learned about dictionary comprehension as well, which is an effective technique that expert developers use while working with dictionaries. 

The next step would be to learn about lists, tuples and sets and learning how and when to use them.  

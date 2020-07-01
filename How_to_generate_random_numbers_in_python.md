
# How to Generate Random Numbers in Python

  

Random numbers have been an integral part of humans' lives for ages. Letting a die or a coin decide the fate of a person or a game has been a way of bringing impartiality to the table. It is also the same reason why randomness plays a huge role in computer science. Random numbers are used in computer science for many applications such as games, cryptography, and even computational neural networks that imitate the biological counterpart of humans.

Random numbers can be separated into two categories called true and pseudorandom numbers. While true random numbers generally require a hardware generator to be utilized, pseudorandom numbers are generated in a deterministic way by software and the results can also be reproduced given certain parameters.

In this tutorial, we will be looking at how to generate pseudorandom numbers in Python using both standard libraries and external modules.

## What Are Pseudorandom Generators (PRNGs)?

Randomness in real life is usually a game of entropy. However, when it comes to computers, we usually provide means of pseudo-randomness externally into the random number generator. These generators give us a notion of randomness, but in reality, the generated numbers are deterministic and the results can be duplicated over multiple iterations as well.

The way these generators work is that they are first tied to a number which is also called the seed value. It is the starting point of generating numbers followed by a sequence of deterministic random numbers. These sequences are decided by algorithms that utilize recursive methods that start from the seed value. There are a few algorithms in use in today's programming languages and the most common one is the [Mersenne Twister algorithm](https://dl.acm.org/doi/10.1145/272991.272995) that is equally distributed over 623 dimensions. Both libraries we will be using today in this tutorial make use of this algorithm to generate random numbers.

Now that we have an understanding of PRNGs, let's write some code with Python.

## Generate Random Numbers with Standard Python Module

Python has lots of standard libraries that make the whole ecosystem independently a complete one. In order for us to generate random numbers, we will be using the standard module [‘random’](https://docs.python.org/3/library/random.html). We will go over a few use-cases and attempt to get ourselves familiar with pseudorandom numbers and their concepts before we try an external library to get our tasks done.

### Generating Numbers without Seeding
    

In Python, we have seen some developers generate random numbers by just calling the function random() without involving any sort of seeding.

Let's try that out now.
```python
from random import random
print(random())
```
  

The output will be a floating-point value between 0 and 1. Since we did not involve any seeding, you must be wondering how did the program generate a number. In order to find the answer to that, let's look at the [source code](https://svn.python.org/projects/python/trunk/Lib/random.py) of random.

If we look at the function definition for `random()`, we will see that it has involved a seeding from within. Then, if we look at the function definition for `seed()`, it can be seen that in the event seeding is not explicitly called in the code, it uses system time in fractional seconds as a seeding point to initialize the PRNG.

### Generating Numbers with Seeding
    

Let us now get ourselves familiar with the seeding process.

Consider the following code.

  
```python
from random import seed
from random import random
seed(10)
print(random())
print(random())
```
  

Output:

> 0.5714025946899135
> 0.4288890546751146

  

If you try the same code on your device, it is apparent that the results are similar. Let us now try to set a different seed point and run the code.
```python
seed(20)
print(random())
print(random())
```
  

Output:

> 0.9056396761745207
> 0.6862541570267026

  

Again, the results are similar in both this tutorial and your device. Therefore, it can be understood that with the same seed values, we are able to reproduce the same results even across multiple devices.

We’ve established that using the `random()` function, we are able to generate floating-point values between 0 and 1. However, when we are dealing with numbers, we might also need to generate integer values. Let us next see how it is done.

  

### Generate Random Integer Values
    

Generating random integers with Python is really easy and requires no additional logic to convert or truncate the generated number. Let us use `randint(a, b)` function for that. a and b denote the min and max values we are expecting the PRNG to generate. Therefore, it will generate values between a and b.

Let us try to generate a pseudorandom integer between 0 and 5.

  
```python
from random import seed
from random import randint
seed(10)
print(randint(0,5))
```
  

Output:

> 4

  

We can further try to see how seeding works by trying to generate an integer by initializing the randint function to different seed values. Let us try to generate values for different seed values from 0 to 10.
```python
from random import seed
from random import randint
for i in  range(0,10):
	seed(i)
print('Seed: '+str(i)+' - Int: ' +str(randint(0,5)))
```
  

Output:

> Seed: 0 - Int: 3
> Seed: 1 - Int: 1 
> Seed: 2 - Int: 0 
> Seed: 3 - Int: 1 
> Seed: 4 - Int: 1 
> Seed: 5 - Int: 4
> Seed: 6 - Int: 4
> Seed: 7 - Int: 2
> Seed: 8 - Int: 1
> Seed: 9 - Int: 3

  
  

However, if you are wondering whether we can generate the value 5, try seeding the value 19.
```python
seed(19)
print(randint(0,5))
```
  

Output:

> 5

  

### Generate Floating-Point Numbers within a Range
    

We now know how to generate integer values and by default, they are being generated within a range specified by us. Let now see how we can do the same with floating-point values.

When we are using the `random()` function, we know that the values are being generated within the interval [0,1]. We can use simple arithmetic and remap this interval to generate numbers within a custom interval we want.

Let us say that we want to generate random floating-point numbers between 10 and 20. If we add 10 to every random number we generate, we will be changing the interval from [0,1] to [10,11]. However, we also want the interval to end at 20. Therefore, we can easily scale up the interval by a multiple of 10.
```python
seed(10)
new_rand = 10 + (20-10)*random()
print(new_rand)
```
  

Output:

> 15.714025946899135

  

Therefore, we can understand the following to map a random number to the range we want.
```python
new_rand = min_val + (max_val-min_val)*random()
```
  

### Generate Random Gaussian Values
    

The random module of Python also provides a facility to generate pseudorandom values that correspond with the Gaussian distribution. The `gauss(a, b)` function can be used for this task. a and b denote mean and standard deviation respectively for the Gaussian distribution from which we want to pull values.

Let us generate a few values from a Gaussian distribution with a mean of 0 and a standard deviation of 1.
```python
from random import seed
from random import gauss
seed(10)
for i in  range(0,10):
	print(gauss(0,1))
```
  

Output:

> -0.9537170080633371
> -0.45909415683868526
> -0.5992494722090856
> -0.32014240105647934
> 0.7217183074100624
> -1.717264917767424
> -0.33685383179186373
> -0.485574822383911
> -0.8837397625290433
> -0.11542039433046081

  

### Random Element Selection from Sequences (Lists, Dictionaries, Strings)
    

Imagine we have a list or a dictionary and we are required to draw random elements from them. Python standard module random has a function called `choice()` just for that task.

Let us see how we can randomly pull elements from a list.
```python
from random import seed
from random import choice
my_list = ['a','b','c','d','e']
seed(10)
choice(my_list)
```
  

Output:

> ‘e’

  

We can draw different elements randomly from the list by using alternative seed values.

Let us now see how we can do the same with a dictionary.
```python
from random import seed
from random import choice
my_dict = {0:'a', 1:'b', 2:'c', 3:'d', 4:'e'}
seed(10)
choice(my_dict)
```
  

Output:

> ‘e’

  

However, it should be borne in mind that the keys of the dictionary should be integers starting from 0 and consecutively incrementing.

Let us try to find the pattern here.
```python
seed(10)
randint(0,5)
```
  

Output:

> 4

  

We can understand that with the seed value 10, the randint function will output 4 for the pseudorandom integer between the range 0-5. From the `choice()` function we seeded at the same value, we can observe that the randomly selected element was the 4th element starting from a 0-indexing sequence with 5 elements. Therefore, we can conclude that `choice()` function behaves the same way as `randint()` and additionally returns the pseudorandom number-element that was generated based on the initialized seed value.

### Choosing a Subset from a List Randomly
    

The random module is so versatile and facilitating that it has provided us with a feature to select a subset from a bigger set randomly via the `sample(seq, size)` feature. As the arguments’ names suggest, this function takes in the set and the size of the expected subset as parameters.

Let us see it in action.
```python
from random import seed
from random import sample
my_list = [0,1,2,3,4,5,6,7,8,9,10]
seed(10)
sample(my_list, 5)
```
  

Output:

> [9, 0, 6, 7, 4]

  
  

We have randomly selected a 5-element subset from `my_list` set that has 11 elements. We can try different seed values and experiment with drawing different elements from the `my_list` sequence of elements.

  

### Shuffling A List
    

Shuffling feature is provided by the `shuffle(seq)` function that takes the sequence to be shuffled as an argument. It should also be kept in mind that this function directly modifies the original object. Let us see this function in action below.
```python
from random import seed
from random import shuffle
my_list = [0,1,2,3,4,5,6,7,8,9,10]
seed(10)
shuffle(my_list)
my_list
```
  

Output:

> [5, 2, 8, 3, 1, 10, 4, 7, 6, 0, 9]

  

Now that we have gotten ourselves familiar with the standard random module, let us move onto experimenting with the NumPy module.

  
  
  

## Generate Random Numbers with NumPy Module

NumPy Python library is popular among many other external modules that deal with tasks related to multi-dimensional matrices, arrays, and vectors. This module also has lots of mathematical functions related to matrices. However, a pseudorandom number generator is also an integral part of this module for machine learning model developers. There are functions that have been provided by the NumPy.random module and they can be found under their documentation comprehensively.

However, in this tutorial, we will only go through functions similar to the ones we experimented with earlier. Let us now explore the random module from NumPy.

### Generating Numbers without Seeding
    

Just like we did with the standard random library, let us generate a random number without seeding. It should be kept in mind that the same process happens underneath when we are attempting to generate pseudorandom numbers this way.
```python
from numpy.random import rand
rand()
```
  

This will output a random number depending on your system time.

However, this function offers an additional functionality the standard module does not offer. We can pass a parameter to specify the number of random numbers we want the PRNG to generate.
```python
from numpy.random import rand
rand(4)
```
  

Output:

> array([0.73641456, 0.40761286, 0.93791648, 0.5100432 ])

  
  

### Generating Numbers with Seeding
    

We already know that these pseudorandom numbers are deterministic. Let us try the same approach with NumPy.
```python
from numpy.random import rand
from numpy.random import seed
seed(10)
rand()
```
  

Output:

> 0.771320643266746

  

We can also verify that the standard random and NumPy.random modules have different outputs although their underlying mechanisms are similar.
```python
from random import random
from numpy.random import rand
from random import seed as seed1
from numpy.random import seed as seed2
seed1(10)
seed2(10)
print('Standard: ' + str(random()))
print('NumPy: ' + str(rand()))
```
  

As both the modules have a seed function, we are importing them as `seed1` and `seed2` respectively corresponding to standard and NumPy modules.

Output:

> Standard: 0.5714025946899135 
> NumPy: 0.771320643266746

  

### Generating Integer Values
    

NumPy also offers a feature to generate integer values as we did with the random module. However, in addition to the parameters that specify upper and lower bounds, this function also takes the optional parameter of the number of random values.

We will now experiment with it.
```python
from numpy.random import seed
from numpy.random import randint
seed(10)
randint(0, 5)
```
  

Output:

> 1

  

We will not generate 5 random numbers between 1 and 100.
```python
from numpy.random import seed
from numpy.random import randint
seed(10)
print(randint(0, 100, 5))
```
  

Output:

> [ 9  15  64  28  89]

  

### Generating Gaussian Values
    

Generating Gaussian values is a feature that can be found on the NumPy.random as well. However, instead of `gaussian()`, we have the function `randn()` to perform the same task. However, the catch is that with `randn()`, the standard deviation and mean are by default 1 and 0 respectively. We will have to scale the outputs if we are to find Gaussian values for different parameters.
```python
from numpy.random import seed
from numpy.random import randn
seed(10)
randn()
```
  

Output:

> 1.331586504129518

  
  

Let us scale it to a mean of 10 and a standard deviation of 100
```python
from numpy.random import seed
from numpy.random import randn
new_mean = 10
new_std_dv = 100
seed(10)
new_mean + randn() * new_std_dv
```
  

Output:

> 143.1586504129518

  
  

## Conclusion

Random numbers are very important in computer science for various applications. For most day-to-day scenarios, we only use pseudorandom numbers and it is rare that we have the resources to afford generating true random numbers.

We understand that the pseudorandom numbers we generate are deterministic and therefore, can be reproduced as long as we initialize the sequence with the same seed value. We also experimented with the random module from Python standard packages as well as the random module from the external library NumPy.


# Understanding Null in Python

## What is Null?
Null means no value is defined. Null is used to represent a pointer that doesn't point to anything or when a variable or an argument is empty. In many other programming languages, Null is often defined to be 0. Java and PHP are two popular languages that use Null.

Let’s see how Null is used in PHP and Java.

PHP
```php
<?php  
$exampleVariable = NULL;  
?>
```
  

Java
```java
exampleVariable = null;
```
  
However, the concept of Null is quite different in Python as Python has None to define Null objects or variables. While None serves the same purpose as the Null, None doesn’t define 0 or any other value. None is its own object in python.

Check the examples below
```python
exampleVariable = None
```

```python
exampleVariable = None  
print(type(exampleVariable))
```

**RESULT**
![](https://lh3.googleusercontent.com/x6RSU8tsE3sL5lTajToR1qpIxk9uMrA83PqOjPZoNHEoOYz1xxMs8_kK-plqDzUt-VW0aZzajt5A-wysZ_RmDG8q9LzC6UFEg20rbyKGPP_kA1Ky-H3viQv8VFGvxcSYbSM4_uaVVZl28MIZLw)

  
## Assigning None to variables in Python

In other programming languages, variables can be declared without assigning an initial value to them. Also Null can only be assigned to specific types of variables. However, you can’t declare variables without assigning values as it will give an error.

See the example below.
```python
Variable  
print(Variable)
```
**Result**
![](https://lh6.googleusercontent.com/jtXpkkAsMhmhfVyawr1RstCu9pL4PlD-B0gw49x0w_0iEXQaRp8LiitY8L77qCuy7Z7OztZo9PxvAYxOw6jq8T-S8L14TfNC8BGBCVHDzeURvq1-erGx1BCE2UeHIoaMJv79KJl7CfVudBRZig)

In such instances, you can assign None at the variable declaration But in Python, you need to assign a value to a variable at the initial declaration and None can be assigned to any type of variable.
```python
noneVariable = None  
print(noneVariable)
```
**RESULT**
![](https://lh4.googleusercontent.com/qQpB1c1znNmr85vbzTYOy25oPKc56xTBDmkSEluAv_FUqj8rl5hkp50Pd_m145ZsiCH-aYHbANzC0JEaLlIFj_R9qtvrw1lfEG-Y56LaguyYbJ5-IEA5gXn43w1OpG-EKHvdXZU6zhdTZnCYdQ)

If a variable is not defined properly, it will cause a NameError. When None is declared, the variable will be a Null object. In Python, None is only equal to None. It is not equal to an empty string, the Boolean value False, or the numerical value 0.

The IF statement in the python code below demonstrates this clearly. It checks if the “noneVariable” is equal to the empty string, 0, False, or None. The IF condition only validates when the variable compares with None object.

```python
noneVariable = None

if noneVariable == "":
    print("None is Equal to an empty string")
elif noneVariable == 0:
    print("None is Equal to 0")
elif noneVariable == False:
    print("None is Equal to False")
elif noneVariable == None:
    print("None is Equal to None")
```
  
**RESULT**
![](https://lh3.googleusercontent.com/sKmnuvV7pJTKmXfLLMGUkl-reJS4U894ilIIdRnNGEsqpPXRTATha4HJG60NfLHtatcvIjgJHLZv8YoWHUKAC243lhc2gDDNFGbOGSv3rAX7Lzx3BWOnY7fW5PDOH_UKNh5rbzTzWELna7a1RA)

## Understanding more about None

Any function without a proper return statement returns None. In Python, None object is so ubiquitous in REPL, it won’t print None unless the user explicitly tells it to. The following examples show how None is identified in Python.

### Python None as a return value.
```python
def examplefunction():
    pass

examplefunction()
print(examplefunction())
```

**RESULT**
![](https://lh5.googleusercontent.com/Mvk_YBMeP7shHSLE0IRKzfvvWygZYW6w8-oRiIl8c7lI8mKmaDXGmXhz6jUuhkWwV7Z-U3PaE1Kqk9A9ZX3Q8HGTw6E0jxK9WCS22LsW7A8uIW4aaRci8jI0Yxvu5kWqTk9uQ3gV6UFhoTGIlg)

In this instance, when a function is created with no explicit return value, Python returns None as the result. Because Python REPL won’t print None unless explicitly declared we use the print statement to identify the output.
```python
print()
print(None)
print(print('Hello'))
```

**RESULT**
![](https://lh5.googleusercontent.com/M8vB6p0aXAqQpfWLFTTHLyXL3SQ9oZw-EB9-4BfWGs-O3aZ_TcaJhuv1GphRjqbPsETGF-E1EzcEW_H9uAxGm_vQnmSGZWOzoqrkZx0G_pvehWX9k4voZ1wJnMSLq09-YjTn-bX83jueXPOf-g)


In the python print() function, there is no return value to the function itself. Because of this, the first print() statement in the above example returns no explicit value. When the None object passes to the The second print statement, it returns None. Finally, in the nested print() statement the print(‘Hello’) returns the Hello string as the result. But as the print statement itself has no explicit return object, it will be shown as None.

### None to identify missing or default parameters.

Let's look at the docs of list.sort function.
```python
help(list.sort)
```

**RESULT**
![](https://lh4.googleusercontent.com/9tu9IUylef--YXKLeP_z4vYiJQFLxgs-MTQAKfUyyuDXFL9JBVvRCmEQmPJ1jy3V_WKX3-EnIKhtDc-ld8GlARp8t-DkpbeHJks7EcBko_VzupWf4GD0z0Ctu4MzEfuEpXcD-MDu1uceHdRtYg)

As you can see in the output, None is assigned to the “key” parameter. Although the key parameter is required here, it is not provided. So, it indicates None as the default parameter.

## Using None for Comparison

The identity operators and equality operators can be used to test whether two variables are referring to the same object. So, you can use them to test when a variable has been assigned as None.
Both the equality operator(“==”) or the identity operator “is” can be used to check this.
```python
# Equality Operator
x = None

if x == None:
    print("x is equal to None")
else:
    print("x is equal to None")

# Identity Operator
y = None

if y is None:
    print("y is equal to None")
else:
    print("y is equal to None")
```

**RESULT**
![](https://lh6.googleusercontent.com/xU8uCrQ7UgvPK-jVrmEkTnasWrumJ_Jkzuxn5KRBcGX2E5C7LdX9bhpGklG8AEBPVrwRcE7lNPHWWus5TXAuYyJgTdqMdaujGtxm9yLJtXfSM6Vr7n8VOnsWwOkoTIyYEnTKlguh8wRBOiLMIA)

However, there is a difference between the identity operator “is” and the equality operator “==”.

The identity operator checks if both the operands are referring to the same object while the equality operator checks if both operands are equal in value. The below examples demonstrate how these operations can be used properly in comparison tasks.

**Check if an object is None**
```python
import re

stringvalue = "Barry"

# Check if "stringvalue" matches "Harry"
match = re.match(stringvalue, "Harry")

# Check if match is a None object
if match is None:
    print("item do not match")
else:
    print("item do match")
```

**RESULT**
![](https://lh5.googleusercontent.com/FWHfHbVLSQLPSyn4KNB-YaRNx_ZBo2fRIZ8YYXdL6VQnRQng0qwWuwIE_HLIyMZ0VLCpQYDHuo6IhCFlHuf69EvlferxJt7RG8Ij_kLaHqDcOPiuuQq_iSjpTEKI-qQelg8AR_a_W8utuaPGRQ)

In this example, we check if two values match with each other. . The match function will return a None object if the two values passed to it do not match. Then we use identity operators to validate the results.

If you want to correctly verify a value is a None object, using identity operators is the most optimal as equality operators can be fooled when other user defined objects that override the value. The following example shows this scenario.

```python
class CheckComparison:
    def __eq__(self, other):
        return True
    
x = CheckComparison()

# Equality Operator
print(x == None)

# Identity Operator
print(x is None)
```

**RESULT**
![](https://lh3.googleusercontent.com/Y4LXpL6F3r18FBVh0uVQ_9C0SAQKPol6IN-bRpSFKtNNmMRCzpLzy2HiUs4gKzn12IOoH28VrTijVt_iYAiCCx_wxmMSL5npB1m7bqT5hPpNjqNG1EkuZ3dbkKHX2tMJKvY3m2eQI1BqIDB08Q)

The equality operator has been overridden by the object equality (__eq__) of the class CheckComparision and this results in an incorrect output. As identity operators cannot be overridden, the intended result is displayed.

## Using None as a Value in Python

In python, None can be added to a set as an item. Similarly, it can be used as a function parameter.

To illustrate that, we will check the following example. We create an empty class that will be used as the signal not to append. Then create the function “addto_list” with two parameters to add an element to a given “set”.

```python
# To be used as a signal not to append
class AddNone:
    pass

# Main Function
def addto_list(new_element=AddNone, initial_set=None):
    if initial_set is None:
        initial_set = {}
    if new_element is not AddNone:
        initial_set.add(new_element)
    return initial_set

# Initial Set
colours = {"pink", "purple", "blue", "green", "yellow", "orange"}
print(addto_list(initial_set=colours))
```

**RESULT**
![](https://lh4.googleusercontent.com/ktU9mj290m6F637wrUw3Yc8OylyoYgKnZCgiCmCpYC8Et1UAl5wEJrqZrl_70hoLIU0lfcfrdR2Y1Luo1jMD3o6-eWapGnGfbKQrku6jlTscYxILIv0gKsW2tC3D7T92QRcaEmdhmP8Fy1FU8g)

As we have defined default values for each parameter, it is not necessary to pass both values for each parameter. We pass the “colours” set as the initial set. This results in output returning the “colours” set back as it's not a None object. Please note that because sets are unordered, the resulting set shows the items in a random order.

```python
# To be used as a signal not to append
class AddNone:
    pass

# Main Function
def addto_list(new_element=AddNone, initial_set=None):
    if initial_set is None:
        initial_set = {}
    if new_element is not AddNone:
        initial_set.add(new_element)
    return initial_set

# Initial Set
colours = {"pink", "purple", "blue", "green", "yellow", "orange"}
print(addto_list(None, initial_set=colours))
```

**RESULT**

![](https://lh3.googleusercontent.com/MVeDEmkypIe2f7X7Ck7fIz-NI4Vop0rlkn0e4ZGuwlzEZGXKrnlBfuQEAw8YLkR1tdYvRwf2Wjmeg6HZ_CF2c5HWT4-3jFpNay9AwWbKrKNQpoW261P0iypaok5ANMaCM7m6YU69JgsfydnssA)

In the above instance, we pass both parameters. But for the new_element, we pass a None object, and for initial_set, we pass the colours set. As you can see the None object is added to the set. When None is a valid input item, it can be added to a set.

## None in Tracebacks

Let’s have a look at one of the common issues related to None. If you see an error like “AttributeError: NoneType object has no attribute …”, it means you have tried to use None keyword in an incorrect way. One of the common reason for it could be calling a method on a variable that is defined to be Null.

Let us consider the following examples.

```python
# fruits set with items
fruits = {"cherry", "banana", "apple"}
fruits.add("orange")
print(fruits)
```
**RESULT**
![](https://lh5.googleusercontent.com/fOLDb6NFi4bYwmLcu4wq4lmeNA52lBI8Npug3BymWS0Vd30tPFPXAa9Fc7oEd1sVPTbd2JADD7wVqIN-oJFL2TMsY1vSibAhy4htnb2py0xfVxvs4lC9jx8XZSkVmc5CuMiRj4Sph5rWe0Yt8A)

In this instance, we create a set called “fruits”, and add another value called “orange”. Here, the code executes successfully as the Python sets contain the add method. However, the following code won’t be successful

```python
# fruits as a None Object
fruits = None
fruits.add("strawberry")
print(fruits)
```

**RESULT**
![](https://lh6.googleusercontent.com/PPNEb7Gk8MpE3ZDfQDq8V4NBtUx6dJTNziiPEzUqEnwPXzD4mB-BIzygWwhFxWxVdasCBifCEs4Z3wXReVy90FjUAwppDx4n9ukpH1AkC9fK9yEH_PjT3wUhDJF7hng-qtLWC_eKVNo4TQd2Iw)

In the above example the “fruits” variable is declared as a None type object. As there is no add method associated with None object this results in an error.

So next time, when you get a traceback like this in your code, first, check the attribute that raised the error. In the above example, it was the add() method. Then you can find the object on which the method was called. After figuring out how the object became None, you can work on fixing the code.

## Conclusion

All in all, as a first-class citizen in python, None plays a significant role in programming. None can be used for various tasks such as checking missing values, comparing results. Being an immutable keyword None is a solid choice for parameters in functions over mutable types.
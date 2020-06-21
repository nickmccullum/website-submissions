# Comparing Objects in Python: &quot;==, !=, is, and is not&quot;

In Python, the identity operators ( **is** and **is no** t) and the equality operators ( **==** and **!=** ) have a small difference between them. You would have experienced unexpected behavior while using the **is** or **is not** operators to compare values. In Python, the **is** and **is not** operators are used to check if two objects share the same memory location and the **==** and **!=** operators are used to compare their values. .

In this tutorial, we will discuss the differences between equality operators and identity operators and when to use them. We will also see what leads to an unexpected behavior when we use the **is** or **is not** objects.

# Table of Contents

You can skip to any specific section using the table of contents below.

- Equality Operators Vs Identity Operators
- Comparing Objects Using Equality and Identity Operators
- How Python Operators Work Behind the Scenes
- Using the Right Operators

# Equality Operators Vs Identity Operators

As we mentioned in the earlier tutorial, everything in Python is an object and has a specific memory location associated. The **is** and **is not** operators in Python check if two objects share the same memory location. Note that two objects with the same value will not share the same memory location. The identity of an object can be checked using the **id()**.

In cPython, some objects that have the same value have the same id. The commonly-used integers form – 5 to 256 are interned in cPython. That is, each number in this range occupies a fixed and singular place in the memory.

The sys.intern() can be used to compare the memory addresses instead of comparing each character.

from sys import intern

a = &#39;sample&#39;

b = &#39;sample&#39;

a is b

print (id(a))

print (id(b))

a = intern(a)

b = intern(b)

a is b

print (id(a))

print (id(b))

Output:

47183403408368

47183402865976

7183403408368

7183403408368

Initially, the memory address of both the variables are pointing to a different location. However, the intern function ensures that they are referring to the same variable.

# Comparing Objects Using Equality and Identity Operators

Now, let us see an example where we will use both the **is** operator and the **==** operator to understand the difference between both these operators.

data1 = []

data2 = []

data3=data1

if (data1 == data2):

    print("True")

else:

    print("False")

if (data1 is data2):

    print("True")

else:

    print("False")

if (data1 is data3):

    print("True")

else:

    print("False")

data3 = data3 + data2

if (data1 is data3):

    print("True")

else:

    print("False")

The output of the above code will be as follows:

This is true.

This is false.

This is true.

This is false.

- In the first _if_ condition, the value of both the lists data1 and data2 are being compared. Both the lists data1 and data2 are empty lists. Therefore, the first _if_ condition gives the output as TRUE.
- In the second _if_ condition, the memory locations of data1 and data2 are compared. Hence, the output of the _if_ condition is FALSE.
- Now, data3 and data1 share the same object memory. As a result, the third _if_ condition will be TRUE.
- Since the two lists are concatenated, it will create a new list. Therefore, the fourth **if** condition will be FALSE.

Now let us look at the **!=** operator and the **is not** operator. **!=** is defined as the not equal to operator. If the operands on either side of an expression are of the same value, the **!=** operator will return the output as FALSE and they are of different value, the output will be TRUE.

Let&#39;s see this below example.

a = 120+2

b = 122

if (a != b):

    print("Not equal")

else:

    print("Eqaual")

if (&quot;computer&quot; != &quot;comp&quot;):

    print("Both are different")

else:

    print("Both are same")

The output of the above code will be as follows:

Equal

Both are different

Let&#39;s now look at the **is not** operator. Like the **is** operator, the **is not** operator compares the memory location of the two objects. It checks the **id()** of the objects being compared and returns FALSE if they are same. If they are different, it returns TRUE.

x=10

y=x

print (id(x))

print (id(y))

if (x is not y):

   print("Memory location not same")

else:

   print("Memory location same")

x=10

y= 20

print (id(x))

print (id(y))

if (x is not y):

    print("Memory location not same")

else:

    print("Memory location same")

94383631757216

94383631757216

Memory location same

94383631757216

94383631757536

Memory location not same

The first _if_ statement compares if the memory location of x and y are same or different. From the output, it is clear that both x and y share the same memory location. Then, x and y are assigned two different memory locations. This is confirmed from the output of the second if statement.

# Using the Right Operators

Now that we have understood the difference between the **==** and **!=** operators and the **is** and **is not** operators, respectively let us understand when we should use these two operators.

## Comparing Equality

As a standard rule, except when comparing to **None** , use the **==** and **!=** operators to compare values. When you want to compare if two values are equal, use the **==** and **!=** operators. Here, you are not concerned about the memory location of the variables. You only want to check if the content in both these variables are the same.

## Comparing Object Identity

If you want to compare the identity of two objects, that is if they are stored in the same memory location, use the **is** and **is not** operators. These operators are very useful in comparing variables to **None** and are preferred over class methods while comparing variables to **None**.

# Conclusion

In this tutorial we have learnt that we can compare the object location of two objects using the identity operators and we can use the equality operators to compare the value of two Python objects. We also saw few examples of these operator types. The tutorial also explained when to use the identity and equality operators. This should help you in preventing the unexpected behavior in your code when you compare two objects.
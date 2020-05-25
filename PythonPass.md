
# Python Pass: Doing Nothing, and Why That's Useful

The `python pass` statement is called a _null operation_, this means that when it is executed, nothing happens! It is a useful placeholder when a statement is required syntactically, but you desire no code to be executed, for example:

```python 
def my_func (arg):
	pass # A function that does nothing (yet)
```

```python 
class my_class:
    pass # A class with no methods (yet)
```

This might seem completely useless at first but there are many great reasons to use the Python `pass` statement:

-   Speed up the development stage
-   Explicitly silence exceptions
-   Create type hierarchies

## Speed Up the Development Stage

This is probably the most useful place to use the Python pass statement, so it's important to understand why we use it here. 

When developing, we sometimes want to ignore the explicit behaviour of a function in order to continue programming the main flow of our program with the intention of adding the functionality later.

For example, let's build a program that takes in a message from the user, replaces all the spaces in that message with underscores, and then prints it out to the user.

We might start like so:
```python
if __name__ == "__main__":
	in = input("Please enter your message: ")

	## Convert all spaces to underscores
	result = in.replace(' ', '_')

	print(f"Here is your resultant: {result}")
```

However, what if you needed to validate the user input before the manipulations and then write the resulting message to a file?

When adding a new feature to existing code I (along with many other developers) like to use **_stubs_** to add functionality to the existing code while staying organized.

```python
def validate_input(msg):
	if (len(msg) > 0):
		return True
	else:
		return False
# TODO
def write_to_file(msg):
	pass
	
if __name__ == "__main__":
	in = '' # empty string

	# Validate, looping until valid message received
	while (validate_input(in) is not True):
		in = input("Please enter your message: ")

	## Convert all spaces to underscores
	result = in.replace(' ', '_')
	print(f"Here is your resultant: {result}")

	write_to_file(result) # Call our stub
```

In this example we have a stub for the `write_to_file` function, which we have not implemented just yet, however, the stub reminds us that it is still necessary to do (hence the TODO) not to mention that this saves us time right now from implementing that function.

In the end, we will need to implement the function, however, at this point, we are able to confirm that the rest of our program is functioning correctly before getting around to that.

This helps speed up development because at this point if we were to find a bug, the scope is smaller meaning that the bug will be easier to find.

Having that call to the stubbed function, `write_to_file` is useful to remind you to implement it later but also to avoid the need to add the call in later once you do implement the function. 

Keep in mind that `write_to_file` is a very simple use case, you could probably implement this function in a few minutes and not need to stub it out at all. However, this concept applies to much more complicated function such as encryption algorithms that need to be thoroughly tested out in isolation before being applied to a login system. 

It's helpful to insert a call to the stubbed function in where it is needed so that when you do implement that function you don't need to worry about it. The whole point of using a stub is to simulate that the functionality is already there when it is not.

Next, let's go through a slightly different use case, still relating to speeding up our development cycle. 

When using conditional statements within a loop to decide how the data should flow through your program you sometimes need to simply, do nothing in a certain case.

For example, counting the number of odd and even numbers in a sequence while **_ignoring all 0's._**

```python
def count_numbers(sequence):
	evens = 0
	odds = 0
	
for (num in sequence):
	# Even numbers should be divided by 2
	if num % 2 == 0:
		evens = evens + 1
	# Odd numbers will not divide by 2 evenly
	elif num %2 != 0:
		odds = odds + 1
	# Otherwise, zeroes should be ignored
	else:
		pass
```

In this case, you need to account for the current number in the sequence being a 0, but you really don't need to do anything with that information, so simply, do nothing. 

You could easily rearrange this solution and check for if the number was a 0 and step to the next loop iteration, or add an extra check for the 0's and count them, then simply not return the data. However, in this case, it's much simpler and less time consuming to just do nothing with `pass`!

A common question about the Python pass statement asked is the difference between `pass`, `break`, and `continue`. The differences between these three statement can most easily be understood by look at an example:

```python
if __name__ == "__main__":
	print("break:")
	for val in  "Python":
		if val == "h":
			break
		print(val)
		
	print("----")
	print("continue:")

	for val in  "Python":
		if val == "h":
			continue
		print(val)
		
	print("----")
	print("pass")

	for val in  "Python":
		if val == "h":
			pass
		print(val)

	print("The End")
```
Output:
```python
break:
P
y
t

----
continue:
P
y
t
o
n

----
pass
P
y
t
h
o
n
The End
```

`break` will end the loop while `continue` and `pass` both allow the loop to complete. However, the subtle difference between `continue` and `pass` is that the `continue` statement will restart the loop on its next iteration. 

When the condition (`val == "h"`) was met and `continue` was called, `val` was increment and the loop continued. 

When the condition (`val == "h"`) was met and `pass` was called, nothing happened at all and the loop continued. 


## Explicitly Silence Exceptions

There are certain cases where you may want to simply ignore an exception being raised, this can be helpful when the exception is irrelevant in the performance of your script. 

This may sound like a bad coding practice, and it very well can be if used improperly! 

Here is an example of the correct way to use this trick, taken from the `xml` library for Python:

```python
try:
    self.version = "Expat %d.%d.%d" % expat.version_info
except AttributeError:
    pass # unknown
```

The `AttributeError` is probably the most commonly used error, in this case, often time we want to ignore this error for various reasons. The main time to use this technique is when logging optional object attributes from an instance during runtime. 

In this case, the `version` attribute is not an option for the class, and therefore the line of code `self.version = "Expat %d.%d.%d" % expat.version_info` will raise an `AttributeError`. Since the developer was only using this value for logging, they don't need to escalate this exception at all. 

An example of what **NOT TO DO** would be this:
```python
try:
    os.unlink(some_filename)
except:
    pass
```

Can you guess why?

That's right, it's because here we would be ignoring ALL types of errors raised within the try block. This means that any error that occurs, whether it be an `AttributeError` or `FileNotFoundError` we are simply ignoring it. 

This is very bad coding practise because you could potentially be ignoring a highly fatal error in your code. So as a general rule of thumb, if you plan to use the `pass` statement to silence an exception, make sure you are deliberately silencing just the one!


##  Create Type Hierarchies

Type hierarchies is basically a fancy phrase for using inheritance to create a family of parent-child relationships between classes. In this case, we would be able to inherit functionality from a parent class into a child class in order to extend or override the behaviour. 

The most prevalent example of creating type hierarchies in Python would be `Exceptions`. Fundamentally, all Exception classes work the same way, however, it's beneficial to create a subclass with a much more specific exception name in order to more accurately represent the error's happening in your code.

An example of this would be the `ImportError` which is a parent class to children such as the `ModuleNotFoundError`. The `ImportError` is raised when an `import` statement has trouble successfully importing the specified module, which, if that's the case, can be more accurately represented by the `ModuleNotFoundError`.

In this case, the code behind the `ImportError` and the `ModuleNotFoundError` is identical, however, when the exceptions are raised to a developer the name "ModuleNotFound" gives a much more accurate indication of what the problem is. Most likely indicating an issue with the path to the module you're trying to import. 

So, in this case, we have a *type hierarchy* that looks like this:
- [`BaseException`](https://docs.python.org/3/library/exceptions.html#BaseException)
	- [`Exception`](https://docs.python.org/3/library/exceptions.html#Exception)
		-  [`ImportError`](https://docs.python.org/3/library/exceptions.html#ImportError)
			- [`ModuleNotFoundError`](https://docs.python.org/3/library/exceptions.html#ModuleNotFoundError)
			
Now, how does this pertain to a pass statement? Well, as I mentioned the behaviour of the `ModuleNotFoundError` would be the same as it's parent class `ImportError`. The code would look like this:

```python
class ModuleNotFoundError(ImportError):
	pass
```

This is a very simple usage of the Python `pass` statement which allows you to create a subclass that does not change the behaviour of the parent but in this case, allows you to create a more accurate name of the class. 

Let's put this example in a more user-friendly context, say we had a program where you needed to read a file from a server. The `FileNotFoundError` may be a very useful exception to detect within your code. 

However, let's assume that when you attempt to read assets from your server there are multiple different file types (images and text files). In this case, to be more specific in your code and to help developers understand the exception, you can create a type hierarchy like so:

```python
# Subclass of FileNotFoundError for images
class ImageNotFoundError(FileNotFoundError):
	pass
	
# Subclass of FileNotFoundError for text files
class TextFileNotFoundError(FileNotFoundError):
	pass
```

So now we have this type hierarchy:
- [`BaseException`](https://docs.python.org/3/library/exceptions.html#BaseException)
	- [`Exception`](https://docs.python.org/3/library/exceptions.html#Exception)
		-  [`OSError`](https://docs.python.org/3/library/exceptions.html#OSError)
			- [`FileNotFoundError`](https://docs.python.org/3/library/exceptions.html#FileNotFoundError)
				- `ImageNotFoundError`
				- `TextFileNotFoundError`

Here, `ImageNotFoundError` and `TextFileNotFoundError` are called siblings because they are both children of the same parent. You can think of it as a tree and both these errors are living at the same level making them siblings.

This sort of functionality can be extended even further to add more accurate information for your exceptions to be even more accurate to the error being raised. 

```python
# Subclass of ImageNotFoundError for jpeg's
class JpegNotFoundError(ImageNotFoundError):
	pass

# Subclass of ImageNotFoundError for png's
class PngNotFoundError(ImageNotFoundError):
	pass	
```

Now that we've created more accurately named errors for our program to raise, let's see what they would look like to a developer. 

We can write a simple script to raise our exception:
```python
if __name__ == "__main__":
	raise  FileNotFoundError(errno.ENOENT, os.strerror(errno.ENOENT), 'foobar')
```
Which will give this output:
```python
Traceback (most recent call last):
	File "pass.py", line 7, in <module>
		raise FileNotFoundError(errno.ENOENT, os.strerror(errno.ENOENT), 'foobar')
FileNotFoundError: [Errno 2] No such file or directory: 'foobar'
```

When raising one of our children classes, `JpegNotFoundError` for example,  we can see the difference is minimal but provides a lot more information to a developer.

```python
if __name__ == "__main__":
	raise  JpegNotFoundError(errno.ENOENT, os.strerror(errno.ENOENT), 'foobar')
```
Which will give this output:
```python
Traceback (most recent call last):
	File "pass.py", line 7, in <module>
		raise JpegNotFoundError(errno.ENOENT, os.strerror(errno.ENOENT), 'foobar')
JpegNotFoundError: [Errno 2] No such file or directory: 'foobar'
```


## Conclusion

Now you should have a better understanding of what the Python pass statement is, how it's useful and when you should be using it. 

Learning how to use Python pass ***properly*** will benefit you most with speeding up your development stage and can make you a more efficient developer! 

It's important to understand the proper usage of Python's pass statement in order to avoid bad coding practices and introducing bugs in your code. Remember, if you are using `pass` to silence an exception to be very specific and never silence all errors!



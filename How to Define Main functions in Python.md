# How to Define Main Functions in Python

Python is a very interesting programming language to learn. In programming languages, when an operating system runs a program, a special function called main() is executed automatically. Python also has a main(). In Python, the focal point of the execution of any program is the main() and it acts as the entry point of the code. It is important to define the main function to start executing a program. It is important to define the main function in Python to start the execution of the program. The program does not get executed as a module, it has to be run directly.

In this tutorial, we will understand what a main function in Python is and how it works. We will also see how the variable \_\_name\_\_ works in Python.

# Table of Contents

You can skip to any specific section using the table of contents below.

- Basic main() in Python
- Mode of Executions
- Best Practices Using main() in Python

Basic main() in Python

In Python scripts, a conditioning statement sometimes follows a defining function. Let&#39;s look at an example.

```python
print(&quot;Hello World&quot;)

def main():

print(&quot;A basic main function&quot;)

if \_\_name\_\_ == &quot;\_\_main\_\_&quot;:

main()
```

Output:

```
Hello World

A basic main function
```
In the above code, the main() prints the message &quot;A basic main function&quot; when the script is executed. This is followed by a conditional statement (if statement). The if statement compares the value of \_\_name\_\_ to the string &quot;\_\_main\_\_&quot;. If the conditional statement is true, it prints &quot;A basic main function&quot; upon execution. This is a very common code pattern when files need to executed as Python scripts or imported in a module. It is important to realize that the in Python \_\_name\_\_ is defined based on how the code gets executed. Let us first understand the different modes of execution in Python before seeing how the above code works.

# Modes of Execution

One can instruct the Python interpreter to execute a script in two ways.

- Execute the file as a Pythons script.
- Import the code from a Python file to another file.

Irrespective of how you choose to execute your scripts, Python defines a special variable with a string. The value of the string will depend on how the code gets executed.

Let&#39;s look at an example where we will use a file, mode\_of\_execution.py.

```python
print(&quot;We are testing different modes of execution.&quot;)

print(&quot;The variable \_\_name\_\_ shows the context in which the above file runs.&quot;)

print(&quot;The value of \_\_name\_\_ is:&quot;, repr(\_\_name\_\_))
```
In this file, we have three print statements defined. While the first and second print statements are only printing some random statements, the last print statement will use the inbuild Python function repr() to print the value if the variable \_\_name\_ with the introductory phrase present in the print statement.

The inbuilt function repr() provides an option to produce the printable form of an object. In the above example, repr() returns the string value present in the variable \_\_name\_\_.

So far, you would have encountered the words module, file, and script in this tutorial. Though there is not much difference between these terms, it is important to know the purpose of these terms.

File: This is a Python file that contains a script. The file extension is .py.

Script: This is a Python file that you want to execute to accomplish a task. The script is executed from a command line.

Module: This is a Python file that you want to import from a script, an interactive interpreter, or another module.

## Executing the file as a Python script

Here, we are trying to execute the file as a Python script. While executing a script, the code the Python interpreter is executing cannot be interactively defined. You can execute the file mode\_of\_execution.py from the command line using the below code.
``` shell

$python3 mode\_of\_execution.py

We are testing different modes of execution.

The variable \_\_name\_\_ shows the context in which the above file runs.

The value of \_\_name\_\_ is: &#39;\_\_main\_\_&#39;
```
In the above example, note that the variable \_\_name\_\_ has a value &#39;\_\_main\_\_&#39;. This indicates that the variable is of type string. In Python, strings defined between single quotes and doubles quotes have no difference.

You can obtain the same output if you include a shebang line in your script and execute the file directly using ./mode\_of\_execution.py. You can also use %run magic in your Jupyter or IPython notebook. You can also execute this script by adding the m-argument to the command line.

In all of the above three instances, the variable \_\_name\_\_ has the same string value &#39;\_\_main&#39;.

## Importing the code from a Python file to another file

Let us now see how we can import the code from a Python file to another file. Python allows you to take advantage of modules that are already built using the _import_ keyword.

When you use the import keyword, Python executes the statements in the defined module. Let us see how we can import the mode\_of\_execution.py file. To do so, you must import this file by starting the interactive Python interpreter.

```python
import mode\_of\_execution

We are testing different modes of execution.

The variable \_\_name\_\_ shows the context in which the above file runs.

The value of \_\_name\_\_ is: &#39;\_\_mode\_of\_execution\_\_&#39;
```
In the above code, note that the interpreter executers three print functions. The first two lines in the output are the same as what it was when the file was executed as a script. However, the third print statement gives a different output.

When the code is imported, the value of \_\_name\_\_ and the name of the module that is being imported will be set the same. This is clear in the third output. The value of \_\_name\_\_ is &#39;mode\_of\_execution\_ and this is same as the .py Python file we are importing from.

Note: If you try and import the same module again without quitting Python, you will not get any output.

# Best Practices While Using Python Main Functions

We now know how differently Python can handle the different modes of execution. It is also important to understand the best practices while using the main function to be able to use the code for multiple purposes. Some of the best practices are as follows:

- Ensure that the majority of the code is in a function or a class.

As you are aware, all codes are executed when the interpreter imports the module. Your code could sometimes take longer to run a computation, write a file, or print information that could confuse your terminal.

In such instances, instead of letting interpreter execute the code after it imports the module, you will want to have a control that triggers the execution of the code. To do so, you will have to ensure that the code is in a function or a class.

- Control the execution of the code using the \_\_name\_\_

This is useful when you want a function to be executed while running a script from the command line instead of executing it when the file is imported by the interpreter. In such instances, we can give the variable \_\_name\_\_ different names and use a conditional statement to alter the behavior of the code.

- Run the code inside the main()

Though the main() is not assigned any significance in Python, it is always a best practice to define the main() as the entry point function and to run the code inside this main(). This helps other programmers who read your code to know where your code starts.

- Use the main() to call other functions

Your script might read data from a different source (a disk, web api file, or a database), processes this data, and writes this data to a different location. In such cases it is best to define these tasks in a different function and then use the main() to call these functions.
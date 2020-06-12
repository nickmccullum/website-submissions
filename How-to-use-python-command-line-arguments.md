
# How to Use Python Command Line Arguments

  

Generally, command line arguments are parameters that are input to the program at its invoking moment. CLIs are used for various purposes from testing to providing the developer and users with an interface to communicate with the program. Just like in most programming languages, Python offers this feature as well. There are in-built as well as custom libraries to deal with arguments in Python.

  

Although there are many more arguments. Understanding the basics are crucial. Let us start with a simple program you can write to familiar yourself with arguments.
```python
import sys
print('Arg count:' + str(len(sys.argv)))
for i in  range(0,len(sys.argv)):
	print(f'Argument {i}: {sys.argv[i]}')
```
  
  

If we execute this from the terminal/shell with the command python mypythonscript.py Hello World, the following will be the output (Modify the command with your file name).

    Arg count:3
    Argument 0: mypythonscript.py    
    Argument 1: Hello    
    Argument 2: World

  

If we go through the outcome line by line, it says that there are 3 arguments. The first argument is the file name and subsequent arguments are the ones that were input during invoke time.

Let us now look at what sys.argv is.

  

## What is sys.argv?

  

From the previous example, it can be seen that the command line arguments can be accessed by sys.argv. Although it may seem straightforward at the beginning, we should also understand the following use-cases and aspects of sys.argv before we go deeper into command line arguments.

### Accessing arguments
```python
import sys
print(f'First argument: {sys.argv[0]}')
print(f'Second argument: {sys.argv[1]}')
```
  

If we execute this with python mypythonscript.py Hello, we would get the following output.

    First argument: mypythonscript.py    
    Second argument: Hello

  

As we already know, the first argument is also the file name. Let us change the code a bit.
```python
import sys
print(f'First argument: {sys.argv[0]}')
print(f'Other arguments: {sys.argv[1:]}')
```
  

Let us execute this with python mypythonscript.py Hello World How Are You.

Output:

    First argument: mypythonscript.py    
    Other arguments: ['Hello', 'World', 'How', 'Are', 'You']

  

We now understand that the arguments can be accessed by using their index. We can also treat sys.argv the same way we treat a list. However, that is the very reason why we should be more careful when we are dealing with sys.argv.

  

### Sys.argv is global

Sys.argv is available globally through the scopes of each Python program. This means, all the imported modules will have access to sys.argv. However, sys.argv is also mutable. For instance, consider the following code.
```python
import sys
print(f'Before: {sys.argv}')
sys.argv.pop()
print(f'After : {sys.argv}')
```
  
  

Let us execute it with python mypythonscript.py 1 2 3 4 5

Output:

    Before: [' mypythonscript ', '1', '2', '3', '4', '5']    
    After : [' mypythonscript.py', '1', '2', '3', '4']

  
  

Therefore, it is also advised that the required variables are stored in separate variables of the program is complex and intricate.

## Python Command Line Arguments

We have introduced ourselves to Python command line arguments. Let us now look deeper into them.

Usually, when invoking a Python script, the following is the usual syntax.

`python -Flags script.py arg1 arg2 arg3 …. argn`

  

In this invoking command, script.py is compulsory as it is what specifies which script is being run. Both flag arguments are optional. However, as this tutorial is about command line arguments, we will be working with both flags, arguments, and a few more additional features that are important to command line arguments.

  

### Flags

Flags in command line arguments specify how the invoking program or instruction should behave.

Example:-

Let us run the following in the terminal.

`python`  

This would open the Python shell.

    Python 3.8.3 (default, Jun 10  2020, 16:00:55)    
    [GCC 5.4.0 20160609] on linux    
    Type "help", "copyright", "credits"  or  "license"  for more information.    
    >>>

  

However, if we add a –V flag to it as follows, it will return its version.

`python –V`

Output:

    Python 3.8.3

  

### Arguments

Arguments are inherited from POSIX standards. They are also called operands. They can be used to pass data or parameters to the invoking script to function as intended. In real life, they are mostly used by developers for testing purposes.

### Subcommands

Subcommands are also a form of arguments. Although these subcommands are not used explicitly while running Python scripts, they are a part of the Python ecosystem as pip uses subcommands. Commands like install, freeze under pip can be called subcommands. Not only they use pip's usual commands but also each feature’s own options. For instance, if we are to install modules specified by the requirement.txt file, we would use the following command.

`pip install -r requirements.txt --no-index`

  

In the above command, install is the subcommand.

  

## A Standard Python Library - Argparse

Python has a few standard libraries like argparse, getopt, optparse that ease up all the hassles in putting together a piece of code with command line arguments. These libraries are heavily used and community-favored. In this tutorial, we focus on argparse as it is the most favored by the community from all command line argument libraries.

Argparse is the go-to option for many developers when it comes to command line arguments. It comes in handy when writing user-friendly interfaces which happen to be command line based. Let us start by practicing a simple argparse example.
```python
import argparse
if  __name__ == "__main__":
	parser = argparse.ArgumentParser(description="""
	Let us create a user contact.""")
	parser.add_argument("name", help="Name of the user")
	parser.add_argument("password", help="Password")
	parser.add_argument("email", help="Email")
	args = parser.parse_args()
	name_v = args.name
	password_v = args.password
	email_v = args.email
	print("Name : " + name_v)
	print("Password : " + password_v)
	print("Email : " + email_v)
```

If we run python mypythonscipt.py, it will output,

    usage: mypythonscript.py [-h] name password email
    
    mypythonscipt.py: error: the following arguments are required: name, password, email

Then we can run it with the arguments it requires. Notice how we can parse arguments with whitespaces. (We can also use double quotes encapsulating the words we want to send instead of a backward slash.)

`python mypythonscript.py Johnny\ Cash abc1234 johnny.c@example.com`

  

It will output,

    Name : Johnny Cash  
    Password : abc1234    
    Email : johnny.c@example.com

  
  

In the above code, we have created a parser object with argparse.ArgumentParser. Then arguments have been defined with the add_argument function.

Let us now run the command

`python mypythonscript.py -h`

with the help flag.

Output:

    usage: mypythonscript.py [-h] name password email   
    Let us create a user contact.    
    positional arguments:    
    name Name of the user    
    password Password    
    email Email    
    optional arguments:    
    -h, --help show this help message and exit

  

It can be seen that by default, argparse has defined a help option as well.

  

Let us add optional functionality to our code. Notice the --gender argument in the following.

  
```python
import argparse
if  __name__ == "__main__":
	parser = argparse.ArgumentParser(description="""
Let us create a user contact.""")
	parser.add_argument("name", help="Name of the user")
	parser.add_argument("password", help="Password")
	parser.add_argument("email", help="Email")
	parser.add_argument("--gender", help="Gender")
	args = parser.parse_args()
	name_v = args.name
	password_v = args.password
	email_v = args.email
	gender_v = args.gender
	print("Name : " + name_v)
	print("Password : " + password_v)
	print("Email : " + email_v)
	print(f"Gender : {gender_v}")
```
  

Notice that in the last line, we have not concatenated the gender_v variable. This is because in the event of no argument being present for the Gender, it will be a NoneType and NoneTypes cannot be concatenated.

  
  
  
  
  
  

If we run the code with the help flag, it will output,

    usage: mypythonscript.py [-h] [--gender GENDER] name password email  
    Let us create a user contact.    
    positional arguments:    
    name 			Name of the user    
    password 		Password    
    email 			Email    
    optional arguments:    
    -h, --help show this help message and exit    
    --gender GENDER Gender

  
  

If we give the command

 `python mypythonscript.py Johnny\ Cash abc1234 johnny.c@example.com`

it will return

    Name : Johnny Cash    
    Password : abc1234    
    Email : johnny.c@example.com    
    Gender : None

  

Now if we include the `–gender` flag and the argument with

`python mypythonscript.py Johnny\ Cash abc1234 johnny.c@example.com --gender male`

it will return,

    Name : Johnny Cash   
    Password : abc1234    
    Email : johnny.c@example.com    
    Gender : male

There you go with the basics of argparse.  
  

## Alternative Approaches Instead of CL Libraries

We have now been familiarized with argparse. However, it is also important that we have an idea about underlying mechanics of using pure command line arguments. We will now take a look at two common approaches in dealing with these in practice. Although these are not the only approaches, these can be used to lay a solid foundation in understanding pure command line arguments.

### File Handling

Before we get into file handling, there is one more thing to be known; Secure Hash Algorithms. SHA is a family of cryptographic hash functions that generates a hexadecimal number out of an input. Although the newest version is SHA-3, in this tutorial we will use SHA-1 for demonstration purposes.

Let us write a function to take a file name as a command line argument and output its SHA-1 .
```python
import hashlib
import sys
def  get_sha1(file_name: str) -> str:
	sha_hash = hashlib.sha1()
	with  open(file_name, mode="rb") as f:
		sha_hash.update(f.read())
	return sha_hash.hexdigest()
for arg in sys.argv[1:]:
	print(arg)
	print(get_sha1(arg))
```
  

We can run this with the command python mypythonscript.py anotherfile.txt

This would return,

    anotherfile.txt    
    da39a3ee5e6b4b0d3255bfef95601890afd80709

  

You can confirm the accuracy of the SHA-1 by running the following in the terminal.

`sha1sum anotherfile.txt`

  

Output:

    Da39a3ee5e6b4b0d3255bfef95601890afd80709 anotherfile.txt

  
  

### Standard Streams

There are 3 standards streams in Python that denote inputs, outputs, and errors. We can use these to our advantage by chaining them one after another.

We will demonstrate this by printing a list of company names first and trying to sort them as follows.
```python
def  get_names():
	names = ['GreenHub', 'MassTent', 'SilkWise', 'CoachMe', 'AirBuild']
	for name in names:
		print(name)
get_names()
```
  

It will output

    GreenHub    
    MassTent   
    SilkWise    
    CoachMe    
    AirBuild

  

However, if we execute the script with,

`python mypythonscript.py | sort`

  
  
  

it will output the following.

    AirBuild    
    CoachMe    
    GreenHub    
    MassTent    
    SilkWise

  

As you can see, they are sorted.

Now let us add some notifications before and after the lines.
```python
def  get_names():
	names = ['GreenHub', 'MassTent', 'SilkWise', 'CoachMe', 'AirBuild']
	for name in names:
		print(name)
print('Initiating')
get_names()
print('End')
```
  
  

However, if we send the same instruction, it will output the following.

    AirBuild    
    CoachMe    
    End    
    GreenHub    
    Initiating    
    MassTent    
    SilkWise

  
  

It is visible that even our notifications have been sorted. We can print out notifications separately by sending traces to the standard error stream via our notification print statements.
```python
import sys
def  get_names():
	names = ['GreenHub', 'MassTent', 'SilkWise', 'CoachMe', 'AirBuild']
	for name in names:
		print(name)
print('Initiating', file=sys.stderr)
get_names()
print('End',file=sys.stderr)
```
  
  

This will output,

    Initiating   
    End   
    AirBuild    
    CoachMe    
    GreenHub    
    MassTent    
    SilkWise

  

Therefore, by changing the error stream to the output stream, we can disengage our sort argument from sorting the notifications.

  

## Validating Command Line Arguments

Validating your command line arguments are important in ensuring there are no extreme cases that fail your code. Let us look at one example that we used earlier with file handling.

### File Validation

Rerun the file handling code from the previous section. What happens if we specify a file that does not exist?

`python mypythonscript.py filedoesnotexist.txt`

  

It will return,

    filedoesnotexist.txt    
    Traceback (most recent call last):    
     File " mypythonscript.py ", line 23, in <module>    
    print(get_sha1(arg))    
     File " mypythonscript.py ", line 11, in get_sha1    
    with open(file_name, mode="rb") as f:    
    FileNotFoundError: [Errno 2] No such file or directory: ' filedoesnotexist.txt '

  
  

Instead of this, we can have a prompt to ask for the correct file name.

  

Look at the modified code below. Notice the newly added try and except statements.
```python
import hashlib
import sys
def  get_sha1(file_name: str) -> str:
	sha_hash = hashlib.sha1()
	try:
		with  open(file_name, mode="rb") as f:
		sha_hash.update(f.read())
		return sha_hash.hexdigest()
	except:
		print("\nWrong file name! Retype the file name correctly\n")
		file_name = input()
		return get_sha1(file_name)
for arg in sys.argv[1:]:
	print(arg)
	print(get_sha1(arg))
```
  
  

If we run the same command,

`python mypythonscript.py filedoesnotexist.txt`

  

now it will return a prompt.

    Filedoesnotexist.txt    
    Wrong file name! Retype the file name correctly

  

We can type the file name into the prompt and it will return the file's SHA1.

  

## External Python Packages for Command Line Arguments

We already know how to write pure command line arguments and also to ease up the code development with the help of standard modules such as argparse. However, there are also a few additional modules that have been written which are really sophisticated. We will go over a simple implementation of two of the most community favored modules.

### Click

This module is heavily used in the Python microwebframework, Flask. This has also quite a bit of functionality that stretches beyond command line arguments. However, we will try a simple hello world example here

Install click first.

`pip install click`

Let’s code.
```python
import click
@click.command()
@click.option('--count', default=1, help='number of greetings')
@click.argument('name', default ="World")
def  hello(count, name):
	for x in  range(count):
		click.echo('Hello %s!' % name)
if  __name__ == '__main__':
	hello()
```
  
  

We can give the command

`python mypythonscript.py`

  

It will return,

    Hello World!

  

If we give a name argument,

`python mypythonscript.py Johnny`

  

Output,

    Hello Johnny!

  

### Prompt Toolkit

This is one of the best packages to make your code more user-friendly and colorful. In this, we will implement a simple hello world example to get ourselves familiar

Let’s first install the package.

`pip install prompt-toolkit`

  

Let’s code.
```python
from prompt_toolkit import prompt
from prompt_toolkit import print_formatted_text
from prompt_toolkit.formatted_text import ANSI, HTML, FormattedText
from prompt_toolkit.styles import Style
print = print_formatted_text
def  hello():
	name = prompt('What is your name?: ')
	style = Style.from_dict({"hello": "#fb1222", "name": "#14afb4 italic",})
	text_fragments = FormattedText(
[("class:hello", "Hello "), ("class:name", name), ("", "\n"),]
)
	print(text_fragments, style=style)
if  __name__ == "__main__":
	hello()
```
  
  

If you run the command

`python mypythonscript.py`

  

It will return a prompt to enter a name.

    What is your name?:

We will enter a name here and press enter.

    What is your name?: Johnny

  

It will output,

    Hello  Johnny

  
  
  
  

## Conclusion

This tutorial covered all the important topics in laying a good foundation of command line arguments. Command line arguments are used to acquire inputs from the user to change the behavior of the program. They are extremely important to a developer and with additional libraries, textual user interfaces that are beautifully designed can be built to offer a better user experience.











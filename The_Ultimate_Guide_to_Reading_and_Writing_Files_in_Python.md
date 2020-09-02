# The Ultimate Guide to Reading and Writing Files in Python

  

## 1. Introduction
    

Python is one of the best languages for many of the elements of computer science including data science, server-side developments, database handling, etc. Almost all the time, all these tasks require reading and writing information from and to external files. Therefore, it should be in every Python developer’s repertoire to properly handle and deal with files. In this tutorial, we will learn about how to perform various kinds of file handling tasks that might be required for tasks such as, but not limited to, writing a text file, logging data to a server log, and reading big data files.

## 2. Concept of a File
    

For today’s topic, it’s important that we have a proper idea of what a file is if we are to handle them the right way. If we look at any file, it can be identified as a set of bytes that consists of data. These files generally have three main components called ‘’header, ‘data’, 'end of file’. As the name suggests, the header contains metadata such as file name, its type. Data consists of the contents of the body of the file that has been written by an author. Finally, the end of the file contains a character that signals the end of the whole file. There are thousands of registered file types and in this tutorial, we will mainly focus on the .txt format. We will now look at a few key concepts that are important when we are learning about file handling.

1.  ### Path
    

When a file is to be accessed, its location has to be known. We can specify using the file path. The path contains 3 major components. They are the folder path, the file name, and the extension. The extension is the portion that starts after the filename with a period(.) symbol. If the file we are interested in resides in the current working directory, then we are not required to specify the folder path as we can directly mention the file using only its filename and the extension.

2.  ### Newline/End of File
    

In files, it is important that we do understand that there are line endings or newlines. When we consider different operating system environments, sometimes the way these line endings have been defined is different from each other. For instance, in Windows, carriage return (CR) and line feed (LF) markers are used together. However, in Unix/Linux environments, only the line feed marker is used. Therefore, developers should be aware of these kinds of subtle differences between different OS environments.

3.  ### Encoding
    

Character encoding is another aspect of files one should keep an out for. Encoding can be defined as the mechanism of translating the byte data to characters that are readable by humans. The most popular encoding methods are ASCII and Unicode. If you are to parse these without errors, the correct encoding type has to be known.

Now that we have acquired enough background knowledge, we are ready to move on. Before we move to the next section, go ahead and open up a Jupyter Notebook, or a Python script in your favorite IDE. Have a sample text file called ‘mytextfile.txt' saved inside your working directory.

Let's get started.

## 3. Opening a File
    

Opening a file is the very first thing we should do before we are able to read its content or to write new content to it. Opening a file in Python is intuitive. Let's go ahead and open a file.


```python 
my_file = open('mytextfile.txt')
```


If we output the file,

```python
print(my_file)
```

It would say

```
<_io.TextIOWrapper name='mytextfile.txt' mode='r' encoding='UTF-8'>
```

The mode here is open for reading and is specified by the ``‘r’``. The encoding has been identified as Unicode ``‘UTF-8’``.

Every time we open a file, we should always remember to close the file. Unless the file is closed, there could be unwanted resource leaks and might lead to unexpected behavior. Therefore, we should establish a way to close the file following the opening of it. There are two major ways of doing that. We will look at them now.

1.  ### ``try`` , ``finally`` blocks
    
```python
try:
	my_file = open('mytextfile.txt')
	#Further processing comes here

finally:
	my_file.close()

```
In this, we are opening the file inside a try block and then closing it inside a finally block. If this method looks lengthy, then you might be interested in knowing the next approach.

2.  ### Using ```with```
    

```python
with open('mytextfile.txt') as my_file:
	#Further processing comes here
```
We are using the 'with' statement here followed by the open statement. This way, Python handles any issues internally and closes the file by itself. We recommend that you use this approach along with another argument inside the open function specifying why you are opening this file.

Example:

```python
with open('mytextfile.txt', 'r') as my_file:
	#Further processing comes here
```

As we already know, ‘r’ specifies that this is in the read mode. There are a few more modes as follows.

``‘r’`` - Open for reading

``‘w’`` - Open for writing or overwriting

``‘rb’`` - Read using binary mode

``‘wb’`` - Write using binary mode

``‘a’`` - append

We will now go ahead and see how we can read the content in a file.

## 4. Reading a File
    

The content of mytextfile.txt is as follows.

```
Hello World
How you been
Good to see you
My old friend
```

As you can see, there are four lines in our text file.

There are a few approaches we can use to read the above file as follows

1.  ### read(size)
    

This function takes in an optional size argument that specifies the number of bytes to be read. If size = -1 is passed or if no arguments are passed, the entire file is read.

Example:

```python
with open('mytextfile.txt', 'r') as my_file:
	print(my_file.read(5))
```

Output:

```
Hello
```

If we look at the code, we can see that we are instructing the interpreter to read 5 bytes from the file that has returned us with 5 characters from the file we opened. If we are to further understand how this works, look at the following.

```python
with open('mytextfile.txt', 'r') as my_file:
	print(my_file.read(5))
	print(my_file.read(5))

```
Output:

```
Hello
Worl
```
We have instructed to perform the read() function twice and read 5 bytes each time. From the output, we can understand that it has returned 5 characters in two chunks. Although in the 2nd line, there are only 4 letters, the space character has also been taken into consideration when the function returned the 2nd chunk.

2.  ### readline(size)
    

This function also takes in an optional size argument. It specifies the number of characters from a line that should be read. If size = -1 is passed or if no arguments are passed, the entire line is read.

Example:

```python
with open('mytextfile.txt', 'r') as my_file:
	print(my_file.readline(1))
	print(my_file.readline(2))
	print(my_file.readline())
```

Output:

```
H
el
lo World
  
```

If we look at the code, we are instructing the interpreter to read and print 1, 2 characters from the first line respectively and then finally print all the remaining characters of the same line. (Notice the newline character as well)

3.  ### readlines()
    

This function reads the rest of the lines from the file and returns them as a list.

Example:

```python
with open('mytextfile.txt', 'r') as my_file:
	print(my_file.readlines())
```

Output:

```
['Hello World\n', 'How you been\n', 'Good to see you\n', 'My old friend\n']
```

If we compare the output with our original file, we can see that all of the lines have been returned as a list in the output.

Now that we have covered the basic functions, let's see how we can properly read files while iterating over each line.

```python
with open('mytextfile.txt', 'r') as my_file:
	current_line = my_file.readline()
	while current_line !='':
		print(current_line, end = '')
		current_line = my_file.readline()
```

Output:

```
Hello World
How you been
Good to see you
My old friend
```

If you look at the code, what we are doing is reading each line completely and moving to the subsequent one until we are met with an empty string that is also the end of file character.

We can also do the same by using the readlines() method and printing the elements of the list one by one as follows.

```python
with open('mytextfile.txt', 'r') as my_file:
	for current_line in my_file.readlines():
		print(current_line,end = '')
```

This would output the same as above.

We can also further make it easier by iterating over the my_file object itself as follows.

```python
with open('mytextfile.txt', 'r') as my_file:
	for current_line in my_file:
		print(current_line,end = '')
```

The output is the same as the above. However, it should be kept in mind to pass the end parameter to the print function as set it as the empty string instead of the default newline character. We are doing this as each line of our files already contain a newline character and we do not want to include an additional newline character by the print function.

We will now look at how we can write to files.

## 5. Writing to a File
    

If you recall, we did have multiple functions to read files. More or less the same, we do have two functions as below that can be used to write to files.

1.  ### write(text)
    

We are passing the text we want to write to the file

Example:
```python
with open('mytextfile.txt', 'r') as my_file:
	content_list = my_file.readlines()

with open('mytextfile_reversed.txt', 'w') as my_new_file:
	for line in reversed(content_list):
		my_new_file.write(line)
```

If you look at what we have done here, we are first reading the content of our original file ``mytextfile.txt`` and, saving it in the content_list object. Then later, we are opening a ``mytextfile_reversed.txt`` file that gets created as if it does not exist already. Then we are writing the elements in the reverse list as lines.

If you go ahead and open the ``my_new_file.txt``, you will see that we have written the lines of our original file to this new file in the reversed order.

  

2.  ### writelines(sequence)
    

We can write a sequence to the file using this function.

Example:

```python
with open('mytextfile.txt', 'r') as my_file:
	content_list = my_file.readlines()

with open('mytextfile_reversed.txt', 'w') as my_new_file:
	my_new_file.writelines(reversed(content_list))
```

In this code, we are performing the same action as above. However, instead of iterating using a for loop and writing the list that ultimately is a sequence, we are writing using writelines() function.

## 6. More Examples
    

1.  ### Appending
    

Now that we have a good idea of reading from and writing to text files, we will look at how we can append texts to an existing file.

```python
with open('mytextfile.txt', 'r') as my_file:
	content_list = my_file.readlines()

with open('mytextfile_reversed.txt', 'a') as my_new_file:
	my_new_file.writelines(reversed(content_list))
```

Let’s run the same code as above but only change the parameter we are passing from 'w' to ‘a’ that stands for append. We are ultimately expecting this instruction to append the reversed list from our original file again to this mytextfile_reverse.txt to the end.

If we execute the above and open the file, we will find that its content has been changed to the following.

```
My old friend
Good to see you
How you been
Hello World
My old friend
Good to see you
How you been
Hello World
```

2.  ### Opening Two Files Simultaneously
    

It would not be surprising if you ever wondered how we can work with two (or more) files at the same time. Let's say we are to read content from one file and write to the other file in one go. Let’s try to do that.

We will go ahead and create two files as follows.

``new_text_1.txt``
``new_text_2.txt``

We will add content as ``I am file 1`` and ``I am file 2`` respectively.

Let’s write the code now.

```python
with open('new_text_1.txt', 'r') as my_file_1, open('new_text_2.txt', 'a') as my_file_2:
	content_1 = my_file_1.readlines()
	my_file_2.writelines(content_1)
```

If we read the new_text_2.txt, we will read its content as follows.

```
I am file 2
I am file 1
```
Therefore, we can say that we have successfully read the content from one file and appended it to the other simultaneously.

3.  ### Reading an Image
    

Before we do this, find an image (In this, we are opening a png image), and save it in the working directory. Then go ahead and open it as follows. Make sure to change the file name to the name of your image.

```python
with open('my_image.png', 'rb') as my_file:
	print(my_file.readline())
	print(my_file.readline())
```

This will output

```
b'\x89PNG\r\n'
b'\x1a\n'
```

If you want to see how the file looks in binary, go ahead and print the whole while using read() method. This can be useful when we want to read files and prepare them to be emailed or to change its metadata.

  

## 7. Conclusion
    

In today’s tutorial, we learned about how to handle files using Python. We opened and closed files while reading from and writing content to them. We learned a lot about files, file types, character encoding, and other related aspects to manipulating files using Python. If you want to learn more about file handling using Python, feel free to go ahead and read the [official documentation](https://docs.python.org/3/tutorial/inputoutput.html) as you may find lots of resources that might be useful to you as a Python developer.

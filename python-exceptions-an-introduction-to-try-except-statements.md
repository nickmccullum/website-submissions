# Python Exceptions: An Introduction to Try Except Statements

  

## Introduction

There are many errors associated with computer programs. These are mainly compiler errors and runtime errors. As the names suggest, compile errors occur at the compile-time and runtime errors occur while the program is running. Although the former can be identified, generally, runtime errors can only be found when the program throws an exception and crashes. However, if the programs are to run smoothly without any interruptions to its flow, there should be a mechanism to address this.

For instance, let us take a look at the following code.

    my_list = [0, 1, 2, 3]
    
    print(my_list[5])

  

If we try to execute this code, since we are trying to access an index that is out of the my_list’s range, it will throw the following error.

    IndexError: list index out of range

  

Had this piece of code been in a bigger program, once it  reaches this point, it would throw this error and terminate the execution. If this had happened in a packaged program already running in an end user’s device, it would be a disaster as the program would crash every time it would run into an error.

This is where exception handling comes in. It is an essential tool or a mechanism in programming languages to deal with runtime errors and refrain the execution of the program from being terminated.

Let us add a few lines and modify the above code slightly.

    my_list = [0, 1, 2, 3]
    
    try:
    
      print(my_list[5])
    
    except:
    
      print(100)

  

This program would give 100 as its output. If we take a look at the code, we can see that the original print statement is placed in a try block. There is also an except block added with a print statement. In simple terms, this means try to print the 5th index of myList, and if it does not succeed, print 100 instead. However, you should note that we have not specified what types of errors should be caught.

In Python, the try block is always followed by at least one except statement. With multiple except statements, we can define what errors to be caught or not. This helps the computer to execute the program handling different exceptions in different ways.

In Python language, the most popular and widespread class of exception handling is the Exception class. Python developers can also have user-defined exceptions; this Exception class is usually the user-defined exception classes are derived from. However, the Exception class has a parent class and sibling classes. Let us look at the Python exception hierarchy in the next section.

  

## Python Exception Hierarchy

The hierarchy of Python exception classes has been established on the BaseException class. Therefore, all the exception instances or objects are always derived from this BaseException class or its child classes. BaseException has four immediate child classes; SystemExit, GeneratorExit, KeyboardInterrupt, and Exception.

  
  

## Catching Exceptions

As mentioned earlier, the procedure to deal with exceptions is to catch them and decide what to do afterward. If the program might potentially throw many types of errors, they can either be addressed as a whole or even individually. The following is a general guide with examples on how to deal with the exceptions.

### Catch All
    

Use the following if the program is simple, and you need to catch all the exceptions and handle them the same way.

    try:
    
       # An instruction that might likely
    
       # throw an exception
    
    except:
    
       # What to do about it

  
  
  
  

 ### Avoid Masking Special Exceptions
    

This way, special exceptions are not masked. For instance, sibling exception classes of the Exception class will not be caught here.

    try:
       # An instruction that might likely
       # throw an exception but preferably
       # not a from a sibling class of Exception
    except  Exception:
       # What to do about it

  

### Catching Exceptions Explicitly
    

In this scenario, multiple except statements can be maintained to catch different exceptions and handle them individually. The syntax is,

    except  YourErrorHere:

  

The following is the code snippet with the try statement.

    try:
       # An instruction that might likely
       # throw an exception
    except  BufferError  as e:
       # What to do about the caught BufferError
    except  ArithmeticError  as e:
       # What to do about the caught ArithmeticError

## Raising Exceptions

Python offers lots of flexibility with exceptions. The developers can even instruct the program to raise built-in exceptions in addition to the user-defined ones. This comes handy in performing unit testing with exception handlers and extreme conditions in the program.

Users can also raise warning messages in addition to exceptions. These are useful in informing or altering the users about the program in scenarios such as the use of outdated modules, reaching allowed memory limits. One can issue warnings after importing the Python warnings module.

However, it is the sole responsibility of the user as there is no mechanism to regulate what exceptions or warnings can or cannot be raised by the user.

Consider the following code.

    my_list = [0, 1, 2, 3]
    
    my_list_index = 5
    
    if(my_list_index>len(my_list)):
    
       raise  Exception("Index is out of range. Use a value less than 4")

  

The above code would produce the following output.

    Exception: Index is out of range. Use a value less than 4

  

This raise statement gives developers the ability to force exceptions at different points of their code and must be fulfilled with an instance of BaseException, or one of the derived classes.

## User-Defined Exceptions

Python enables developers to define their exception classes. They are usually derived from the Exception class. They would behave in the same way as the other classes do.

As a rule of thumb, they are kept as simple as possible with just enough attributes to identify the potential error to be caught. Moreover, a main base class is created, extending the Exception class, and other subclasses are derived from that user-defined base class depending on the error conditions.

Consider the following code.

    class  MyBaseErrorClass(Exception):
       # This is the user-defined base class
       pass
       
    class  MyErrorOne(MyBaseErrorClass):
       # This is a user-defined child class
       # derived from the user-defined base class
    
       def  __init__(self, my_value):
          self.my_value = my_value
    
       def  __str__(self):
          return(repr(self.my_value))
    
    class  MyErrorTwo(MyBaseErrorClass):
       def  __init__(self, my_value, my_user_name):
          self.my_value = my_value
          self.my_user_name = my_user_name
    
    def  __str__(self):
       return('user ' + self.my_user_name + ' entered ' + str(self.my_value))

  

We can test what happens if the error gets caught as follows.

    raise(MyErrorTwo(2,'David'))

  

The above would produce the following result.

    MyErrorTwo: user David entered 2

  
  
  

## Exception Wrapping

In exception wrapping, wrapper classes are written for exceptions to encapsulate one into another. This comes in handy when there are collaborative implementations of libraries.

For instance, consider a scenario in which a file reader library internally uses another 3rd party library called SomeLib to acquire files from Google Drive. In case if the expected file is missing from Google Drive, let’s assume that it throws somelib.exceptions.wronglink error. However, since the user does not know this, there could be issues if exceptions are thrown by the internal library. You can address this issue by wrapping the exception. 

Check the following code for an example implementation.

    class  MyFileReaderLib(Exception):
       def  __init__(self, msg, somelib_exception):
          super(MyFileReaderLib, self).__init__(msg + (": %s" % somelib_exception)) 
          self.somelib_exception = somelib_exception
    
       def getFileOnline:
          try:
             return somelib.getfile('drive.google.com/u/2akjhaADS')
          except somelib.exceptions.wronglink as exep:
             raise MyFileReaderLib('Link is wrong or file not found', exep)

  
  

  
  

## Exception Logging

Logging exceptions is just as notable as catching exceptions. A message or any other relevant information should be logged for future reference. You can use the logging library to accomplish this. 

The following is one of the most straightforward implementations of logging.

    import logging
    
    try:  
       # some instruction that will raise an error
    
    except  Exception  as e:
       logging.exception("message")

  

The instruction inside the except statement will produce a stack trace with the message. Note that logging.exception should only be used inside the except block. If it is used elsewhere, it might produce unexpected results.

  

## Conclusion

Exceptions handling is used in programs to ensure that the flow of execution is not interrupted with any raised errors. They can be considered to be essential components of the program workflow itself. In the event any errors are raised, the program will follow the instructions defined in the except statements.

Adding an else statement to try-except statements would add the functionality of signaling the program that no errors were raised. Consider the following code.

    my_list = [0, 1, 2, 3]
    
    try: 
       print(my_list[3])
    except:
       print(100) 
    else:
       print('No errors')
    
      
    
The above will produce the following result.
    
    3
    
    No errors

  

Note that by adding a final statement to the try-except block, the program can perform a final task after executing the tasks inside the except block.

    my_list = [0, 1, 2, 3]
    
    try:
       print(my_list[5])
    except:
       print(100)
    else: 
       print('No errors')
    finally:
       print('Just exiting try-block')
    
The above code will produce the following result.
    
    100
    
    Just exiting try-block.

  

So, there it is. That is how to perform exception handling in Python.

Have a good day!







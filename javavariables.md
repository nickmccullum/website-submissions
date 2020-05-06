## All You Need to Know About Java Variables
 
Java is a robust language and is used to build many programs. Variables can be considered as building blocks of any language. Variables in Java have a huge role to play in making it a widely accepted language. A variable can be defined as a name given to a certain memory location, which is a basic unit in a program. All languages use variables to store data and the value of a variable can be changed during the execution of a program. Any operation done on the variable will affect the memory location.
## Java Variables
In Java, the variables are declared before use. I will discuss more in the next section. A variable contains a data value and thus, it has a data type. It can be anything ranging from texts to codes to numbers.
Despite Java being object-oriented, not all variable types are objects. It is built on basic variable types called primitives which include the following:
byte (number, 1 byte)
short (number, 2 bytes)
int (number, 4 bytes)
long (number, 8 bytes)
float (float number, 4 bytes)
double (float number, 8 bytes)
char (a character, 2 bytes)
boolean (true or false, 1 byte)

## Declaring and Initializing Java Variables
Java is a strong-typed language and therefore, variables have to be defined before they are used. Here is how to declare and initialize different variables.
### Number

```java
int myNum;
```
To initialize myNum, you can use following two methods:

```java
int myNum;
myNum = 40;
```

Or

```java
int myNum = 5;  // declaring and initializing the variable together
```

To declare and initialize double floating-point number:

```java
Double d = 4.5;
d = 3.0;
```

To use float, you need to cast:

```java
float f = (float) 4.5;
```

Or you can do it as follows (a shorter way of casting):

```java
float f = 4.5f;
```

### Character and Strings
It is not common to put an ASCII value in a character and it has special syntax as follows:

```java
Char c = ‘g’;
```

String has special treatment in Java. Here are some ways of using it:

```java
String s = new String (“This is a string created using constructor”);
String s1 = “This is a string created without a constructor”;
String sAdd = s + s1;
```

Operator overloading is supported only in String class in Java. + operator is used to concat two strings.

```java
int myNum = 7;
String s = “I have “ + myNum + “pens”;
```
 
### Boolean

It accepts only true and false as values. 

```java
public class Program {
    public static void main(String[] args) {

        // Test true and false booleans.
        boolean value = true;
        if (value) {
            System.out.println("A");
        }
        value = false;
        if (!value) {
            System.out.println("B");
        }
    }
}
```

Output

```
A
B
```

## Type of Variables in Java
#### 1. Local Variables
A variable that is defined within a block or a method is called a local variable. Their scope is, therefore, limited to the block or method in which they are declared and can only be accessed within it. Initializing these variables is mandatory.

```java
public class StudentData {
public void StuAge()
{
    	// local variable age
    	int age = 0;
    age = age + 5;
    	System.out.println("The age of the student is : " + age);
}
 	public static void main(String args[])
{
    	StudentData obj = new StudentData();
    	obj.StuAge();
}
}
```

Output:

```
The age of the student is : 5
```

#### 2. Static Variables

Static Variables are also referred to as Class Variables. They are declared using static keyword within a class outside a block, or a method constructor. There is only one copy of a static variable per class irrespective of the number of objects we create. Static variables are created when the program execution begins and are destroyed when execution ends. Initialization is not mandatory in static variables as they have a default value of 0. Accessing static variables through an object will not halt the program, instead, the compiler will replace the object name to the class name automatically.

```java
import java.io.*;
class Employee {
 
	// static variable salary
	public static double salary;
	public static String name = "Nick";
}
 
public class EmpDemo {
	public static void main(String args[])
	{
 
    	// accessing static variable without object
    	Emp.salary = 10,000;
   	 System.out.println(Emp.name + "'s average salary is:"
                       	+ Emp.salary);
	}
}
```

Output
```
Nick’s average salary is: 10,000
```
#### 3. Instance Variables
Also known as non-static variables, instance variables are declared in a class outside any method, block, or constructor. These are created when an object of a class is created and get destroyed along with it. Access specifiers may be used for instance variables. Initialization is not mandatory, and the default value is set to 0. They can be accessed only by creating objects.

```java
import java.io.*;
class Marks {
	// These variables are instance variables.
	// These variables are in a class
	// and are not inside any function
	int engMarks;
	int sciMarks;
	int comMarks;
}
 
class MarksDemo {
	public static void main(String args[])
	{
    	// first object
    	Marks obj1 = new Marks();
    	obj1.engMarks = 90;
            obj1.sciMarks = 85;
    	obj1.comMarks = 80;
 
    	// second object
    	Marks obj2 = new Marks();
    	obj2.engMarks = 70;
    	obj2.sciMarks = 75;
    	obj2.comMarks = 85;
 
    	// displaying marks for the first object
    	System.out.println("Marks for the first object:");
    	System.out.println(obj1.engMarks);
    	System.out.println(obj1.sciMarks);
    	System.out.println(obj1.comMarks);
 
    	// displaying marks for the second object
    	System.out.println("Marks for the second object:");
    	System.out.println(obj2.engMarks);
    	System.out.println(obj2.sciMarks);
    	System.out.println(obj2.comMarks);
	}
}
```

The output will be:

```
Marks for the first object:
90
85
80
Marks for the second object:
70
75
85
```
#### 4. Parameters
A parameter can be defined as a variable that is passed to a method when the method is called. They are only accessible inside the method where they are declared and a value is assigned to them when it is called.

## Java Variables Naming Conventions
While naming the variables in Java, there are certain rules to be followed to keep the code easy to understand and error-free. Below are the conventions that are followed by the programmers while naming the variable.

1. Variables in Java are case sensitive. This is to say that student, Student, and STUDENT are three different variables.
2. The name of the variable must start with a letter, an underscore (_), or the $.
3. After the first character, the variable can also contain numbers (a variable cannot start with the number).
4. The reserved keywords in Java can not be used as variable names. This includes the keywords like int, char, Boolean, and more that have a specific meaning in the Java code.
Take a look at some valid Java variable names:
```java
myint
myInt
MYINT
_myInt
$myInt
myInt1
myInt_1
```

There are some other rules that are generally popular in programmers. That means these conventions are to make the code more readable although if ignored these will not cause any error. Java developers follow these conventions so that they can understand the code and to make it easier for other developers to follow it who have not contributed to writing it. These are:
1. The names of variables are written in lowercase. For example, student, emp, etc.
2. If there are multiple words in the name of the variable, the first letter after each word is written in uppercase. For instance, studentMarks, empSalary, etc.
3. Even though the code allows it, the name never starts with a $ or a _.
4. The static final fields (constants) are named in all uppercase and for a multiple word variable, they are separated by an underscore. For example, EXCHANGE_RATE.

## Java Local-Variable Type Inference

Since Java 10, it is now possible for the compiler to infer the type of a local variable by looking at what actual type that is assigned to the variable at the time of declaration. The enhancement is specific to the local variables, indexes in for-each loops, and local variables declared in for-loops.
Before Java 10, it worked as follows:

```java
String myVar = "An example of a string!";
```
However, from Java 10, you need not specify the type of variable during declaration if it can be inferred from the value assigned to it. Here is how it works.

```java
var myVar = "An example of a string!";
```

The keyword var is used before the variable name here instead of String. The value assigned to the variable tells the compiler about the type of the variable and therefore, it needs not to be written explicitly in the code. Look at more examples below:

```java
var list = new ArrayList();
var myNum = new Integer(123);
var myClassObj = new MyClass();
```

## The Bottom Line
Variables form the basic blocks on which a language is built. Choosing variables and their names can decide a lot when it comes to the functionality of your code. The names must be chosen carefully so that they do not compromise the quality of the code. At the same time, it must be such that if the code has to be developed by multiple developers, they should find it easy to grasp the code.


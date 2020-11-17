# The Complete Guide to Python f-Strings

Python f-Strings are an improved method for formatting strings in python. It was introduced in Python 3.6 as a concise, faster, more readable and less error-prone method of formatting strings. F-Strings are formatted string literals that allows variables, functions and expressions to be embedded in a string. Following is the basic format of a python f-string.

```python
variable = "World"  
print(f"Hello {variable}, This is a f-String")
```

RESULT
![](https://lh5.googleusercontent.com/jqyMqcXWVNdL7drX-pw_fXtROyFqWxm-RBuTvzTtViGxCUxvXlR9JginRQuI7FnOK_EP9QzZdKEErzy0ry9CSyXCH-cDf5xIAL12tIQjA2z-yzCFtsp0RuiHt_e0RwqHNgMK7j2p)

# Alternative Methods of String Formatting

Before the introduction of f-Strings, the main methods of string formatting were percentage formatting (%) and the str.format() method. Let's look into each of these methods.

## Percentage Formatting (%)
This is the original method of string formatting which was available in the python language from the inception. In this method, we use “%s” as a placeholder in a string. Then add the variables at the end of the string with a percentage sign (%). You have to use brackets for  for multi variables. See the below example.

### Single Variable

```python
name = "Barry"  
string = "My name is %s." % name  
print(string)
```
RESULT
![](https://lh5.googleusercontent.com/LwIUPPdiMV_EUJbBHMD0Vl0Lw6szF6tNBxiVH_Bo-c9sWVykc9EYnl7OuUiHnInNE63KKKYxzWyIjVLluVIND4wmDjk661MWlN-aku5dG2mekrryDmCD-xn0k3earH1hUVqYmU3D)

### Multi-Variable

```python
name = "Barry"  
age = 18  
string = "My name is %s. I am %s years old." % (name, age)  
print(string)
```
  
RESULT
![](https://lh4.googleusercontent.com/ko4lincdGLUlOGHvsGnUFkfvuHSI6r3yUUNFbgJqsj1ZTXLTa9OE7aRLH9DvzGq4gAIcMmPpZbVxok_X-_wb_AXl5rYDkyc4-HSDdfueCVYUECOR25mZNjsgQpCcs08qp-t-8vMp)

The main disadvantage of this type of formatting is that it gets complicated as he number of variables increase. It can make the code less readable and easily prone to errors, such as iterables like dictionaries and tuples not displaying correctly. The official Python 3 docs do not recommend this type of formatting, providing the following warning.

“The formatting operations described here exhibit a variety of quirks that lead to a number of common errors (such as failing to display tuples and dictionaries correctly).

Using the newer formatted string literals or the str.format() interface helps avoid these errors. These alternatives also provide more powerful, flexible and extensible approaches to formatting text.”


## str.format()
This style of formatting removes the usage of the percentage (%s) operator. This makes the syntax simpler and more readable. Formatting is now handled by .format() on a string object.

In str.format() method we can use named indexed {name}, numbered indexes {0} or implicit indexes as place holders in a string. Then call the .format() with the variables inside the brackets. See the below examples

```python
name_value = "Barry"  
age_value = 18  
namedindex_string = "My Name is {name}, I am {age} years old.".format(name = name_value, age = age_value)  
numberedindex_string = "My Name is {0}, I am {1} years old.".format(name_value, age_value)  
implicitindex_string = "My Name is {}, I am {} years old.".format(name_value, age_value)  

# Printing the formatted strings  
print(namedindex_string)  
print(numberedindex_string)  
print(implicitindex_string)
```
RESULT
![](https://lh6.googleusercontent.com/wtN0wb2XwqZw5wV_4ee8enAWAbA5l4NaL4H2OsYZbWw6U78-oPIBe2g-wy4XWQQxQEhfOKLRusb9RDIV25oyDscBNU6ValFtnuuyURh01btgXyCLqRGhe36qiF9MLz6BWQ-55kc6)

You can see that `str.format()` is much more simple and functional method than percentage formatting (%). However, this method is still not suited for handling large sets of variables, as the code structure can get verbose quite easily. To mitigate these issues, and as a powerful method of formatting, python f-Strings were introduced.


# Basics of f-Strings

f-Strings are also known as “formatted string literals” is a way in which we can use embedded python expressions inside string constraints. Formatted string literals are declared using “f” at the beginning with curly braces containing expressions that will be replaced with their values. f-Strings can be declared with either a lowercase “f” or an uppercase “F”. These expressions are evaluated at the runtime and formatted using the __format__ protocol.

```python
name = "Barry"  
  
# Lowercase f-String declaration  
string_one = f"Hello World, I am {name}"  
  
# Uppercase f-String declaration  
string_two = F"Hello World, I am {name}"  
  
print(string_one)  
print(string_two)
```
  
RESULT
![](https://lh5.googleusercontent.com/QWWf5YuVTRI-qAtafZqrZRWjlzYvvbQdo0I3ssahts6DMa9FCx2uyoowiP134IuTX4qTO8TNWovd_ig2PZfShkzQ7gbZ4sVHdtr-fkIdSqI8qCJQmnbX4S5XxqjvlFM7YE8ZU5yH)

As you can see f-Strings will make the code more readable while providing powerful functionality. f-String can be used with inline arithmetic operators, iterables, objects, functions etc..

# Arbitrary Expressions in f-Strings

As f-Strings are evaluated at runtime, we can use any valid python arbitrary expressions with it. f-Strings can run these expressions faster than any previous method of formatting. This is possible because expressions are evaluated at runtime and all the expressions inside the curly braces are evaluated in their scope then combined with the string literal of the f-String. Following sections will demonstrate how expressions are processed.

## Arithmetic Operators

### f-Strings with variables

```python
price = 10  
no_of_apples = 5  
string = f"Price of {no_of_apples} apples is {int(price * no_of_apples)}"  
print(string)
```
  
RESULT
![](https://lh4.googleusercontent.com/NA9bf4BpogHzOeZprJYL4wTGUo80BKQMSO3clf4gmFbo74qDDye1kZB21ECIVgCujCGQzez1eve6z8HKNnwY9IQwR7FeHKd4QoQ6menVCUfeyqVdbFww2RbAX3L9Eatdwk_3-4ak)

  
### Inline arithmetic operations
```python
string = f"Price of 5 apples is {5 * 10}"  
print(string)
```
  
RESULT
![](https://lh6.googleusercontent.com/CpAbmW919s2QZHEuWVFFYhxDc0k861kap6QsS7fUBDDeX9lOKvyRAU5-dN4j2C12zrH4IKFzHerDKsK8sI-0azj-5rpGFiVRxstmNFGDVk1U3NuXuiIYELwxDF4KpUdL_jc8tteX)

  
## Functions in f-Strings
```python
# Convert Given String to Hexadecimal  
def  convert_to_hex(value):  
    value_binary = value.encode(encoding='utf_8')  
    hex_value = value_binary.hex()  
    return hex_value  
  
name = "Barry"  
string = f"Hexadecimal value of Barry string is {convert_to_hex(name)}"  
print(string)  
  
# Convert Given Hexadecimal to String  
def  convert_to_string(value):  
    hex_value = bytes.fromhex(value)  
    string_value = hex_value.decode(encoding='utf_8')  
    return string_value  
  
hex_value = "4261727279"  
string = f"String value of 4261727279 hexadecimal is {convert_to_string(hex_value)}"  
print(string)
```
  
RESULT
![](https://lh6.googleusercontent.com/Uh2MN1VVKWDS-l4PdYonZtfO5-n471F1tExgpmm-lGRViYd5lRxIqNzi41evd-JTNdCgp4aC7pownhmfgS_PNeQ4r4IBPz5H7MeopbmrY0OLYft6p-iheEHAYFcyuGwq55Huk49X)

In the above example, we call the functions “convert_to_hex” and “convert_to_string” from the f-string to convert the given values to hex and then back to string format.

## Calling Objects created from Classes
```python
class  PersonalDetails:  
  
    def  find_gender(self):  
        if self.gender == "M":  
            pronoun = "he"  
        elif self.gender == "F":  
            pronoun = "she"  
        return pronoun  
      
    def  __init__(self, first_name, last_name, age, gender):  
        self.first_name = first_name  
        self.last_name = last_name  
        self.age = age  
        self.gender = gender  
      
    def  __str__(self):  
        return  f"{self.first_name} {self.last_name} is {self.age} years old."  
      
    def  __repr__(self):  
        return  f"{self.first_name} {self.last_name} is eligible for a driving licence as {self.find_gender()} is {self.age}"  
  
new_licence = PersonalDetails("Barry", "Stevens", "18","M")  
  
# Get String Representation  
print(f"{new_licence}")  
  
# Get Object Representation  
print(f"{new_licence!r}")
```

RESULT
![](https://lh3.googleusercontent.com/0yqS6otRY4Z1vVCpK5UKLx_Qg2-mRg3QJUCL4KskL0LhbA04evku5HaarbGywFRp-3WzrH6x71mY4xBS3rxxaMsAF2d4c8z6m4QztOwHYGUBR31CdJmrDaiBR_e4J2fAqlmgIXZj)

Using the __str__() and __repr__() methods, we make the Class “PersonalDetails”. A new instance of the class is created called new_licence and is used in f-Strings to call each function within the class. The __str__() function is the informal string representation of the object, while __repr__() function is the official representation of the object. By default, f-Strings identifies the __str__() function, because of this we have to explicitly call the __repr__() using the shorthand ‘!r’

  
## Multiline f-Strings
When defining multi-line f-Strings, each line must start with the `f` otherwise it will not be recognized as an f-String and will not have the necessary formatting to obtain a single line or multi-line output.

#### Multiline f-String with a single line output
```python
# Single Line Output

name = "Barry"  
email = "barry@gmail.com"  
addr = "56, Beach Road, Seattle"  
  
string = (  
    f"My name is {name}. "  
    f"My email is {email}. "  
    f"I live in {addr}."  
)  
  
print(string)
```
  
RESULT
![](https://lh6.googleusercontent.com/yFwQ9hqH6zcAYf20GpSipFPDI6VVZPE1Yr_Km1JPJSE7VvDXThChnOqHyABRsNLQlPno1GqHyLpSyC3QKp4ldqHDmNnaLnVPcG2FsYXr9Ix8bSxMWcW0L55I_R26gas1hRQjGMHX)

### Multiline f-String with a multiline output

```python
# Multi Line Output  
name = "Barry"  
email = "barry@gmail.com"  
addr = "56, Beach Road, Seattle"  
  
string = (  
    f"My name is {name}. \n"  
    f"My email is {email}. \n"  
    f"I live in {addr}."  
)  
  
print(string)
```
  
RESULT
![](https://lh4.googleusercontent.com/4E0_qsLyYTQNoFJGwixeZ-3IXF-lnNs0aWh2-EB1bNHe8XKDXIbcxx_1Go3ow3suphfg9mO98TawOJQ1bovmqb7k8zbiaMFcNxdQBbb6ceAp0vTzgreWD1OJ2wibmMeGNwxO1SSE)

# Special Characters in f-Strings
In this section, we will learn how to use special characters within f-Strings.

## Quotation Marks
Any type of quotation mark can be used when defining an f-String. The only limitation is that you need to add a different quotation mark inside the string opposed to what is defined outside. Otherwise, this will cause a Syntax error.
  
```python
f"{'Barry'}"
```
  
RESULT
![](https://lh3.googleusercontent.com/YY451OzEESIbyFRCOTcscTETiCiQU2U4L46XmAGcVPeLEt6bquxSC-gzr03nisDh_ONpSKNR00Iq97_fcZKi6z5tnI-10z4gMYxvnt2A7wKy1wr0wzs4FOewKad9GveZOrcM_HV0)

```python
f"{"Barry"}"
```
  
RESULT
![](https://lh5.googleusercontent.com/MwT8ugPLax9zsUyoipv0fK-71ht3Wh_0pAI1jvuGfVEu7VIpcd9c72A7A0aEVzBXNbnYPFoEgt1ZxfN6uHQZXsIQiNf9ZpgAAbMdKevLo5DG0zjXrOvp63xufSoL6uLinnMbVeDP)

To use the same quotation mark in all instances of the string, we can use “\” as an escape character
```python
name = "Barry"  
  
#Single quotations  
print(f"Hello, \'{name}\'")  
  
# Double quotations  
print(f"Hello, \"{name}\"")
```
  
RESULT
![](https://lh6.googleusercontent.com/PxuQB9icEZmtO2QThE0FGcmmTK62Wet8Yyg_2NlZ554LaLbswKO7bKvt2yVSIrH_Su6t52g6bYbtw9Pb9ZWzOo53LDo6yDk6d5A-ZOuyKVISND_XxxiFbTZEAPu5fR5SR0laTDa2)

### Other types of quotation marks

```python
# Single Quote  
f'{"Hello, Barry"}'  
f"{'Hello, Barry'}"  
  
# Triple Quotes  
f"""Hello, Barry"""  
f'''Hello, Barry'''
```
  
RESULT
![](https://lh3.googleusercontent.com/VZQxGBek3FHKpOMeWhqCGQrXa7p3KxJ7GBrUKZ4OSbpm4E3ea9C4R9N_jqtC-03xCiUK01gkZXwga3Duz_EdbcCYqlweGtenH5-ezudeVBlKVVTXaOVqAbOrTwRi9mOmVV5k9JxS)

## Braces
To use braces in an f-string, simply add a double set of braces. If triple braces are used it will result in only displaying a single set of braces. To overcome this limitation we can add additional braces so f-String will recognize each additional set of braces. Please refer to the following examples.

```python
value = 50  
# Double Braces  
print(f"The value of the variable is {{50}}")  
  
# Triple Braces  
print(f"The value of the variable is {{{50}}}")  
  
# Multiple Braces  
print(f"The value of the variable is {{{{50}}}}")
```
  
RESULT
![](https://lh3.googleusercontent.com/_bIbiJ07Ytsu2qJztwFC7dIC2bXRaHoZmg72w2kFaFvcj0Yo65UnX4tvp-IqgByt9V22qIjlIUjY4JLoc2lAgXyRf6j0xYIgz5QGzT7YB7ex4jWq71AeKBXByCInmTuWHi2hBpIi)

## Backslashes
Backslashes can be used in the string part of the f-String. However, backslashes can not be used inside the expression. This will result in a Syntax error.

### Correct Use of backslashes
```python
# Using Backslashes  
file_name = "info.txt"  
string = f"File Location is C:\Data\{file_name}"  
print(string)
```
  
RESULT
![](https://lh6.googleusercontent.com/hPPSCXeUUF1zK7CSILNdkW06lLuRQqu5mQDLcOY6ulfzwMG1MAOlfnLT3khMoeWvVjq0JRCDmJ_9JouJ12gi7WG1P0lJMJ_qkqEXQUULEqHcqkWE7Z9JfXDGZwDWs8aPJ-_lu6up)

### Incorrect use of backslashes

```python
# Using Backslashes  
file_name = "info.txt"  
string = f"File Location is C:\Data{\file_name}"  
print(string)
```
  
RESULT
![](https://lh6.googleusercontent.com/sQ4r9KDCbkK12NQLEIBoT8R5tuxCdaWEAeHnA50yQlDzdg9CRg786__ARftt3mvqr34aaxHhqcnv21qlzbN0Sw6doKXfY55UaXUs0xHGT6mDD8Ns1urwTipboSYaed_orIqnxgb2)

You can see, as the backslash is used inside the expression, f-String can not identify the variable. This results in a Syntax error.

## Comments
When dealing with comments, the same rules of backslashes are used. Comments or the hashtag (#) can be only added in the string portion of an f-String. If they are added to the expression of an f-String, this will also result in a Syntax error. Below examples will demonstrate adding comments in f-Strings.

### Correct use of comments (#)

```python
# Using Comments (#)  
name = "Barry"  
user_id = 7851  
string = f"User {name}'s user ID is #{user_id}"  
print(string)
```
 
RESULT
![](https://lh6.googleusercontent.com/Ah4Sy9lgKZhITzQ4pZ84Gcc2mYx9q-T04bko0DKh2f39ig0U6zF4ECBTnAK2CXrpOHiILflOhJQ13oYv0lmqmKs8AN1-P7dZOzBuWuFYohnqceWIjiDIOrMlCT_pOgli0FDyeGSo)

 
### Incorrect use of comments(#)
```python
# Using Comments (#)  
name = "Barry"  
user_id = 7851  
string = f"User {name}'s user ID is {#user_id}"  
print(string)
```
  
RESULT
![](https://lh6.googleusercontent.com/bIq6oYIZcy-Nav-rbmja2ZZS2tWeSSaTDgJjKbNTQTWBks_nJ8GyEdIkv2PK3oxi-oIALAyokgYXO7ELxJYlZPOMYjFMZOxg7-RkVfEc6PNKaIDX8xSC1iei_lIZ5dn8PfKGfl7e)

## Dictionaries
When referencing dictionaries in an f-String, the quotation marks referring to each key-value must be different from the f-String quotation mark. If we create an f-String with a double quotation (“”) marks, we must use the single quotation marks (‘’) to reference the key-value pair. Otherwise, this will also result in a Syntax error.

### Referencing dictionaries

```python
# Dictionary  
user_details = {'first_name' : 'Barry', 'last_name' : 'Stevens', 'age' : '18', 'email' : 'barry@gmail.com'}  
  
# Multiline f-String  
string = (  
f"== User Details == \n"  
f"Full Name : {user_details['first_name']} {user_details['last_name']} \n"  
f"Age : {user_details['age']} \n"  
f"Email : {user_details['email']}"  
)  
print(string)
```
  
RESULT
![](https://lh4.googleusercontent.com/oNE9sKl0znWsAN2DASSy35jCXPExb4IVjbcmXMwC-gw5QZw9rfmqjZTpkUqb0a5Ekqj6iTd7c9bVf-hsBCG8Z-GFyQv9rltovg1mw-Tk1DiFXSlvXRi8RDLb_-BD7vaDQZxSiefN)


In the above example, we identify each key in the dictionary with a single quotation mark and create a multiline f-String composting of all the user details. In the next example, we can identify the syntax error that will occur if we used the same quotation marks as the one used in the initial f-String declaration.

```python
#Dictionary  
user_details = {'username' : 'barry005', 'active_days' : '35'}  
  
# Incorrect f-String reference to the dictionary  
string = f"User {user_details["username"]} was active for {user_details['active_days']} days."  
print(string)
```
  
RESULT
![](https://lh3.googleusercontent.com/ok0REdtUUdWf86p3Neeph0AydDhL13gCWdwC7BsBtnJ0tfyMIUl8_bjvxbrd4GNEKQqRGxcvmts7Xt2BYu8Koobx-0wCXoPM4joPnQqdvSlOLJ3VqpsDLyDCC3qx1ZU5jqry8cmZ)

The syntax error occurs when we are referencing the username key in the dictionary. As we are calling the username key using the same type of quotation mark (double quotes), the f-String identification breaks causing the error. To mitigate this problem, simply reference the username key by using single quotations marks as shown below.

```python
#Dictionary  
user_details = {'username' : 'barry005', 'active_days' : '35'}  
  
# Incorrect f-String reference to the dictionary  
string = f"User {user_details['username']} was active for {user_details['active_days']} days."  
print(string)
```
 
RESULT
![](https://lh3.googleusercontent.com/2sIksvkw4EEQEnmEBuJkl5n4bNWTD5XStOuucj89r008_Hn7fQ5aU32AfXgRYYczhXRc8j46nHoC0AL2mcbKgIRJ9QyQYJp0_Vkm6wXDED0RbDgBag0nHOgBW_DAAq8gVP7k8Bau)

# Conclusion
f-Strings are a paradigm shift in how Python handles string formatting. It Allows users to create strings with expressions directly attached. While anyone can use percentage formatting (%) or str.format() depending on the situation, f-String offers numerous advantages over the those methods such as being more readable, faster handling of data, and more convenient ways to insert variables, functions, and objects to a string constraint.
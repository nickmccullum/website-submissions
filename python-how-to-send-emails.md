
# How to Send Emails with Python

Python is a highly versatile programming language. It consists of many standard libraries that enable many useful functionalities, sending emails is just one of them.

Although it may sound difficult, sending an email with a Python script is quite easy. It is time-saving in the long run and has lots of real-world applications. Whether you need to send bulk emails, send confirmation or verification codes to users, or even automate regular emailing tasks, all that is possible with Python scripts and we’ll be covering them in this article.

We will be using the SMTP (Simple Mail Transfer Protocol) to send emails.

  

## Prerequisites

Let’s get the prerequisites out of the way before we proceed any further. This is what you will need to have:

-  Python
    

I assume that you already have Python installed. If not, please install the latest stable version from [here](https://www.python.org/downloads/).

  

-   A Gmail account
    

It’s fine to use an existing Gmail account. However, in this tutorial, you will be changing a security setting. You will also be using your username and password in plain text. Therefore, it is recommended that you create a separate email account just for this purpose.

It is still possible to use your existing account without changing your security settings, but you will need to use the Gmail API. But that’s a topic for another day.

Irrespective of whether you create a new account or use an existing one, turn ON “Less secure app access”. Click [here](https://myaccount.google.com/lesssecureapps) to go to the relevant page on your Gmail account settings page. Ensure that you are logged in to the correct account if you are logged in to multiple accounts on the same browser.

-   Python Libraries
    

-   SSL Library
    

In this tutorial, we will be setting a secure SMTP connection. So we need the following SSL library. Open a shell or command prompt and install it using pip with the following command:

`pip install ssl`

  

-   smtplib (Part of the standard library)
    

SMTPLib is included as a part of the standard libraries of Python. So you won’t need to install it explicitly.

  

## Online and Offline Email Sending Options

You can test the code in this tutorial using both localhost and Gmail. This allows you to simulate the process as well as to send emails using a real account.

  

### Offline Option - Local SMTP server

Setting up a local SMTP server is a good way to test the functionality of your code. You can send emails and print their content to the shell.

Enter the following command to the terminal and start a local SMTP debugging server.

`python -m smtpd -c DebuggingServer -n localhost:1025`

  

However, if you need to use a port other than 1025, you will need administrator privileges.

The code in this tutorial is mainly targeted for real-world testing. If you wish to test using a local SMTP debugging server, the following will clear things up for you to adapt the other code to your requirement.

  
```python
import smtplib

smtp_server = 'localhost'

port = 1025

sender = 'from@someemail.com'

receiver = 'sendingto@somemail.com'

message = 'Hi. This is a test.'

with smtplib.SMTP(smtp_server, port) as server:

server.sendmail(sender, receiver, message)
```
  

This will simulate sending an email through your local server.

### Online Option - Generic email account (Gmail)

This is a great way to put your code to the test and see it through the email inbox. We will see an example of this in the next section.

  

## Secure SMTP Connection

In the previous section, we sent an email through a local SMTP server without proper security or encryption. However, when we send emails in the real-world, this is not advisable. We have to ensure that the SMTP connection is secure. There are two protocols to make an SMTP connection secure.

They are SSL (Secure Socket Layer) and TLS (Transport Layer Security). TLS is an improved version of SSL. Although SSL is somewhat older, it is still widely used.

There are also two ports (465, 587) that are being used to initiate the connection. If port 587 is used, an unencrypted connection is established, and later encrypted. The connection is initiated using `server = smtplib.SMTP` and later encrypted using `server.starttls`.

If port 465 is used, then SSL encryption is initiated prior to any communication. The SMTP connection is initiated using `server = smtplib.SMTP_SSL`

Despite the port used, Gmail will encrypt the connection using TLS. However, default and trusted CA certificates and their validation can be loaded by calling `.create_default_context()`and creating a secure SSL context.

  

## Sending Emails

### Plain Text Emails

We will be using port 465 in this guide. However, the code required for both ports is given below.

Let’s send an email with only a body and no subject. Be mindful to change the sender and receiver addresses, and password accordingly.

#### Port 465
    
```python
import smtplib, ssl  
smtp_server = 'smtp.gmail.com'  
port = 465  
sender = 'from@someemail.com'  
password = 'myPassword'  
receiver = 'sendingto@somemail.com'  
message = 'Hi. This is port 465.'  
  
context = ssl.create_default_context()  
with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:  
server.login(sender, password)  
server.sendmail(sender, receiver, message)
```
  
#### Port 587
    
```python
import smtplib, ssl  
smtp_server = 'smtp.gmail.com'  
port = 587  
sender = 'from@someemail.com'  
password = 'myPassword'  
receiver = 'sendingto@somemail.com'  
message = 'Hi. This is port 587.'  
context = ssl.create_default_context()  
  
try:  
server = smtplib.SMTP(smtp_server,port)  
server.starttls(context=context)  
  
server.login(sender, password)  
server.sendmail(sender, receiver, message)  
except Exception as exep:  
print(exep)  
finally:  
server.quit()
```
  

### Adding a Subject to the Email

We can add a subject by changing the message to have a ‘Subject:’ and having two newline characters. (\n).

Change the message variable, as shown below, and try resending the email. Please note the triple quotes instead of a single quote.
```
message = """Subject: Hi there

  
This message is sent from Python.""
```
  

If you want to use single quotes instead, use it as follows.

`message = 'Subject: Hi \n\n This message is sent from Python. '`

  

### Styling the Email

We sent emails with a subject and a simple body. This will not always be sufficient in the real world. You will also need to style your text, add hyperlinks and images. Let’s use the email package for this.

The code is rather long, so let’s go through it one step at a time.

Import the libraries and define the variables.
    
```python
import smtplib, ssl  
from email.mime.text import MIMEText  
from email.mime.multipart import MIMEMultipart  
smtp_server = 'smtp.gmail.com'  
  
port = 465  
sender = 'from@someemail.com'  
password = 'myPassword'  
receiver = 'sendingto@somemail.com'
```
  

2.  Define a MIMEMultipart object. We will later convert this into a string and send this as the message.
    

```python
message = MIMEMultipart('alternative')  
message['Subject'] = 'MIME Test'  
message['From'] = sender  
message['To'] = receiver
```

3.  Create plain text and HTML versions of the email you want to send.
    
```python
email_plain = """\  
Hey there,  
Take care  
Bye!"""

  
email_html = """\  
<html>  
<body>  
<p>Hey there,<br>Take care<br>Bye!</p>  
</body>  
</html>  
"""
```
  

4.  Turn them into MIMETEXT objects and attach them to the message.
    
```python
mimetext_plain = MIMEText(email_plain, "plain")  
mimetext_html = MIMEText(email_html, "html")  
message.attach(mimetext_plain)  
message.attach(mimetext_html)
```
  

5.  Send out the email.
    
```python
context = ssl.create_default_context()  
  
with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:  
server.login(sender, password)  
server.sendmail(sender, receiver, message.as_string())
```
  

This gets the work done. However, it requires us to write lots of boilerplate code. We can greatly reduce the number of lines required to send an email if we use the 'Email To’ library. It simplifies the entire process of combining smtplib and MIMEText into one library.

Let’s try that approach as well. Install the ‘Email To’ library using the following command:

`pip install email-to`

  

The code will be as follows:

```python
import email_to  
smtp_server = 'smtp.gmail.com'  
port = 587  
sender = 'from@someemail.com'  
password = 'myPassword'  
receiver = 'sendingto@somemail.com'  
server = email_to.EmailServer(smtp_server, port, sender, password)  
server.quick_email(receiver, 'Testing New Library',  
['# My Title', 'My description'],  
style='h1 {color: red}')
```

  

Notice the port number 587 instead of 465. This is what is used by the email_to library by default.

This library also supports building the body of your email line by line.

```python
import email_to

smtp_server = 'smtp.gmail.com'

port = 587

sender = 'from@someemail.com'

password = 'myPassword'

receiver = 'sendingto@somemail.com'

server = email_to.EmailServer(smtp_server, port, sender, password)

message = server.message()

message.add('# Here is the shopping list')

message.add('- Milk')

message.add('- Espresso')

message.add('- Sugar')

message.style = 'h1 { color: red}'

message.send(receiver, 'My Shopping List')
```

  

Use the message.add() function to add lines to your email body.

  

### Adding Attachments to the Email

Sending attachments is an important part of sending emails. We need to encode the files to be sent via email, as we are working with a stream of textual data. The easiest way to do it is to use `encoders.encode_base64()`. We will be using an image in this tutorial. But you can even send PDF files. However, Gmail refuses some extensions like .exe.

1.  Let’s first build our code to the extent where we have the definitions and the email body with a simple message.
    

```python
import smtplib, ssl  
from email.mime.base import MIMEBase  
from email.mime.multipart import MIMEMultipart  
from email.mime.text import MIMEText  
from email import encoders  
smtp_server = 'smtp.gmail.com'  
port = 465  
sender = 'from@someemail.com'  
password = 'myPassword'  
receiver = 'sendingto@somemail.com'  
  
file_name = 'uploadThis.jpg'  
message = MIMEMultipart('alternative')  
message['Subject'] = 'Sending File'  
message['From'] = sender  
message['To'] = receiver  
message.attach(MIMEText('Sending an attachment', 'plain'))
```

  

2.  Now let's open the file, encode it, and add a header
    

```python
with open(file_name, 'rb') as attachment:  
file_part = MIMEBase('application', 'octet-stream')  
file_part.set_payload(attachment.read())  
  
encoders.encode_base64(file_part)  
file_part.add_header(  
'Content-Disposition',  
  
'attachment; filename='+ str(file_name)  
)
```

  

3.  Attach it to the message as follows:

`message.attach(file_part)`

  

4.  Now, send the email.
    

```python
context = ssl.create_default_context()  
with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:  
server.login(sender, password)  
server.sendmail(sender, receiver, message.as_string())
```

  

### Sending Multiple Emails

Sending multiple emails is another important requirement in the real world. If you know how to import a text file (preferably a CSV), loop through it and get the email addresses, you already know how to do this.

For this tutorial, we will send a simple email with a personalized greeting that says "Hi Name”.

Let’s do this step by step.

1.  Create a CSV file with emails and any other content you want to add to the email.
    

You can also use MS Excel or any other spreadsheet software to do this. Open your spreadsheet software, create a table with two columns 'Name’, and ‘Email' and save it as a CSV.

You can even use the same email address with multiple names if you don’t want to use other email addresses.

This is how it will look like in a text editor.

name,email

John,[john@example.com](mailto:johnsmith@example.com)

Sherlock,[sherlock@example.com](mailto:sherlock@example.com)

Dave,[dave@example.com](mailto:dave@example.com)

  

2.  Now let’s write all the common components of our code.
    

```python
import smtplib, ssl  
import csv  
smtp_server = 'smtp.gmail.com'  
port = 465  
sender = 'from@someemail.com'  
password = 'myPassword'  
  
context = ssl.create_default_context()
```

  
  
  
  
  

3.  Read and loop through the CSV and the personalized emails and access the rows
    

```python
with open('myemails.csv') as f:  
reader = csv.reader(f)  
next(reader)  
for row in reader:
```

  

4.  Send the email using the loop variables:
    

```python
with open('myemails.csv') as f:  
reader = csv.reader(f)  
next(reader)  
  
for row in reader:  
message = 'Hi ' + row[0]  
with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:  
server.login(sender, password)  
server.sendmail(sender, row[1], message)
```

  

5.  Full Code (Further optimized by reducing multiple logins)
    

```python
import smtplib, ssl  
import csv  
smtp_server = 'smtp.gmail.com'  
port = 465  
sender = 'from@someemail.com'  
password = 'myPassword'  
context = ssl.create_default_context()  
with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:  
with open('myemails.csv') as f:  
reader = csv.reader(f)  
next(reader)  
for row in reader:  
message = 'Hi ' + row[0]  
server.login(sender, password)  
server.sendmail(sender, row[1], message)
```

  
  

## Other Email Libraries

There are many other libraries that have made the email sending process much easier. You have already learned about one of them. The following are a few of the other powerful libraries that can be used to send emails with Python:

-   Yagmail
    
-   Envelops
    
-   Flanker
    

  

## Bulk Emails

Bulk email services can be used to send a massive amount of emails for different purposes like marketing and promotional tasks. There are many bulk email service providers. Although they are not free, some of them offer trial versions without you having to purchase their complete service.

The following are a few of the bulk email service providers.
|Service|Free Plan|
|--|--|
| sendinblue |300 emails a day  |
|Pepipost |100 emails a day|
|mailgun|10000 emails per month|
|mailjet|6000 lifetime emails|
|SendGrid|40000 within the first month|

## Conclusion

Python is a great way to automate email sending tasks or even sending automatically generated emails to customers. The standard library required to send an email is smtplib, but there are many other libraries that allow additional styling, adding images, and adding attachments. Emails you send through Python can be transmitted through protocols like SSL and TLS ensuring that your email's content is encrypted.

Disclaimer: This article is purely for educational purposes. If anyone uses it with malicious intent (spamming), we will not be liable for any losses or damages in connection with the use of this tutorial.







# The Ultimate Guide to Working with APIs in Python

## Introduction
    
Python is one of the most versatile languages that can be used to write programs across many disciplines. Most of the time, these projects involve acquiring data and information from other websites. For instance, when websites like Expedia find the best hotel and flight deals for you across hundreds of websites and other platforms, they are relying on application programming interfaces, which are also known as APIs.

## What is an API?
    
Technically, in simple terms, an application programming interface can be identified as a way of integrating one software component with another via the means of a network. In other words, APIs can be used to harness the power of different services from different companies or organizations. There are various rules and specifications that these APIs are built on and it depends on how the API developer has decided to define these interactions with external parties.

When we are integrating an external API into our code, we really do not have to know what happens inside the external software component. Therefore, we can also call these application programming interfaces an abstract layer. It simply means that the complex functionalities inside the code have been hidden from the external world only providing just the right rules, specifications, and the tools to interact with it.

APIs have also been around for a really long time and back in the day, they were only used in the local machine. However, with the internet being ubiquitous, more public APIs have become accessible via HTTP by everyone for tasks such as acquiring weather data, currency exchange rates, breaking news, etc. It should also be noted that being public does not necessarily mean they are free. There are public APIs that require payment of a subscription.

## What are REST APIs?
    
REST is a very common term that we hear when it comes to APIs. At the most fundamental level, REST can be identified as a specified set of rules or conventions to structure an application programming interface that can be accessible via HTTP. In HTTP, there are methods such as GET, POST to interact with a remote source. In REST, we can have these same methods to interact with a supported API. These are called REST APIs. The best thing about REST APIs is that the resource can virtually be anything.

We will not look at some of these methods, which we can also call requests, that will be used most commonly when we are interacting with a REST API.

## Type of Requests
    
Request methods are case-sensitive, and should always be noted in upper case. There are various HTTP request methods, but each one is assigned a specific purpose. HTTP requests work as the intermediary transportation method between a client/application and a server. The client submits an HTTP request to the server, and after internalizing the message, the server sends back a response. The response contains status information about the request.

In HTTP, there are many types of requests. They are also actions that are to be carried out involving remote resources which are specified via a given URL. These requests, generally are case-specific and work as a transportation medium between a server and a client. Simply, when a client sends a request, the server receives it and responds appropriately by sending back a response. When it comes to REST, in four of these requests. Let’s go through them now.

### 1.  GET
    
GET requests are associated with requesting and retrieving data and information from a remote API. This is the most common type of request.

### 2.  POST
    
POST requests are another common type of requests. They are generally used to send data over to the remote server to make new entries or even update existing resources. POST requests can be used to send resources such as information, JSON files, other types of items to the database or the inventory.

### 3.  PUT
    
PUT type of requests can be used to change or modify data in a remote database.

### 4.  DELETE
    
As the name suggests, this request can be used to delete existing data in a database which is specified as a URL.

Now that we are fairly familiar with the type of request that is most commonly used, let’s go ahead with some coding.

## Python Request Library
    
When we are taking the advantage of an API, we need to meet few of the requirements. For instance, first, we need to establish a communication link with the public API. Then sometimes, depending on their set of rules, we may or may not need to have authentication such as a secret key. Let’s take a look at an example of a simple request we can send. For this, we will be using the ‘Request’ library.

```python
import requests
response = requests.get('https://www.python.org/')
print(response)
```
Output:

```
<Response [200]>
```
If we look at the above code, we are importing the request library. Then, we are using the request.get() method to make a request to python.org. Then we are printing the response. Using this response, we can see what headers we have received as well as the body which has the content. As for this request, we are retrieving the response as 200 which is the HTTP status code for ‘OK’ which declares that the request has succeeded.

Before we proceed further, let’s have an idea about the status codes.

#### 1.   200 – OK
#### 2.  204 – No Content
#### 3.  301 – Moved Permanently
#### 4.  400 – Bad Request
#### 5.  401 – Unauthorized
#### 6.  403 – Forbidden
#### 7.  404 – Not Found
#### 8.  500 – Internal Server Error
    

As we already know, the response that we receive contains several parameters that are important to the request. For instance, we can call these parameters as follows.

```python
import requests

response = requests.get('https://www.python.org/')
print(response.status_code)
```


Output:
```
200
```

This means that we can access the status code parameter in our code and use it to our advantage in structuring the flow of our program depending on this status code.

```python
import requests

response = requests.get('https://www.python.org/')
if(response.status_code == 200):
	print('HTTP OK')
```

Output:
```
HTTP OK
```


Moreover, if we directly use the response object inside an if clause, we can make it evaluate True for status codes in between 200 and 400.

```python
import requests

response = requests.get('https://www.python.org/')
if(response):
	print('Request was sent')
```

Output:
```
Request was sent
```

Before we move on further, we need to have a slight idea about what endpoints are.

Let’s consider the following URL.

https://myapi.someapi.com/config/gettime

Imagine that we are using it to retrieve the local time.

Then consider the following URL.

https://myapi.someapi.com/config/getdate

As the name suggests, we can imagine that we are using it to retrieve the current date.

Both of these can be identified as specific locations or URLs that correspond to certain functionalities and features. We can call them APIs which are originating from the same server. Therefore, we can call them endpoints as a general term.

Now that we know what endpoints are, let’s move on.

  

## Accessing Public APIs
    
As we already know, public APIs are services that are open and can be accessed freely or by subscribing to their service.

Let’s go ahead and have our first experience with accessing a public API using the requests library. For that, we will choose the popular [Open Notify](http://open-notify.org/) API service. Using the provided APIs, we can retrieve information about the real-time location of ISS over the earth in terms of latitude and longitude. It is a great API for beginners as it has a very straightforward design. It does not require any authentication and it does not support any inputs to be given from the client side. Therefore, it is a great starting point for APIs.

However, before we do that, let’s check the status code we receive using this API.

```python
import requests

response = requests.get('http://api.open-notify.org/iss-now.json')
print(response.status_code)
```

Output:

```
200
```

Let’s specify a non-existent endpoint and see what status code we receive.

```python
import requests

response = requests.get('http://api.open-notify.org/wrong_endpoint')
print(response.status_code)
```

Output:

```
404
```

We have received the status code for Not Found. Let’s go ahead and write the code to retrieve the real time latitude and longitude of the International Space Station now.

```python
import requests
import json

response = requests.get("http://api.open-notify.org/iss-now.json")
print(json.loads(response.text) )
```

Output:

```
{'timestamp': 1600261290, 'iss_position': {'latitude': '-33.2478', 'longitude': '33.8012'}, 'message': 'success'}
```

If we look at the code, we are importing the json library in addition to the requests library we imported earlier. In most cases, we are receiving the responses as jsons when we are retrieving data from APIs. Therefore, we are using the json library to parse the responses that we receive.

We can separate the latitude and longitude from the response as follows.

```python
parsed_json = json.loads(response.text)

print('Timestamp: ',parsed_json ['timestamp'])
print('Latitude: ',parsed_json ['iss_position']['latitude'])
print('Longitude: ',parsed_json ['iss_position']['longitude'])
```

Output:

```
Timestamp: 1600261290
Latitude: -33.2478
Longitude: 33.8012
```

We also know that there might be instances where the server might be experiencing downtime. Therefore, we need to be able to address any such potential occurrence. Let’s have a status check before we print the response and rewrite the code.

```python
import requests
import json

response = requests.get("http://api.open-notify.org/iss-now.json")

if(response.status_code == 200):
	parsed_json = json.loads(response.text)
	print('Timestamp: ',parsed_json ['timestamp'])
	print('Latitude: ',parsed_json ['iss_position']['latitude'])
	print('Longitude: ',parsed_json ['iss_position']['longitude'])

else:
	print('We are experiencing issues. Please try again')
```

If we look at the code, we are first sending the request, then we are taking it through a status check to see if we have retrieved the HTTP OK response. It should also be noted that we are using the same lines but including the code snippets from the point we are starting to parse the response.

Luckily, there is another [endpoint](http://open-notify.org/Open-Notify-API/People-In-Space/) that is available in the same server that we can try. It is ‘How Many People Are In Space Right Now’. If the data is available, it also returns the name of the spacecraft as well as of the astronauts.

```python
import requests
import json

response = requests.get("http://api.open-notify.org/astros.json")

if(response.status_code == 200):
	parsed_json = json.loads(response.text)
	print(parsed_json)

else:
	print('We are experiencing issues. Please try again')
```

Output:

```
{'number': 3, 'people': [{'craft': 'ISS', 'name': 'Chris Cassidy'}, {'craft': 'ISS', 'name': 'Anatoly Ivanishin'}, {'craft': 'ISS', 'name': 'Ivan Vagner'}], 'message': 'success'}
```

Fortunately for us, it responded with the above letting us know that there are three people in space and that all of them are occupants of the International Space Station. We did cross check it with a few sources as well as [https://www.howmanypeopleareinspacerightnow.com/](https://www.howmanypeopleareinspacerightnow.com/) and turns out, the response we retrieved is in fact correct.

## JSON and Python
    
Since all the responses we received so far contained json, we will learn a bit about the json library from Python.

JSON stands for JavaScript Object Notation. It is a way of transferring data in a both machine and human friendly manner. Python has given a json library for us to easily handle these json objects. This library has two main functions which are useful for us.

### 1.  json.dumps()
    
### 2.  json.loads()
    
json.dumps() function can be used to convert a json object to a string. The other function json.loads() can be used to take a json string and convert it to a Python object.

We have earlier used json.loads() function to convert the json string to a Python object and access it using indices. Therefore, we will only look at how we can use json.dumps to format a response we receive.

```python
import requests
import json

response = requests.get("http://api.open-notify.org/astros.json")

if(response.status_code == 200):
	text = json.dumps(json.loads(response.text), sort_keys=True, indent=4)
	print(text)
```

Output:
```

{
	"message": "success",
	"number": 3,
	"people": [
		{
			"craft": "ISS",
			"name": "Chris Cassidy"
		},
		{
			"craft": "ISS",
			"name": "Anatoly Ivanishin"
		},
		{
			"craft": "ISS",
			"name": "Ivan Vagner"
		}
	]
}
```
There is it. We have touched the fundamentals of how to deal with json objects in Python.

## Conclusion
    
In today’s tutorial, we have learned about what APIs are, what REST APIs are, types of requests, different types of status codes, what JSON objects are, and how we can deal with them in Python. These are the fundamentals that are essential in handling more complex APIs using Python. Feel free to go ahead and try out different APIs that provide functionalities to perform various tasks including calculations and data processing in addition to just retrieving data.The Ultimate Guide to Working with APIs in Python

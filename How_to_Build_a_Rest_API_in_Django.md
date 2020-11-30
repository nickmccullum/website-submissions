# How to Build a Rest API in Django

## What is REST?

REST is the acronym for REpresentational State Transfer. This is a software architecture style that is used to create web services. Any web service that is created using this architecture style is called RESTful web service. REST API provides the functionality to easily provide data to other applications and services, also in some instances to manipulate the data within the REST API.

Following are the main request types of a REST API

-   **GET** - Used to read/request records from a given endpoint and the parameters specified.
-   **POST** - Create a new record in the provided data set.
-   **PUT** - Update an existing record according to a given endpoint and parameters or if record not available create a new record.
-   **DELETE** - Delete the specified record
-   **PATCH** - Updates the individual fields in a record partially updating the record.

API is a window to a database. The API backend will handle the database querying and formatting the response. Typically, the result will be a static response provided in JSON format. A RESTful API provides a simpler way for applications to communicate with each other. The process of querying and converting database values to JSON or another format is called serialization. When creating an API, the correct serialization is of the utmost importance.

## What is Django Framework?

Django is a free and open-source high-level python web framework tailored to creating web applications and services. When creating an API, the Django framework provides built-in functionalities to simplify the process.

The Django framework is based on the model-template-views architectural pattern that allows the developers to focus on the program logic while handling the low-level implementation itself. For example, Django ORM handles the database migrations and queries written for Django models and the interoperability of the Django REST framework provides the functionality to easily serialize the database models to RESTful formats.

## Creating RESTful API using Django
This section will cover how to create a simple Django RESTful API utilizing python virtual environments for simpler dependency management. The API is created in a Microsoft Windows-based environment.

Let us create a Python virtual environment called “simple_rest_api” using the “venv” command in a windows environment.
  
```bash
python -m venv F:\python_projects\simple_rest_api
```

Use the following command in a Linux environment.

```bash
python3 -m venv <Path to Virtual Environment>
```
  
After the virtual environment is created, we use the activation script in the Scripts directory of the created python environment. in this instance, we will be using “Activate.ps1” as we are using PowerShell terminal.

```bash
<venv>\Scripts\Activate.ps1
```
 
![](https://lh6.googleusercontent.com/AMm3XfAzBshdGeDnDC9LbmJI0RYkB9lSIrFjmb0BZVQMEw_Cb5KhTZnm3G35x4p_38IiBPUGOZ39uNpSw990uUDQ9zlOluVP3QZxvUp69prxGeOZKf6bljp0kIj1Bb_8womwjioe)

### Installing and Configuring Django

Within the virtual environment, we install the Django framework.

```bash
pip install django
```
  
![](https://lh6.googleusercontent.com/ha9EqBRZsYGEUA47UrDUntRiSUUIbbiSymK1B-RdlmGAnY2tHlCffYtI8QjWb1myGE-X8FKgbzijfdwiVfg0c8UdSxoN2UX2x0wDikR_fwumLz65sStpKN0B7KKNskFAPJAh2wiI)

After a successful installation of Django, let us create a Django project called “vehicle_details”
  
```bash
django-admin startproject vehicle_details
```
  
![](https://lh6.googleusercontent.com/nSdfCDBcRXVVh1DYWUz32YZtLzYu43o1phQC8wefFE3KllBaEaAa0SkrH8ifTWLZ0pL0_CK98AlY4hewe6VESenfH7VPrjfLQ4USJyGoAPvmi5jptGjFrdwERkY-aLmbggmmpRlY)

We can see that a Django project was successfully created by exploring the newly-created directory. To verify that, let's start the project on the Django server as shown below.

```bash
python .\manage.py runserver
```
 
![](https://lh5.googleusercontent.com/T5ggnR3_D9-JuN2VFWAuKqyJeWLVqj8lz4iWdWwpgcNb2NzPwI6aZ17a8m4kvCR5dBgmpnVzG7T0xozNJwGWo0pjdfzen5OhAQP0x1q-nmpFFmE2UyGIBIVWN7Y9duO7mVCnsoVP)

If the web application is active we can see the following screen by visiting the URL [http://127.0.0.1:8000/](http://127.0.0.1:8000/) or [http://localhost:8000/](http://localhost:8000/)

**Django server interface**
![](https://lh5.googleusercontent.com/1XOn1n7RKInC4-C6GigCQUlUqJ2aCF62NGpoxHScUs4UgbmdwJNJjShzNYG5mFfvtXYUFqf8_rbzNsvw9ys2c4v04YWXjQSM9DQGUbeY9lwR-DUmll1G5_Lg6lqM8RWdoYc07FuX)

### Creating the API App

although we can create the API within the current directory structure, the best practice is to separate the Django project into separate apps for easier management of the codebase.

Let us create a new application called “vehicle_api” and register it as the parent “vehicle_details” project.

```bash
python manage.py startapp vehicle_api
```
![](https://lh5.googleusercontent.com/QFHPUIQDz12T4qiRZVITlzdGQEKD9nGa_2Y-uA2VwZ9Zi7aFtnhldnqv7kKLz_7V3jLBVWj3YRlpg4S3iLbKtcA2lVaExz4uyfh4xmwwZYu5qANUUKRi4HCOAaWgWSq4hRGQ_F8C)

We edit the “vehicle_details\settings.py” file, so the Django framework will identify the newly created “vehicle_api” app.

![](https://lh4.googleusercontent.com/aTXNAKMTb49thiNSyn2goSsCkGYqRZKdkHSeVjYCSmnQoJnQhZemRDgyrqRsilfSyEfEFtc9fLY6J9USYxodotsFTdrs418JxPydqToAprPa7-eM9OqgcZstPskpVLTvSeJRAzf_)

**settings.py**
```python
INSTALLED_APPS = [
    'vehicle_api.apps.VehicleApiConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
  
### Migrating the Database and Adding Administrative Users

We created a new Django model when we created the new app. When we create or modify a model, we need to inform the Django framework to migrate the changes to the database. The Django ORM makes this task easier by automatically creating the necessary SQL commands.

If a new project is created without explicitly creating a database, Django will automatically create an SQLite database for the project. In this case, we will migrate the built-in models in the database using the following command.

```bash
python .\manage.py migrate
```
  
![](https://lh5.googleusercontent.com/cC2TO68v1bKb5nUWILk8NlyZvQ1eOySqZZQodwsl4u_kJCpiWJAoUvGOBy6R4lb6ubfqeGydbMnrvt4HP0SKMf7OqsU237rXdehfDxW7ehmN0f-5Y62z-doTxY55D-gFJoY4TaAg)

After migrating the database, we will create a super-user administrative account to access the project admin interface to review our database. We create an admin account by using the following command and then entering the necessary details.

```bash
python manage.py createsuperuser
```
![](https://lh4.googleusercontent.com/tUZlhTT5lVXgeVVl1gsOPW_A_JmOaTvyhVhK18lkG3r1PF1nMnb1g6Vtvl65iG9-9Hl8ei1FQpEA9JoTyuYZ5rr6K3O1jvmxVFjk0nqOGoqGXSBLwlVpFVDZaRNddrz2o7_N5L8B)

Let us verify if the server is working correctly by starting the Django server and accessing the admin interface from [http://127.0.0.1:8000/admin](http://127.0.0.1:8000/admin) or [http://localhost:8000/admin](http://localhost:8000/admin)

```bash
python manage.py runserver
```
  
**Django admin login screen**
![](https://lh5.googleusercontent.com/4rvv0f-K-8bO4Kpk0jc8z57cn3JhSBVU5fTmhG1Chu2lyU46hTfEHuZSP_PZMjs2E6J_GnmxjGiPtlHmbOMd9L4PBvR-j4Z8EvelEmyg-MINYvzFSCw5LqhJ46JA073qWMo9v3BV)

From the admin login screen, we enter above-created super-user login credentials to access the admin interface.

**Django admin interface**
![](https://lh5.googleusercontent.com/m55S831KN3O9AnopuwW5YXaPszT4BBoIK0fHbEPN9BDXXY-iKmfjr1GMj7AWzCFbNMGf3GHhpJbRX1jnxVX7_AJy3vXI0aO6ouDOk8mVdGG_gPnNIVsh19I7XJMIE7XV7AMSoSGJ)

### Creating the Database

Although we have created a “vehicle_api” application, there is no database associated with it. Using the model functionality in the Django framework, we will create a New_Vehicle database by editing the models.py file.

  
```bash
.\vehicle_api\models.py
```
  
```python
from django.db import models
 
class New_Vehicle(models.Model):
    make = models.CharField(max_length=60)
    model = models.CharField(max_length=60)
    year = models.IntegerField(blank=True)
    price = models.IntegerField(null=True)
 
    def __str__(self):
        return self.make + " " + self.model
```
  
In this model, we create 4 fields to store the vehicle details and define a (__str__) method to inform the Django framework to return the combined make and model of the specified record. This database is fully managed by the Django ORM. , It is mandatory to migrate the changes when a modification is done to a model. we instruct Django about it using the following commands.
  
```python
python manage.py makemigrations
```
  
```python
python manage.py migrate
```

![](https://lh6.googleusercontent.com/lfD4iCEYrGq4VFtt3QqcT4j4YLGj_s6zRCmgPrx1pVXxvNscpqxtqFAQNiKUvFLNcd6IcY1V6fuBxZm54YsERq8dn1yThf_BuFmzRh92LkvX8YpAuq8hFw-c7vDCsN_4LzuSKrlu)

### Associating the Database with the Admin Interface

After the database is migrated, we will modify the admin.py to associate the New_Vehicle model with the admin interface.

```bash
.\vehicle_api\models.py
```
  
```python
from django.contrib import admin
from .models import New_Vehicle
 
admin.site.register(New_Vehicle)
```

Now let us start the Django server and log in to the admin interface to check whether all the change we made is reflected in the interface.

```bash
python manage.py runserver
```

![](https://lh6.googleusercontent.com/YPG_G_JsUGm__FRtRKaHbScJzz2bWmCHZ9WvcjY8G6lhWX-mKDk7Cv8TBoXnw5yB5eqevtHDfc4qthbb7B7BAAf4HMcdMM1GV5Wln6IGSauvCB6zzVXiKTzN6Y-2fhXqnSReTE_9)

**Associated database**
![](https://lh5.googleusercontent.com/9NgJVHdDdoYpFs0LJuCoQ3D54PMB3SXSTT-ltZCtnvtnLNXUxArsLs6v7Jfyiyi4j1OFsWsBxoBktZmA441oRqfc-4MXZ4CjukFNofy-DRz4ewNK61Sl2zlDHpIaOLOwYV6tmwEZ)

Finally, we will add some data to populate the New_Vehicles by adding the details as follows.

**Creating new records**
![](https://lh5.googleusercontent.com/rTIwYlWuhe8g_vMsvHbIPVMJkqwZwOGEIfskIXdmeKBmc3ZH56x83kz0Zeb34Abxai_NGoWi52xA2QRBV593ozvd7LQGI283hN5nGyfBnwzeffPqc5CnFdQab0UM11eNViRsTZQW)

**All records within the data set**
![](https://lh5.googleusercontent.com/ouL0wHt-Hq9RauR0HQpk-M0JnOiNKgjqqWM7OM_oMpn6z4DP75AR4YoYJIonUZOnD-MPxgFFVKpIJ_5e7XUCMaWPeCDveIS1C2dCDYUYUDP-aE8aeHgJ_C2oKjtaxbQ4YOg3yW9m)

### Integrating the Django REST Framework

#### Installing Django REST Framework
The Django REST framework comes as a separate pip module. Therefore, we install the REST framework module separately and edit the vehicle_details\settings.py file to integrate the REST framework functionality with the existing Django project.
  
```bash
pip install djangorestframework
```
  
![](https://lh4.googleusercontent.com/_j97imy9UbxWzjwEU5vcL9r1gt7riV7uYMnPzjiV0QOA70HB3ojnYFtca0JIoEqdG39cbCFqKWqdkzjzH-w0--H7IISyhvNIZIX-I4m7AjKGbvEcqQ-0uKk7mM72uWBMeHbovM_-)

  
```bash
.\vehicle_details\settings.py
```
  
```python
INSTALLED_APPS = [
    'vehicle_api.apps.VehicleApiConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',
]

```

#### Serializing the New_Vehicles Model

The Django REST Framework will convert the New_Vehicle model to JSON format so any API user can parse them. Serialization removes the python dependency of the data set as any programming language can read the JSON format. Also, we can specify which fields should be represented in the JSON string using a serializer. When a user POST JSON data to the REST API, the serializer will convert the JSON to a valid model that can be used inside the programme.

The following example demonstrates how to create a serialization file called “serializers.py” within the “vehicle_api” app. This file will import the “New_Vehicle” module and the REST framework serializer and create a serializer class to only provide the make, model, and year fields via the API.

  
```bash
.\vehicle_api\serializers.py
```
  
```python
from rest_framework import serializers
from .models import New_Vehicle
 
class NewVehicleSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = New_Vehicle
        fields = ('make', 'model', 'year')
```
  
#### Displaying the Data

In the above steps, we have configured a model, added some data to that model and setup serialization to convert the data to the parsable JSON format. In this section, we will create a view and set up URLs to provide access to the data via the API.

##### Setting up a View

Views or “viewsets” are used to send data from the application back end to the browser. The Django framework allows these viewsets (ModelViewSet) to accept and handle GET, POST, PUT and DELETE requests without any additional coding. They also provide us with a single endpoint to handle requests for all views of objects in the database as well as individual object instances.

In our application, we create a view to query the database for all the items in New_Vehicles and pass the data to the user-created serializer so the data gets correctly converted to JSON format.

  
```bash
.\vehicle_api\views.py
```
  
```python
from django.shortcuts import render
from rest_framework import viewsets
from .serializers import NewVehicleSerializer
from .models import New_Vehicle
 
 
class NewVehicleViewSet(viewsets.ModelViewSet):
    queryset = New_Vehicle.objects.all().order_by('name')
    serializer_class = NewVehicleSerializer

```

##### Setting up URLs

The Django URL module provides the users with a way to route the request to the desired view (viewset). In Django, the URLs will be first resolved in the project level. We will edit the urls.py in the “vehicle_details” project folder and add the URL to the “vehicle_api” application.

  
```bash
.\vehicle_details\urls.py
```
  
  
```python
from django.contrib import admin
from django.urls import include, path
 
urlpatterns = [
    path('admin/', admin.site.urls),
    # Path to vehicle_api
    path('', include('vehicle_api.urls'))
]
```

Now we have configured the URL to direct to the “vehicle_api” application, the next step is to direct the user to the requested view. This is done by creating the urls.py file within the “vehicle_api” application.

```python
from django.urls import include, path
from rest_framework import routers
# Importing all Views
from . import views
 
router = routers.DefaultRouter()
router.register(r'NewVehicle', views.NewVehicleViewSet)
 
# Automatic URL routing
# Login URL for Browsable API Functionality
urlpatterns = [
    path('', include(router.urls)),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```
 
The router is a Django REST framework module that will dynamically direct the request to the specified resource. In this case it will direct to the “NewVehicleViewSet”. If any change occurs in the database, the URL will be automatically updated. The router depends on the views(viewsets) to correctly route the URLs.

After the URL patterns are included for the router, we have enabled the browsable API functionality with basic authentication which provides us with an interface to test the API.

##### Setting up Pagination

When dealing with large data sets the pagination functionality provides the API with a way to limit the resulting records to a specified amount. This can mitigate performance issues when retrieving or manipulating large data by breaking down the data set to manageable chunks. We can configure a pagination limit using the “vehicle_details” project settings file by adding the following code block.

  
```bash
.\vehicle_details\settings.py
```
  
```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10
}
```
  
In this instance using the ‘PAGE_SIZE’ attribute we limit the maximum result to 10 records.

### Testing the API

Let us start the server and test if the simple RESTful API is working as intended.
  
```bash
python manage.py runserver
```
  
![](https://lh6.googleusercontent.com/N2BYmp8xz0Bhrnlq0NF70ArPXf5VGP8jP1mU2QA9O_fFmt9xSLtqET8AcNBvQ6SYKGtMJttJZQW8EjLSga2qHbEjP6HAOaVt9ePSwLFCmmJ_gPeG2cAvaZy4O5DAiozq6UdnUCNf)

**API testing view**
![](https://lh4.googleusercontent.com/SonunnhDYpIfHyuM-Doli7DAg4oTfHih36GShOTVL_STr0JBDhx0aojRYcvE4TWqMlijwfKhcgrWdwjH4UZKHFKWUJDreESD9yBHZCsgBuDaI6aLsrjxhQ1o7TlNIW6zWL4CGo6-)

In the above test, as the API Root is presented to the user, we can identify that the Django Server is working as intended. In the following examples, we will check the functionality of the API.

#### GET Request

We click on the link provided in the API Root [http://127.0.0.1:8000/NewVehicle/](http://127.0.0.1:8000/NewVehicle/), this will redirect us to a get request where the resulting data set will omit the price field and display the remaining fields. The results are sorted by make as we have specified the sort order to “make” field in the view.

**GET Request**
![](https://lh5.googleusercontent.com/WosBW5wcC-5PhtP1Szt7uX7x8HgrnOT1VLm6nJtsry0VGpCTQBKXYTbjkswZWAaLM7TMPdGHAqkS9RJlxG3mmkiBu6Isaw4lLpPR7oWA0sD2fkb_Hkrz1Cn6-Xbq7vbDp48-9KtL)

**Requesting the URL via CURL**
  
```bash
curl --location --request GET 'http://127.0.0.1:8000/NewVehicle/'
```
  
![](https://lh6.googleusercontent.com/r8QRUhxJk41PPARL40-ZUYk5zTdPGDGOGae9fOadO58ZTMdDoGpXYqU-oh2DwFiinu1yBIPXQxwx66cRistSTfRbiZ1VUyKhISTIpM6RIDmkNaTMz5aKeRcB006w7tRvAXkFBcYS)
  
**Requesting a Single Item via CURL**
  
```bash
curl --location --request GET 'http://127.0.0.1:8000/NewVehicle/1/'
```

![](https://lh4.googleusercontent.com/rHCpXl1NikA2oid1irPeGH8l0evx9j0HpaBj9sxzBznnHWevmbX6zc4m3--V8AhuzvuTBP4SojQRyl_teDTdAQJdv6a5VkYHlbGyhRRMQhIO3zcioEBev3ryVgRxXwv9iAzNGrv7)

#### Modifying Serializer and View

We can change the serializer to include an id field to make the resulting data set more user friendly. This is achieved by modifying the serializers.py

  
```bash
.\vehicle_api\serializers.py
```
  
```python
from rest_framework import serializers
from .models import New_Vehicle
 
class NewVehicleSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = New_Vehicle
        fields = ('id','make', 'model', 'year')
```

The id field is automatically assigned for each record we created. Then we change the sort order by defining the “order_by” to “id” field in the view.
  
```bash
.\vehicle_api\views.py
```
  
```python
# from django.shortcuts import render
from rest_framework import viewsets
from .serializers import NewVehicleSerializer
from .models import New_Vehicle
 
 
class NewVehicleViewSet(viewsets.ModelViewSet):
    queryset = New_Vehicle.objects.all().order_by('id')
    serializer_class = NewVehicleSerializer
```
  
The output indicates that the new field “id” has been added to the resulting data set while sorted by “id” field.

**Modified GET request**
![](https://lh4.googleusercontent.com/oPLUcXNpkV1b7jDisYINIX-GR6LrspOUekRWKjflG7vxFGtB1PNFIDLjz28EI3Dy1wZAklXlRMkCcBf4rrtPCM4EhFF8WOZT7Qy42x4pib5tuTovBKXjRwwLet5IlYkTkQvl51Bj)

**Requesting a Single Modified Item via CURL**

```bash
curl --location --request GET 'http://127.0.0.1:8000/NewVehicle/1/'
```

![](https://lh4.googleusercontent.com/B66WRVo4550kt7vx__gYqBr-6VZoQlktWSv-F2NqzM82IPzKvkpkAWcIC4Mpq1n51DZz9hIZCdhKkLbGGVwmC422ZoRFW5C2vBhA238l48uwPmzmFQOUdtyr30jynphy3SbChMim)

#### POST Request

Using the inbuilt form in the Django REST framework, we sent a new POST request to add a new set of data as shown below.

**New record creation interface**
![](https://lh5.googleusercontent.com/r2fKdLGNq9_zdmCao0bOtA8tuR2iLmsAgCnor5HHJL6UQ50wj_QL2IqynAActdQEXBVsS3taMQHq1ED49RmRO0JfcAorgIEE7k77yXwd8-LN8OvYT-KOdYCLOxxO1NcIsHVr1R6i)

**Newly created record**
![](https://lh4.googleusercontent.com/4NDLDUUr39lgGZJtqx3e0aJzjKrbL_SeZ1qiZMKhIlY_9WY2cTKcFv4mxfniqrdPJTO7s9OSXocYrWwJJrea9kmFRWVLBWJGa5CoL8QP4oRDlNCMTKlpfrpUwIOQASp14mHHOdfQ)

From the response code 201, we can surmise that the new vehicle details were successfully added to the database. Let us verify this using a GET request.

**GET Request to check the new record**

```bash
curl --location --request GET 'http://127.0.0.1:8000/NewVehicle/'
```
 
![](https://lh6.googleusercontent.com/mYtXoK9WG1X8aUR-5w6R-nb_GXoe621KuQTzuGXQHcz_VO_gR-0OyzDm6xQUij0jqAFC-6KFiBcqs9Cj2IL-gE6VQW2nXDIfVq99YRyG2gFY8HRiQZb8vmBFwA3V9Jk-tZUVerlg)

#### DELETE Request

Let us use the DELETE request to delete the newly created record. The DELETE request will delete the specified record or records. in this instance, we provide the “id” as the identifier to indicate which record to be deleted.

```bash
curl --location --request DELETE 'http://127.0.0.1:8000/NewVehicle/4/'
```
  
**Before and After the record is deleted**
![](https://lh6.googleusercontent.com/uZgBQ3OEWF3NFYUX9yyi-iZaUtmWl098hpvHFBYySlJHamO4Qo4QzHyxhsXWXtt00sjJcMSBHjIluPpxJtb70yWQER9coLuVmmWDiCElpl7cGKEo3WWUTnS2xOzUforNruxekXyB)

## Conclusion
in this article, we learned what a RESTful API is and how to create a simple API using the Python Django web framework. RESTful API are the building blocks of the current connected world allowing easy communication between different types of applications and services.
# Useful Features of the Django Shell

## What is Django Shell
The Django shell is an interactive command-line interface shell environment that combines the Django framework functionality with the regular python shell. The Django shell loads the project-specific parameters and settings that only work within the project which allows the user to isolate the work environment and focus on that particular project.

One of the main functionality this shell provides is easy access to the object-relational mapper (ORM), which allows the user to directly interact with the database. The ORM is responsible for carrying out database queries within a Django project. The object-relational mapper reduces the need for extensive knowledge of relational databases and eliminates the need to use SQL queries within the project in most instances.

### Accessing the Django Shell
The Django shell can be accessed using the `shell` command on a Django project. We will be using a standard Django project called “foodinventory” within the “food” python virtual environment throughout this article.

```python
python manage.py shell
```
![](https://lh5.googleusercontent.com/hjimRMH-kwIwcsg3vOiMwAY_ZpNFMyt6jhQdVpqAsGqIyCf5yRzb8kAf3axl_TtR73H8KU8tmTc2mYlKAFrpgP_YavY0TmKupHClxE2gZLDL4KsnqTuKH6TGZHJvQJk7ZUrBMWUH)

Before diving further into the Django shell we will create a Django app called “fruits” within the “foodinventory” project. Then populate the models.py by creating a “FruitsInfo” table and migrate the changes to create a simple SQLite Database.

```python
python manage.py startapp fruits
```
  
**models.py**
```python
from django.db import models

class FruitsInfo(models.Model):
    name = models.CharField(max_length=30)
    origin = models.CharField(max_length=60)
    price = models.DecimalField(max_digits=4,null=False,decimal_places=2)
    availability = models.IntegerField(default=0)

    def __str__(self):
            return self.origin + " " + self.name
```
  
**.\foodinventory\settings.py**
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'fruits'
]
```
  
```python
python manage.py makemigrations
```

**RESULT**
![](https://lh5.googleusercontent.com/VZIh4a75rXl_KV3PEKImcwhJ3cuxsKcJlDh5aDqoYLrOz6oqdnEGKXc6HMdFuCCcH6llzJoOtMtAtUGaRiJBpr-MF5vOu-UtTXTOCFzg3GqR5zk58AeHyKtUog3nVIvW6spDaxUJ)

```python
python manage.py migrate
```
  
**RESULT**
![](https://lh6.googleusercontent.com/HmRrCynRozDcvXeRGTSpW_Gz2nuNofhjb0oCTvcLcVp6j9Ho-_-FmyaFibvc_R9bAA6SKyxvWHGEJrMXsa16d5Z0Sn05ZXm-6F9GOYuHWn2zRwajo0ksJwB0L7B0PggcqdpDtRlk)

## Inserting Data into the Database
In Django, a model class represents a database table and an instance of that class represents a particular record within the database. This is analogous to using an INSERT statement in SQL. A record can be created simply by initiating the model class using the defined keyword arguments and calling the save() method to commit the new record to the database.

In the following example, we will look at how to add a new record to the FruitsInfo model class. First, we need to import the “FruitsInfo” class to the Django Shell then create an object of the “FruitsInfo” class called the record using all the keyword arguments and finally using the save() method to insert the record to the database.
  
```python
from fruits.models import FruitsInfo  
record = FruitsInfo(name="apple",origin="USA",price=2.5,availability=1000)  
record.save()
```
  
**RESULT**
![](https://lh4.googleusercontent.com/riZPmD5JskIjDtaxkjEycxDwToZH0Ppmde2hrxF6HicXGuOSrQ5abkbW78CQj9pjukaXgokjMS8ZjEHkcn8wrvgSS4Fmk3Dl-73pws5aSigTOTmZt6or6PMuaeO0jxL-v28o4HoA)

As there are no errors indicated in the Django shell, we can assume that the record was successfully added to the database. Let us verify this by using the “all()” method to call all the records from the database.

```python
FruitsInfo.objects.all()
```
**RESULT**
![](https://lh4.googleusercontent.com/L3LCSzyJbfRme_UMPhk6sGOLxVKb0wopVnLFHEMINTOrUSZ-LgNa5LqSISzqwtKjD5F3YaXCjTCwhSTvDO7cvfXZqgcuxWIeveNq54JQvzWWjc_ScEeySrwbqZTkOy9HF5LdTBMu)

Because we have defined a “\__str\__()” method to display an object in a human-readable format, the “all()” method will display only the value defined in the “\__str\__()” method. The value() method allows the users to extract the values of a given object as shown below.

  
```python
FruitsInfo.objects.all().values()
```

**RESULT**
![](https://lh5.googleusercontent.com/7ZkhnKO7bz_JDH1DqULeE5wdHIs31a7o-8wfDzMzfRzt9EJfKIKUPFqAy3D84NFJlX6c5Z8jkI9OdXNeRHfjCBvl5kGOSby_7lA2S3D74hw4wV8EiWQQcFxKy13tTOVI-7zEx71U)

Another way to insert a record to a model class is to use the “create()” method. It  eliminates the need to call the save() method to commit the record to the database.

```python
from fruits.models import FruitsInfo  
record = FruitsInfo.objects.create(name="orange",origin="canada",price=1.25,availability=2000)
```

**RESULT**
![](https://lh4.googleusercontent.com/e8SBa2Hdb4JbC1AFXSoMFDAin8R2dHGQVOnxAOoEmQPgrvt7x761yaFVPxvFMPkMi0ZYDX2E5pNvgwPlo8Wcs3oDFx7K565rRjIQeh2nhOl_XpMXL4W356HKI0RQGQRl31ghXB7Y)

Let us verify if the record was inserted into the database using the “all()” method.

```python
FruitsInfo.objects.all().values()
```
**RESULT**
![](https://lh4.googleusercontent.com/IyXYA75PjUzTXLIrCHf2dGXwriiJQ6Tt6ymJJiEep7tqXsHINMBY2sFnRtV4U7sfRa1wi3NWu-hoxfubYNLlagxPp87Dhm5k8xCjf_3fZFT3HoHJtAhfAnO2Ksq43GWpyYY-lmLK)

The above output shows us that the new record was created without the need to declare the “save()” method.

### Inserting Multiple Records
In this section, we will look at how to insert multiple records to a specified class. We will create a new FruitsVendors class within models.py in the fruits app and migrate the changes.

**Modified models.py file**
```python
from django.db import models

class FruitsInfo(models.Model):
    name = models.CharField(max_length=30)
    origin = models.CharField(max_length=60)
    price = models.DecimalField(max_digits=4,null=False,decimal_places=2)
    availability = models.IntegerField(default=0)

    def __str__(self):
            return self.origin + " " + self.name


class FruitsVendors(models.Model):
    vendor_id = models.CharField(max_length=4, null=False, primary_key=True)
    vendor_name = models.CharField(max_length=60)
    vendor_location = models.CharField(max_length=60)

    def __str__(self):
        return self.vendor_id + " - " + self.vendor_name + " - " + self.vendor_location
```
 
In the new FruitsVendors class, we have defined a primary key field named “vendor_id”. Then we defined the “__str__()” to display all the data within the class in a formatted string.

**Migrating Changes**

```python
python manage.py makemigrations  
python manage.py migrate
```
  
**RESULT**
![](https://lh6.googleusercontent.com/uJ621pgfbfG-GB_UN7MejHIy7BxSM7p97j3B3Gu4i_zw7kBvp66sRCH0y37OYMNfF2plQ6S9zhTP2feeMpKxHqI-uHJ5yV676FyhJHgnyZic1zNy70x_fX3TbGS9Z8TRTKosdCfu)

Let us look at how to insert multiple records to the FruitsVendors class at one using the bulk_create() method and the Django shell.

```python
from fruits.models import FruitsVendors  
  
FruitsVendors.objects.bulk_create([FruitsVendors(vendor_id="V001", vendor_name="Fresh Fruits", vendor_location = "New York"), FruitsVendors(vendor_id="V002", vendor_name="Direct Delivery", vendor_location = "Sao Paulo"), FruitsVendors(vendor_id="V003", vendor_name="Fruit Mate", vendor_location = "Sydney"), ])
```
  
**RESULT**
![](https://lh3.googleusercontent.com/TEpATpjLfStZdnSPcoErH-gVTTKV8HYGRtr2ArdPq8Y0Mkhz-JkB2M3IEgImd9LMTUvRET6AQeg6NJXAOyIc09gXUON2_LVM1H-qcGjH_6AZSLd-p_7CZEH-I3xW8aB7JmLUl-rP)

## Searching the Database
With the Django shell, we can search for objects within a database. When searching, we can use filters to extract specific objects. This is analogous to SELECT and WHERE statements in SQL. Let us look at how to search for records within the FruitsInfo class.

### Searching for all objects

Using the all() method, we can obtain data for all the records within a table. If “__str__()” method is declared within the class, it will be the output of the all() method. To obtain the values within the object, we can append the values() method to the all() method.

```python
from fruits.models import FruitsInfo  
FruitsInfo.objects.all()  
FruitsInfo.objects.all().values()
```
**RESULT**
![](https://lh6.googleusercontent.com/17k84C2_Mu99krjG4Uw1prBOm_2MOGORwpKew3hdeUZdVVUQPidumCxHPeMfzV0fdggM_DjKIP58OXxVDrAVU1oy3UcDhuCVR1FtBlhkxMuJDSl1EsciMLWOo73364rW6skJNwb3)

### Searching for a Single Record
The all() method with the filter can be used to retrieve a single record from a table. This is accomplished using the filter() method. The following examples demonstrate how to search for records by the id field and name field.

**Search records by “id” integer field**

```python
from fruits.models import FruitsInfo  
FruitsInfo.objects.all().filter(id=1)
```
  
**RESULT**
![](https://lh4.googleusercontent.com/wIfziC1bXcaUd_uDfw0MGHndv_tbnRDj7dMIqQWtzB9RDaxocLNZlSCDTZGuH6q-qGnM2nBkGqUtxOQp6ngTsJfAHHKhGGJ7vY2I6tZNjVBSEfFiqb6InHGVeiTh_cAjfBJhr0Oj)

  
```python
FruitsInfo.objects.all().values().filter(id=1)
```
  
**RESULT**
![](https://lh4.googleusercontent.com/xpsN48OIl7trisJaMfA-cLi7Zrebptve4HPmunVpkuGmbgRX70xeMe-uT0OEYl-QVOyUGfneNtWU284hhvamnmryqMLBoTuGRMauViLcxO4QOWLZvh1ikrcK7WyUJAzE-nYlfS56)


**Search records by “name” string field**
```python
FruitsInfo.objects.all().filter(name='orange')  
  
FruitsInfo.objects.all().values().filter(name='orange')
```
  
**RESULTS**
![](https://lh5.googleusercontent.com/q1tZ1ClvudOvtuijamq4sc4z2UzIDUjRHewMf0_CO5VhxBxADlo1q7iOlq5TLXsgwgmi35KcGeH_iXlK4bgPfrs3oZo2-Mv1K6uayRUIUqE4PNKf9P2LH96ezDw9lC9SquBWgur1)

The filter() method will always return a Django QuerySet even if there is a single record in the output. If we wanted to retrieve a single record, we can use the get() method. However, if there is more than a single record that matches the query we specified within the get() method, this will result in a “MultipleObjectsReturned” error.

The get() method is most viable when we search using unique index fields such as the primary key. Let us see how the get method can be utilized using the “id” field.

```python
record = FruitsInfo.objects.get(id=3)  
print(record)
```
  
**RESULT**
![](https://lh4.googleusercontent.com/vi5cAqCWxevvo2mebG3giIlwrDWs1K6agEU6qPrHhf7kqYLe-j8MolRMc1k_Mkm4Omo_CAqO-akXulpdxcXu-OqVevjMRQq1B3OIIB0Am9h-ymckOKU_oK59BpnKKqBFjfJWlxt7)

### Retrieving specific data from a record
When using the get() method to retrieve a specific record, we can extract the information for a defined field using the new instance created while searching for the record. In the following example, we create a new instance called “record” for the FruitsInfo class where the “id” field is equal to “3”. Then we extract the information of each field.

  
```python
record = FruitsInfo.objects.get(id=3)  
print(record)  
  
print(record.name)  
print(record.origin)  
print(record.price)  
print(record.availability)
```
  
**RESULTS**
![](https://lh4.googleusercontent.com/5si9PY5yWYwNSwQN3Le1-UcQ5ape6yrP-TxpFkArNjMTLuwhNxpq6hkRTVMYFA7KCNzdCVByRIa8b0BcWjsovQRQI1SE2e3oj2_WKh99fgRCSDTbW3KSK2pAV_kvxHGZTRiEP4ZL)

Let us create a custom print statement using each field in the record

```python
print(f"The stock of {record.name} which originates from {record.origin.title()} is at {record.availability} and each {record.name} is priced at {record.price}.")
```

**RESULT**
![](https://lh3.googleusercontent.com/8BYHTRJdOMdd_NWgl5rrAD9ENjf2Lm_531Aj1qRLK2wyM0wZUPG02uMQv1-rx4gntZx8Lq4v33FqfNkUGovgc5jmBvqt-jiva1sIm2NOfI-z3RYdnNfREU6vEw3GgNEyj55QZfCW)

## Field Lookups
In Django Object-Relational mapper, we can specify operators to further filter out the resulting dataset. This is analogous to the operators that can be specified within a SQL WHERE statement. Some example field lookups and their corresponding SQL operators are;

-   contains - LIKE
-   range - BETWEEN
-   gte (greater than or equal to) - >=
-   lte (less than or equal to) - <=

The following examples demonstrate how we can use the Field lookups from within the Django Shell

### contains operator
Let us search for vendor names that include the name “Fruit” in the FruitsVendors class.

```python
from fruits.models import FruitsVendors  
FruitsVendors.objects.filter(vendor_name__contains='Fruit')
```
  
**RESULT**
![](https://lh6.googleusercontent.com/3GyXF2ZKhix_gq932yr0sFbbQBkW2xUe73iA-sN6rCfqhglwaj1S92tkfveaVXNZjKvjYgGgHu1AzlbaOWORVCtsYRgE39JcmYhkaACvyN8i84Lo0UBwAT4zrvvTukL1F-4aMVJt)

### gte and lte operators
In the following examples, we will search for records where the price is greater than or equal to 2 and where the availability is less than or equal to 1000 in the FruitsInfo class.

```python
from fruits.models import FruitsInfo  
FruitsInfo.objects.filter(price__gte=2)
```
  
**RESULT**
![](https://lh6.googleusercontent.com/itOxU3nE-LXmtuY9E9an-hyQZayPzbyybvBboV-2oIdvjSbSwNgs-q8aWPU4ms4D-EhKGMamskpGAqgeuzxR7uOqsj4J74qn92fSI57oWUP8sSw0-N91855ghEyystD3kOFs1san)

  
```python
from fruits.models import FruitsInfo  
FruitsInfo.objects.filter(availability__lte=1000)
```

**RESULT**
![](https://lh4.googleusercontent.com/APx-92XctgvVN6Mxgxx6kNik4IJsJzV7vHUGDO6Lc_HIf4oitXHNaWlfu8W9daSOwNueL58dDZv29yvd8zi0xuPzv9nYzbdp5fQJgJx_03NFcURdghZeERlnPWIu294osoEw7zi_)

## Updating Records
The Object Manager provides a method called update() to update a single record or multiple records. When a successful update is done, the output will be the number of affected records within the database. The update() method is analogous to the UPDATE statement in SQL.

The following examples demonstrate how the update() method can be utilized.

### Updating a Single Value
The update operation can be done along with a filter() method to specify the record that needs to be updated. Let us update the origin of the apples (id=1) in the FruitsInfo table.

```python
from fruits.models import FruitsInfo  
record = FruitsInfo.objects.get(id=1)  
print(record.origin)  
  
FruitsInfo.objects.filter(id=1).update(origin='australia')  
  
record = FruitsInfo.objects.get(id=1)  
print(record.origin)
```
  
**RESULT**
![](https://lh6.googleusercontent.com/uB90R1mdjEwav7CBMY6L7ZQEpkW8QwQ5ClEbDoP_LnNNEkJ07g3Ci5bTfX2jmpULbYEa64_PZ8YftEMS-1n_D_skVNLxkgYCtM3JBeyUggJTCerDZZk72qgopGsPHKIFqDU6C_vM)

From the above code block, we first check for the original value of the origin field of the record. Then we update the origin to “australia” and finally verify the update operation by calling the origin field using the get() method. As we have only updated a single record, the update operation outputs the number of records affected which is one.

### Updating Multiple Values
In this section, we will take a look at how to update multiple fields within a record. To demonstrate this, we will be updating the price and availability field in the kiwi (id=4) record.

```python
record = FruitsInfo.objects.get(id=4)  
print(f"Price = {record.price}, Availability = {record.availability}")  
  
FruitsInfo.objects.filter(id=4).update(price=0.55, availability=5000)  
  
record = FruitsInfo.objects.get(id=4)  
print(f"Price = {record.price}, Availability = {record.availability}")
```

**RESULT**
![](https://lh5.googleusercontent.com/WtVVtxYlBFQJFOgofQcZMY-RUR1AQv4196Az0PgGosPIc_mtDkwItVMQQHlJdlkmlXlHf0EispiXJP4RosbaddgWg_poukXvVa4sWDH_w_l7KJh9WlOdmmf69qGokbaEwUYtZAdk)

In the above code block, we have defined multiple fields that need to be updated within the update statement. The output of the update operation still signifies one because we have only updated multiple fields of a single record.

### Updating Multiple Records
When updating multiple records, the main consideration is that the field that undergoes the update operation must be present within all the records. If the field is not available this will result in a FieldDoesNotExist error.

In the next example, we will update the availability field of all the records to 10000. we achieve this by using the update() method without specifying a filter.

```python
FruitsInfo.objects.all().values()  
FruitsInfo.objects.update(availability=10000)  
FruitsInfo.objects.all().values()
```
  
**RESULT**
![](https://lh5.googleusercontent.com/pauJRqkONGu_zGE2p-nBsn97cpu9g3qTp5fU3h9tCKUJdkTIXJMxVAJ_49VQSFAUvED64w53c9CV6FxY2RNNMlkYtVfWD_UFEJKSOlQR6hd3iNDmkFIcfElnClxOKO-P2R-M-i2J)

The output of the update operation shows us that there are four records affected by this update.

## Deleting a Record
Django shell provides the delete() method to delete records from a specified class. This is analogous to the DELETE statement in SQL.

### Deleting a single record
When deleting a single record we must use the get() method as it returns the specified object directly. Let us delete the kiwi (id=4) record from the FruitsInfo class.

```python
FruitsInfo.objects.all().values()  
FruitsInfo.objects.get(id=4).delete()  
FruitsInfo.objects.all().values()
```
  
**RESULT**
![](https://lh4.googleusercontent.com/t9KXKv6ykeyPAvdFt6e9twSzKXn-uJg8Y-Q_pE2mpzzT6mJZ6VBj4KpyWty8nNePzdWToYC-6Uo3ONJyZUWsN87n-A5FHQUUQxzukBIKMer9gLGD3PfaeW5i34o-87PA6YRy0Bo5)

The delete() method also outputs the number of records affected by the delete operation.

### Deleting Multiple Records
The delete() method can be used to delete all the records within a given class by simply specifying the delete operation with the all() method. In the following example, we will delete all the remaining records from the FruitsInfo class.

```python
FruitsInfo.objects.all().values()  
FruitsInfo.objects.all().delete()  
FruitsInfo.objects.all().values()
```
  
**RESULT**
![](https://lh4.googleusercontent.com/PnOU3hS-PxBms_13RsqOzNeKizge_S02RCu9jEhLV0n0pXYZ1A0hGbCDh9NPvQPhl2txt1yaKmzIgtoVE7IfGHnLdv-BR5TDdV4WfT__Dc10XF2xv119TZlGQBqW-Bf7zd-P7X9B)

From the above output, we can identify that the delete operation is carried out on all the remaining three records.

## Conclusion
In this article, we learned how to use the Django Shell to interact with the database using the Django Object Relational Mapper. The Django Shell provides all the functionality of the standard python shell while adding the functionality of the Django framework directly to the shell environment. This enables developers to test and debug database interactions without the need to modify the Django project.
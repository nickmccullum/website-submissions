# How to Customize Django Admin Interface

The Django framework comes with an integrated administration interface to carry out various administrative tasks. Its purpose is to provide developers with a convenient interface to perform CRUD operations on user models and other administrative functionalities like authentication, user permissions, etc. This interface is designed to be used as an internal management tool and not as a frontend tool. The Django project describes the admin interface as below,


“One of the most powerful parts of Django is the automatic admin interface. It reads metadata from your models to provide a quick, model-centric interface where trusted users can manage content on your site.”


One of the best features of this admin interface is the ability to customize the interface according to the developer’s needs. During this article, we will discuss how to customize Django’s admin interface.

## Enabling the Django Admin

First and foremost, you need to enable the Django Admin interface. Then, you need to create a Django project called “VehicleSales” and an app called “salesinfo” with a superuser “admin” to access the Admin interface. There, you will not perform any migrations (makemigrations) as it is the database creation and there are no any user-created objects to be migrated. All the examples presented in this article will be based on a Powershell Terminal in a Windows Environment. However, all the commands are cross-compatible and can be run in any environment.

```python
django-admin startproject VehicleSales  
cd .\VehicleSales\  
python manage.py startapp salesinfo  
python manage.py migrate  
python manage.py createsuperuser
```

**Creating the project and the app**
![](https://lh3.googleusercontent.com/-Tq_Dbsxr-XiTZDtMlijMzNpRrDYLS4Ry6WvwPiod6l2K84sOeiqKsRYD5u_7QIF1pqwT-2Bw0OTXmCXySnmt0w0nziW27HP6w_Uq0uh2zqQ58e-xuo4K7xAUt5ioMp544nZwmnc)


**Creating the user**
It is important to note that access to the Django admin interface is limited to users with superuser or staff attributes.


![](https://lh3.googleusercontent.com/FWN3KskspJUUgb0koj7hTWotHvKfQt3M1voFAlGxv2Fjxn69mJwcm2c9rTokA7uYchpbBRcmyIxaANyoIbP8TFl3vdtcGFtVYVG5JdW1ScvlPkjldeVVMfSG5QJHFNhF8uaXswBv)


The next step is to update the settings file of the project to include the “salesinfo” app. For that, simply add the app name in the INSTALLED_APPS section of the settings file.

  

**VehicleSales/settings.py**
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'salesinfo',
]
```

After that, you have to populate the models to define the database structure. You will be creating three classes: Owner, VehicleSales and VehicleType..

**salesinfo/models.py**
```python
from django.db import models
from django.core.validators import DecimalValidator
 
class Owner(models.Model):
    owner_id = models.CharField(primary_key=True, max_length=30)
    first_name = models.CharField(max_length=50, null=False)
    last_name = models.CharField(max_length=50, null=False)
    invoice = models.ManyToManyField("VehicleSale", blank=True)
 
    class Meta:
        verbose_name_plural = "Owners"
        db_table = "Owner"
 
    def __str__(self):
            return f"{self.first_name} {self.last_name}"
 
class VehicleSale(models.Model):
    invoice_id = models.CharField(primary_key=True, max_length=30)
    date = models.DateField()
    vehicletype = models.ForeignKey('VehicleType', verbose_name='VehicleTypes', on_delete=models.PROTECT)
 
    class Meta:
        verbose_name_plural = "VehicleSales"
        db_table = "VehicleSales"
        ordering = ("invoice_id",)
    
    def __str__(self):
            return f"Invoice - {self.invoice_id} - {self.date}"
 
class VehicleType(models.Model):
    make = models.CharField(max_length=60)
    model = models.CharField(max_length=150)
    year = models.IntegerField()
    color = models.CharField(default='Unknown', max_length=50)
    price = models.DecimalField(null=False , decimal_places=2, max_digits=10, validators=[DecimalValidator(10, 2)])
    description = models.TextField(null=True)
 
    class Meta:
        verbose_name_plural = "VehicleTypes"
        db_table = "VehicleType"
 
    def __str__(self):
            return f"{self.make} {self.model}"
```
  

You have defined the db_table name option in the Meta class to indicate the names of the tables that will be created in the database. Then you should add the above models to the Django Admin interface by importing them as shown below.

**salesinfo/admin.py**
```python
from django.contrib import admin
from salesinfo.models import Owner, VehicleSale, VehicleType
 
@admin.register(Owner)
class OwnerAdmin(admin.ModelAdmin):
    pass
 
@admin.register(VehicleSale)
class VehicleSales(admin.ModelAdmin):
    pass
 
@admin.register(VehicleType)
class VehicleType(admin.ModelAdmin):
    pass
```

In the above example, the ModelAdmin class is used to represent the model in the admin interface while the register decorator is used to register the ModelAdmin classes for each model. You can also use the admin.site.register(<ModelName>) instead of the register decorator to register the model.

The last step of configuring the admin interface is to migrate the changes and start up the server.

```python
python manage.py makemigrations  
python manage.py migrate
```
**Make Migrations**
![](https://lh3.googleusercontent.com/XKTRQ294-cI-Z-W_ZKHqEcYU7Q_2WoO6dSdngwXzk2n0qc1NK9_w0henyueRGsBCRBCl7revpMR5XVFM-leDObTN6Te8Mp-DS_I-nKKBULqEOnkQ1hZqOKNCkDnvtqFTG2Yo7GdP)
 

Once the migrations are done, start the Django server and access the Admin interface by visiting [http://127.0.0.1/8000/admin](http://127.0.0.1/8000/admin) in your browser.
```python
python manage.py runserver
```

**Start the Server**
![](https://lh4.googleusercontent.com/Y3q31e68T7Hp6n5J2kK1H-AnC_xNC6lnCeSSPKIGeNBQ68Q1aAzX2DzD9z_PhjN-z_B0xTWSC1er-PAfY2VuQdadgs8mgNXsmcN_duQp3_4SRZjNaLBf-0Zq_O7tWGcTuC6v1B3M)

  

**Django Admin Interface**
![](https://lh3.googleusercontent.com/h9zf--cw3C19uK9f17aUNggtV9fSlsEUu-cEBcRVeCdvK7y-GF47WWtJfL4fCxl3xsMwaBr3SJulTbTRS5d6c_vlIXBgbYV-19axVh3ZuCWMRKe6m-_96jcPyNxXHPPJUWdOfQ5D)
 

Now you have configured a basic Django Admin interface with all the user models bound to it. Before moving into customizations of Admin interface, let’s add some data to the models. First, you can add data to the simplest model which is the VehicleTypes. For that, Click on the VehicleTypes, then click on “ADD VEHICLE TYPE” and fill the information in the correct fields. Repeat the same process for other models as well.

![](https://lh5.googleusercontent.com/kiN6Nr8oxEp9tl-zGagtaU6pc1WhIsoef-YToXN4hquMxb7XPCuMqKEngSA7tAzrFV3kosxS33UKzfsao4bfdgh0MGwyhL5MoyAv1dcrJs_WMR565Nx8R2eOT0WQarxQPChYWZ3q)

  
  

**VehicleTypes**
The (\__str__(self)) method will be used to display the name of each object.
![](https://lh4.googleusercontent.com/o4EiARTrYmp-z3rktNevUAOi6kfp0Hk7QuxsXg3aszf4RTu7tn0gTyyFSP0nPAyf7umR8dZ5YReJ85g_zSJV6WCAEsXZW7_1KWm1oztqQaFkH-yHxOK_g5tauTjoNreIl2cpEdNk)
 

**VehicleSales**
![](https://lh6.googleusercontent.com/kBY0WZH_GV1ry9u_Od7o_o-vFFoEZpOqe8p7XvYVgyyHHrwAv4aLfmP5ULy_EwlRAXxOLzcLT1tvVNqPty7TS4MqDswAmNTnFNwN7Kv9n2CMIwbX37fAtAufspzkcJ8RdvghAkWU)
 

**Owners**
![](https://lh3.googleusercontent.com/YCs6JLIJPlX8_A6VL1steU0GkCFyKQlpIZ0AvWIa-O78FBLVnQjLBFqRyHlvUY1a5xPL1rqDNpW2AJremh97coBdsyv27xavnHIevqgziuP_9mQwV315MVWzGJRcaWK_COD5zraJ)

Now, you have a complete set of data that can be used to learn about how to customize the Django Admin interface in the next section.


## Admin Interface Customization

  

The Django admin interface offers various customization options and even allows to create separate admin interfaces that enable user separation using permissions. Most of the customizations can be done using the ModelAdmin class that acts as the representation of a model in the administration interface. You can even change the look and feel of the interface by using the Django template engine.


Through the following section, you will learn how to change the functionality of the Admin Interface using the ModelAdmin class.

### Changing the List View

In Django,  if the (\__str__) method is implemented by default, it will be taken as the raw name. This string representation method is the default method for drop-downs and multi-selections. The following examples illustrate different ways of changing the admin interface.

Using the list_display attribute, you can define which fields should be displayed. This attribute should be defined as a tuple even if there is a single element.
 
```python
from django.contrib import admin
from salesinfo.models import Owner, VehicleSale, VehicleType
 
@admin.register(Owner)
class OwnerAdmin(admin.ModelAdmin):
    list_display = ("owner_id", "first_name", "last_name")
```

The above code block will change the Owner list to display all the defined fields.

![](https://lh5.googleusercontent.com/8n9OaOVyn08COYPNF2TkaDkCPno_9KdT3JuAAvO_uoNTWs17h2KlcFtLTALkdfV0xL4j-RWdXtb7kspv_RD9Thgb6e8dUvtOFWI_PoSJjAKM-KaJ_AIp4wQqZelCK_jm8h-ZcTpH)


You can change the order of the Owners list by defining the ordering attribute in the Meta subclass of the Owner Model class or simply within the admin module.

**salesinfo/model.py**
```python
class Owner(models.Model):
    owner_id = models.CharField(primary_key=True, max_length=30)
    first_name = models.TextField(max_length=50, null=False)
    last_name = models.TextField(max_length=50, null=False)
    invoice = models.ManyToManyField("VehicleSale", blank=True)
 
    class Meta:
        verbose_name_plural = "Owners"
        db_table = "Owner"
        ordering = ("first_name", "last_name")
```
  

**salesinfo/admin.py**
```python
@admin.register(Owner)
class OwnerAdmin(admin.ModelAdmin):
    list_display = ("owner_id", "first_name", "last_name", "get_no_sales")
    ordering = ("first_name", "last_name")
```
  
  

The above code will arrange the order of the Owners list first by first_name and then by the last_name as shown in the below result. In the table, the order in which the items have been arranged is indicated at the top right corner of the ordered column.


![](https://lh3.googleusercontent.com/XWEC24wNHa6oUa9P3oneC5JVVcbbAFEQi2_ZysPge17OIr_wTCI7RkzPnjM6e2M05ruqj3hWXITr0ZVMFNgHhKy61NWIU6JA1POff56xicYj4FSv7RpeSM89SnpfxuxjM95efmTM)


Now, let's modify the above code further by adding a custom field to indicate the number of sales for each owner. You can create a custom function called get_no_sales to retrieve the count of records associated with the specific owner object

```python
@admin.register(Owner)
class OwnerAdmin(admin.ModelAdmin):
    list_display = ("owner_id", "first_name", "last_name", "get_no_sales")
 
    def get_no_sales(self, obj):
        no_of_sales = VehicleSale.objects.filter(owner=obj).count()
        return no_of_sales
    get_no_sales.short_description = "No of Sales"
```
  

**RESULT**
![](https://lh5.googleusercontent.com/2umQUXVnecpHer3zSM6rQB1M8ZKEen0VHR_2KHjeIdj5E464mSshaIbzbj_aF6OztTvc2n7igltadQ4RQgbLxCzoT1k8-SB_z7fqz6_dw1SVoD-r9O0H0Q5A4zo6lVRLvmDiZZm7)


### Combining Data from Other Models using a Foreign Key

In case if there is a Foreign Key, you can call upon that field (Foreign Key) as an object to get other fields of that model. In the below code block, the Foreign Key field is called and it will return the string representation of the object. Then, the price field can be called by using that Foreign Key field as an object.

To achieve this, you have to create a new function called get_price and return the price field as price_total and assign the function to the list_display attribute. Additionally, you can define the short_description attribute to the function so that it will display it as the header of the column.

```python
@admin.register(VehicleSale)
class VehicleSales(admin.ModelAdmin):
    list_display = ('invoice_id', 'date', 'vehicletype', 'get_price')
 
    def get_price(self, obj):
        price_total = obj.vehicletype.price
        return price_total
    get_price.short_description = "Total Price"
```

**RESULT**
![](https://lh4.googleusercontent.com/XFSllTzQCGHDZ5nhsLdKlKwGM_bYF7LUyjnR85S5StdG7SWgfQylftmYn47YO-QKr8ilLFxhXWQAazbziDGiVnbauZ9eunKW77B1Oub4_llMgRUsbp6c349_a6gq6va2U8CfSw5m)


### Linking Objects

Through the Django Admin interface, you can create links to other objects using a Foreign Key relationship. That can be done by using the reverse() and urlencode() methods. The following code block shows how to link the corresponding sales invoice with the vehicle type.
 
```python
from django.contrib import admin
from django.urls import reverse
from django.utils.http import urlencode
from django.utils.html import format_html
from salesinfo.models import Owner, VehicleSale, VehicleType
 
@admin.register(VehicleSale)
class VehicleSales(admin.ModelAdmin):
    list_display = ("invoice_id", "date", "get_vehicle_details", "get_price")
 
    def get_price(self, obj):
        price_total = obj.vehicletype.price
        return price_total
    get_price.short_description = "Total Price"
 
    def get_vehicle_details(self, obj):
        link = (
            reverse("admin:salesinfo_vehicletype_changelist")  + "?" + urlencode({"id": obj.vehicletype.id})
        )
        return format_html('<b><a href="{}">{}</a></b>', link, obj.vehicletype)
    get_vehicle_details.short_description = "Vehicle Type"
 
@admin.register(VehicleType)
class VehicleType(admin.ModelAdmin):
    list_display = ("make", "model", "year", "color", 'price')
```
  

In the above example, there is a new method called “get_vehicle_details” and it is using the reverse() function to point to the relevant admin page. You can define the reverse function URL as below.

```python
admin: <app>_<model>_<URL name>
```

The model name must be in lowercase. You can refer the official Django documentation for more information about [django.urls module](https://docs.djangoproject.com/en/3.1/ref/urlresolvers/). Then, adding a query string to the end of the URL will point to the relevant object using the object id (obj.vehicletype.id). This will create a URL that is equivalent to: **admin: <app>_<model>_<URL name>/?<id_field>=<id>** and which points to the linked object. Finally, the complete URL will be returned as an HTML link using the format_html command with the object’s string representation as to the URL name.


In addition to the above changes, you can expose all the fields in the Vehicle Type model to be displayed in the admin interface using the list_display attribute.


**Linked Vehicle Sales**
![](https://lh5.googleusercontent.com/qmgDRG9woNGx04bY4HXQut-vzAgwQUdXAFAyJDHtqsZlgmGGxcTegoWrS9di9YaXcYuLyrO4h4h8gCbellHQ7ii8VwxjnuwimRECcxwQXxbM1FES4TBI4RFyvF4rGye6tiP0BNS8)

**Linked Object**
![](https://lh4.googleusercontent.com/X2G5ydqKMFfJniH_7O9swCJubsi1hoZ7CwGRIHeLUA-llJKm42ff9Q3Qbf9IxETi-t6RtlfVeGgDXpOSozekEOXkKeMDgM-rksdvRYzqfYp_mfaq9TepXP0IhNKbihH2GpyAbV4Z)


### Adding Filters

Django's built-in filter widget allows you to filter data according to the specified field. This is done using the list_filter attribute and it should also be defined as a tuple. Let us add a filter to the VehicleTypes object to filter results by year.
 
```python
@admin.register(VehicleType)
class VehicleType(admin.ModelAdmin):
    list_display = ("make", "model", "year", "color", 'price')
    list_filter = ("year",)
```

**RESULT**
![](https://lh6.googleusercontent.com/3WxiA94KzkTptXBMjK77YeS8uaZU-4IcxffpOjB3Y1J3XYOtmSsQI-wSnnAvg_j4jtVZCsDnPqYZvVxIKoF64Ui40FmokMJRwkhSEx0OV8G78-hb1ultikWWJWO0QJDGxnzmomVx)


### Adding a Search Field

Django supports adding search fields in the Admin interface using the search_fields attribute. When defining a search field, it should be defined as a tuple or a list and can be extended using modifiers. Let's add a search field to search vehicles by make.

```python
@admin.register(VehicleType)
class VehicleType(admin.ModelAdmin):
    list_display = ("make", "model", "year", "color", 'price')
    list_filter = ("year",)
    search_fields = ["make"]
```

The following screenshot shows how to search for any make that contains the letters ‘au’ anywhere in the make field value of each item. This is equivalent to **%au%** search in SQL.

![](https://lh5.googleusercontent.com/oVom0OVLopLsStmlig1iv54us2-vudIm9ZgoSCdAmkHuO5rK86OBn7-nz7vwW2uOuxX01eVAsDgJLZBpa-Du5I_L1zA3wLloiOrQmavw7y1oKL3gsZQ__V8ZCzDovoUu5RTgPRzp)

You can also define multiple fields in the search_field attribute and it will result in searches that contain results from all the defined fields.

```python
@admin.register(VehicleType)
class VehicleType(admin.ModelAdmin):
    list_display = ("make", "model", "year", "color", 'price')
    list_filter = ("year",)
    search_fields = ["make", "model"]
```

The following search will look for “5” in both make and model fields. This is equal to an OR condition as it will perform the search as **make = %5% OR model = %5%**.


![](https://lh3.googleusercontent.com/xkyZ1cXmsl9Y0IgbtEBzIdC1_JUM1lUqLBp6AqQWzQdCTwb3j4Fp4n2Bq6m_d77Jx2Wpvx4VbI1frc09vMVsRupmDYBvA2FQ85-y8_yux-Xsglp5rQbc1pLpRrB9AiJ4GyqcTjt7)


### Modifying the Add and Edit Interfaces

The fields in forms can be modified using the fields attribute or the fieldsets attribute. The fields attribute lets users rearrange, group, or hide fields within the form. In order to demonstrate this functionality, let's change the order of the fields and hide the description field from the add Vehicle Type form. The field will be defined according to the order given in the fields list.

```python
@admin.register(VehicleType)
class VehicleType(admin.ModelAdmin):
    list_display = ("make", "model", "year", "color", "price")
    list_filter = ("year",)
    search_fields = ["make", "model"]
 
    fields = ["make", "model", "color", "price", "year"]
```

**Before Modifications**
![](https://lh5.googleusercontent.com/Eq-ZO9dN7S2q_JA50oW3hSsK73KzdZzyiG-oeOp3m0i7MtLY8gxmvXiMmJEliVcBHHtSBKsjxgAJut2dJrh_YQvMw3lKbicBju-NdOcPI1Yw7ZdnXsZ5WoU4UndzOvtCNaR8X89X)

**After Modifications**
![](https://lh5.googleusercontent.com/-fz2E7Zop3j3cmJDZqT_hehdq1X3Rom6pagoabMoTDKb6OENfFd8qiW0Jo8DP1uOSF5M7XwHUT3O8nXJzaCtvrlnqJERalgRm0lfM6tcInhJZbiPj3Ji3Hk93OKPdtDN-1sV850t)
 

The Fieldset attribute can be considered as an advanced version of the fields attribute. It enables users to create sections within forms. In the following example, the description field is moved into a new section.

```python
@admin.register(VehicleType)
class VehicleType(admin.ModelAdmin):
    list_display = ("make", "model", "year", "color", "price")
    list_filter = ("year",)
    search_fields = ["make", "model"]
    ordering = ("make", "model")
    fieldsets = (
        (
            "Required Information", {
                # Section Description
                "description" : "Enter the vehicle information",
                # Group Make and Model
                "fields": (("make", "model"), "color", "price", "year")
            }
        ),
        (
            "Additional Information", {
                # Section Description
                "description" : "Enter any additional information",
                #Enable a Collapsible Section
                "classes": ("collapse",), 
                "fields": ("description",)
            }
        )
    )
```

**Modified Interface**
![](https://lh3.googleusercontent.com/NE0_L4yIhSHr7Tf81FoEVg3Qxi2o7W3F3aoh9Rx9Gx0qcXS2EnX3tUSNKwASNoZjztDvwv5AioN_jeDi1IWp3ySJkeaTcmuc9_gCUI24SkLvuRn_-bsoMmYE0Weep0irpETp8Q7d)


## Conclusion

Django offers a whole set of customization options even though we have only scratched the surface of it within this article. Here, we mainly discussed how to customize Django administration interface using the ModelAdmin class. On top of that, you will also gain a proper knowledge on how to modify the way data is presented, add search, filtering, and ordering options, changing form fields and the way they are represented by referring to this article.

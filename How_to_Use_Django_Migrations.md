# How to Use Django Migrations

## What are Django Migrations?
In Django, whenever a model is created, updated, or deleted, a new migration will be used to propagate the changes to the given database schema.

Django framework has built-in support to interact with relational databases such as MySQL, PostgreSQL, or SQLite. Django allows us to interact with these databases without needing to write SQL queries. This is done using the object-relational mapper or ORM. The object-relational mapper provides the functionality to write Django models, where each defined database field will get mapped to the corresponding field in the database without the need for using SQL queries.

When a model is defined, migrations come into play to commit these changes to the database.

**Migrations Commands**

Django comes with several migration commands to interact with the database schema.

-   **migrate** - used for applying and removing migrations.
-   **makemigrations** - create new migrations based on changes made to models.
-   **sqlmigrate** - displays SQL statements for a given migration.
-   **showmigrations** - lists projects migrations and their status.
    

Migrations can be considered as a version control system for the database of the application. While `makemigrations` command packages the change made to models into individual migrations files and the migrate command is used to apply the packaged migrations into the database.

Django makes migrations for any changes done to the applications models or fields even if the change does not affect the database. The reason for that is having all the historical data relating to the specific model or fields allows accurate reconstructing of data. The migration files of each application reside in a “migrations” directory. Migrations are designed to be committed to and distributed as a part of the codebase. Using migrations allows the users to produce a consistent dataset from development to production environments.


## How to Use Migrations
In this section, we will look at how to use migrations in a Django web application. First, let us create a simple project called “vehicle_sales” where two applications capture the current prices and historical prices of the vehicles called “vehicle_sales” and “vehical_sales_history” respectively.

All the examples provided below are done using PowerShell in a Windows environment. However, all Django based commands are interoperable irrespective of the operating system used.

### Creating and Configuring the Project and Applications

```python
django-admin startproject "vehicle_sales"
```
  
![](https://lh4.googleusercontent.com/ZaTSMsyS_YBLpUbKUx2T-4A87Xtnlqh-ruHH6BI50ti_VY3w6qSeRpHEpfDC7YvujoINgcElfSSiUIX0jLjs4GEATUPZvdlZqd57zx6iBkUtfjGZt73fCZjUsiOf7X1ffBV0wEdc)

  
  
```python
python manage.py startapp vehicle_sales_history
```
  
![](https://lh4.googleusercontent.com/dBFvJUsnVWve8tWHfxqOzOi3RLKTY0cMV26BWgqqMi0kaMulXHjtFX2yUcPCB5viiMQMsG0M0749CRGmiDBYWl-pHw2h_S3jTyFpaxMrHYuyfz1BfJTG87xtRTos15oSc4oDcc9f)

  
Let us look at the folder structure of the project before any migration files are made. The tree command is used to obtain a formatted output in PowerShell.

```powershell
Get-ChildItem | tree /F
```
Linux users can use the following command

```bash
ls | tree
```
  
**RESULT**
![](https://lh5.googleusercontent.com/ftaN9OAQM5B5__y5QBnJAs26hEuECCB-S1q408YlnTLpB76RSLC0OZNbqQKQCV5uIJ8CXrCFzIkmuZHmC8RGd2-Jnb5rOZ5ytCqH_djwzFF_oMFOdnRmo01P51u_tzoE0DaRcF80)

  
### Populating the Model

The “vehicle_sales_history” application model must be created before we can use migrations. we will create the following model and add the application to the INSTALLED_APPS in the main settings.py file.
 
```powershell
.\vehicle_sales_history\models.py
```

```python
from django.db import models
 
class SalesPriceHistory(models.Model):
    date = models.DateTimeField(auto_now_add=True)
    make = models.CharField(max_length=60)
    model = models.CharField(max_length=60)
    price = models.DecimalField(null=False , decimal_places=2, max_digits=10)
```
     
```powershell
.\vehicle_sales\settings.py
```

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'vehicle_sales_history',
]
```
  
Before making migrations, let us check the Model for Errors using the “check” command. The check command checks all the files within the Django project for common errors and we can specify which category to check by using the -tag attribute.

  
**Check the complete Django project**

```python
python manage.py check
```

**Only check the models within the Django project**

```python
python manage.py check --tag models
```
  
**RESULT**
![](https://lh4.googleusercontent.com/DvL-S-Qjo7anYRBHApuKviJ4eXY0xiJfKZv45hGnbDzFY4lVi9DxmTI-BZhJBZJwMYwc1wftJc-qGvOZJ8Ndp36zgR-YGRaqeLRU-hQYwccjpXefCFGpgswmAkPKHBaFnSPeXvWD)

  
### Initial Migration

#### Using makemigrations command
Let us look at how to make the first migration so the changes that were done to the model file will be reflected in the database. In this instance, the database will be a simple SQLite database created by default by Django.

```python
python manage.py makemigrations vehicle_sales_history
```

**RESULT**  
![](https://lh3.googleusercontent.com/PE8hnJ6mzdJjW8S1MhrfKjQwpzbXhHAgAOLRog9i0oZ6yzN3dyQdGmKSAkBf7Usg0Mc1MOkf3B_zRAc84EoQe3ieB1jvNH98JJJbDCV6_JQ1HPe9qHJJNDxzPKDVBMGFXFLt0jB7)

Now, let us look at the folder structure of the project to identify the newly created migrations file

![](https://lh4.googleusercontent.com/-sd_J3a3rchmL4bejZq4AyGkZXWKKcoP_HUzxfpBDpSP6qDjEf7PdyM49J7YyRIgFdZwguMhiIMSlaLbLY-yzpY05hf824rEkfxGGr-6Ez1kgnnWfUzzeZpEvUPtj6JjXtiO8HUv)

We can identify that a new migration file called “0001_initial.py” has been created inside the migrations folder. This is the file that will be used to create the initial table structure in the database. The “db.sqlite3” is the default simple database created by Django. When a user tries to access a non-existent SQLite database file, Django will automatically create an SQLite database. This behavior is unique to SQLite before using any other backend database like PostgreSQL or MySQL a new database must be created manually.

**0001_initial.py**

You would have noticed in the migration file there is an additional field called “id” that has been defined. It's created as the primary key field in the migration file automatically becuase we have not defined a primary key in the model.py file. A primary key field can be simply defined by adding the parameter (primary_key=True) to the desired field.

```python
from django.db import migrations, models
 
 
class Migration(migrations.Migration):
 
    initial = True
 
    dependencies = [
    ]
 
    operations = [
        migrations.CreateModel(
            name='SalesPriceHistory',
            fields=[
                ('id', models.AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('date', models.DateTimeField(auto_now_add=True)),
                ('make', models.CharField(max_length=60)),
                ('model', models.CharField(max_length=60)),
                ('price', models.DecimalField(decimal_places=2, max_digits=10)),
            ],
        ),
    ]
```
  
  

We have used the makemigrations command to create migrations however the changes will not be reflected in the database until we apply the migrations using the migrate command.

#### Using migrate command

Before applying the migrations, let us explore the SQLite database to check if there are any tables created. We will be using the Django dbshell management command to access the default SQLite database.
 
```python
python manage.py dbshell
```

**RESULT**  

![](https://lh4.googleusercontent.com/K7slPlIp8_A5BWggLbmHNKIN221fsZlFkEi-hR1x4RzXI2Mfftdo1rjgkugd1A2EY6G3KXIXPVKtVqCFRq6iSvxF2HaUhow7QJBxHUsKISZupcdpw2__y4m8OEbFl9gBD3eaRMNY)

When we check for tables using the “.tables” command nothing returns as output so we can assume that there are no tables in the SQLite database.

The sqlmigrate command can be used to identify the SQL queries which will be written to the database without applying the changes. The sqlmigrate command requires two mandatory arguments, the name of the app and the migration name.

```python
python manage.py sqlmigrate vehicle_sales_history 0001_initial
```

**RESULT**  
![](https://lh6.googleusercontent.com/9G73ZVrRkARqujBMDI82Lp1u_WJi8fiq-v5FJ-8Fo_JAMfLlMyUNT4tbW5HhvFktLI4p9DjTEe0Vc1ID0nN9s7zn5ahXruhMwsq2cCDhcDadIHx6L1ERKsUwRxNIkhtFg27l4Fnc)

Let us now apply the migrations using the migrate command. When the migrate command is called, it will apply the migrations from both the user-defined migration files and system migrations. 

```python
python manage.py migrate
```
  
**RESULT**
![](https://lh4.googleusercontent.com/P_fS_fzwLhea3ZqUPbhJJQBairtvlhIUA1WTQUp6-xQrMt3LKthXU27ef-xFUSktdgl4eYO2VmKE1US3PTCT_bFBMDkaJj8zxvKmO_A_nZ_aPf5fkkGQsFD0VrsbgXWXEtbjHKas)

After a successful migration operation, we will look at the SQLite database to verify if the migrations are successfully applied.

  
```python
python manage.py dbshell
```
  
```python
.tables
```

**RESULT**
![](https://lh4.googleusercontent.com/Uv5YpH2o5jwf8k-isyyGDZ2mxsI3u3jyihqTAXiP2q2oOj7gpbLkC5iwCc1mRUvMZ3F6pJvtoJMJBGB7VfQaJlZ1Dwbhf9fz5xkgSU5cFWIMrbbAA5bOLDaNEClcLuk-kIGqIi8n)

From the above output, we can identify that both the user-defined and system tables are successfully created within the database. The user-created 'SalesPriceHistory' model is created as ‘vehicle_sales_history_salespricehistory’. Let us look at the structure of the table to verify if the fields are correctly defined. The “--indent” parameter is used to obtain a formatted output.

```python
.schema --indent vehicle_sales_history_salespricehistory
```
  
**RESULT**
![](https://lh5.googleusercontent.com/tU47EmB_T7ZIZ69iHzAscpyceGQZwL-toL3mrzYpghxAPJig0gItg16IOJ4NdbasivaB68_0aML5LYX5jmK3vgs0XdNZW06FMHki0m0mNzLHL3HTegdHMJRBSeKkp4hSt-2G6pE1)

Migrations will only get applied if there are changes found in the models. When there are no migrations to apply, the makemigrations or migration commands will not act.

**makemigrations command**

![](https://lh5.googleusercontent.com/VLl9naBAf6JC713eNljZ43YxHRekR6MvB0gl7MTSrd71O6Pa5ZncsPodPbtE9PRpFsQHiRNvqXGSgkpA_1VcSfLosRcM5T7EUpil6Bug0fJzxBypoSKbx2LRkT0EfdKdAizC77Z1)

**migrations command**

![](https://lh4.googleusercontent.com/KiRAO9Y_2w-Q03ETk7Qp9X_c08SFlJmSTGU9NakNfUx0xVBmFKbeAKLRC5z2e33UcWWEmVokT-aMjucwz9Q81spOS1yC2Ubv8bvPtkyge8yxobAqvSTBZaL7KJ823w1P_kgqkvwA)

  

### Subsequent Migrations
Let us have a look at how modifying the models reflect in migrations. When a model changes, the database table must be changed according to the changes done to the model. However, if the model definitions are different from the current database schema, this will result in a django.db.utils.OperationalError.

In the vehicle_sales_history model, we will be changing the “model” CharField to a TextField and add a new field called color with the default value “Unknown”.

  
```python
.\vehicle_sales_history\models.py
```
```python
from django.db import models
 
class SalesPriceHistory(models.Model):
    date = models.DateTimeField(auto_now_add=True)
    make = models.CharField(max_length=60)
    model = models.TextField()
    price = models.DecimalField(null=False , decimal_places=2, max_digits=10)
    color = models.CharField(default='Unknown', max_length=50)
```
  
When the “makemigration” command is called, the subsequent migration files will be created with the current time of the system attached to the file name. Using the --dry-run operator, we can identify what changes will be made to the new migration file before creating the migration file.

  
```python
python manage.py makemigrations --dry-run
```
  

**RESULT**
![](https://lh3.googleusercontent.com/b7G1qPV0_PiP0LriaK6GWR2lTHenFhoRrUTSw7T97MqAJAb1vJH6xIC7mPZdRtN4AqVosZNkL0jlN627OKsjjROQz8Zl5UOaDnQe0QNrlvL_QIyQydejXUkxNxmsajoYEW9_Mn4u)

  
  
```python
python manage.py makemigrations
```
  

**RESULT**
![](https://lh5.googleusercontent.com/v4AC862kAAgi0fzNhmoK6PbKn8_TiokwjYTCwFFM2EFQ2v5w0jR7AFsrL5VoK6463fLFc3D9x2kTyZnxwqo0MvHqDOEtxLzxk4vtr-yKy7yJIp0lhkLdr3xWbocvy-MiazK-Cq19)

  
The makemigrations command will create a new file called **0002_auto_20201205_0500.py** within the migrations directory.

![](https://lh5.googleusercontent.com/492iyjamnh5RaQE3RXMbCeSO98konTMFq_L9yUhTm6BtRPFGhMnlE8mTqvjeaA_237SWnodupL4A6xu_IpqqPBi7MxVLGlQ-5eiIBKyB-AfPggkBW2tjET5j8l075HV3h_somYgJ)

  
Using the migrate command, we apply the changes to the SQLite database and validate the changes by exploring the database from the Django shell. The sqlmigrate command will print out the SQL commands that will be executed within the database. Note that the command can be executed without using the full name of the migration file. In this instance, the first four digits of the file name are used.

  
```python
python manage.py sqlmigrate vehicle_sales_history 0002
```
  

**RESULT**
![](https://lh6.googleusercontent.com/eHn8sSTmvu8o-QPWd8l4bROF8s5qisNBK8mxHqTKPU8mHvzEsOMjXOG768mKabknbH_g9zoxhY06grMD3mfCcfzmGeuvpwOQu99csgK-Fc-HfVKS35w3Tsrg_APAb1F1lE2q_gvI)

  
  
```python
python manage.py migrate
```
  

**RESULT**
![](https://lh4.googleusercontent.com/32JaJNYQ86sKJAePdn7D6KWkjV6LjtNsTXeKTYEOYzWCW3XOIduDI1_51TO4ma2cKgH_l7a7Hfn-tATRZVPBHi153PuZOEgOE8j8qUtw3rkWjolaXJmLH5tYkmkCmKZGepmVT5uo)

  

#### Verifying the database

```python
python manage.py dbshell
```
  
```python
.schema --indent vehicle_sales_history_salespricehistory
```
  
**RESULT**

![](https://lh3.googleusercontent.com/U7S1iZ0aCyeh1vXs4bcRz33_q4wQHogoN_S83KnDwb8wVMzYRoWrKC_4khLGZCZ0eTv7hRJKzHFWp_jfpq3GLwFGhhn26EKzTB7zGX7aoYGHILPnnb_u5RWCQzgHwFprjpVVw4lY)
 

The above output demonstrates that the changes made to the model file are successfully reflected in the database. The “model” field has been converted to a text field while the new “color” field has been added to the database.
  

### Listing Migrations
The showmigrations command is designed to provide a detailed overview of the migrations within all the apps associated with the given Django project. If migration is already applied, it will be indicated with an “X” in front of the migration.

```python
python manage.py showmigrations
```
  
**RESULT**
![](https://lh3.googleusercontent.com/ZD8_M-6US6f4aD-YW0kd_btmpov2o4-kBoKqYhDaUffbpXA0haT0TqWEo6s6jFMPYigHkOvbELqcmQVKFBbNonvRycZu2xWxd2CY1qHlPVuCWa631n-6A1Pz5i9qRO4Vskzf775z)

We will modify the model.py file in the “vehicle_sales_history” app to create a new table called “InventoryHistory” and create a migration file and see how it is reflected in the “showmigrations” command before the changes are applied to the database.

  
```python
.\vehicle_sales_history\models.py
```

```python
from django.db import models
 
class SalesPriceHistory(models.Model):
    date = models.DateTimeField(auto_now_add=True)
    make = models.CharField(max_length=60)
    model = models.TextField()
    price = models.DecimalField(null=False , decimal_places=2, max_digits=10)
    color = models.CharField(default='Unknown', max_length=50)
 
class VehicleInventory(models.Model):
    date = models.DateTimeField(auto_now_add=True)
    make = models.CharField(max_length=60)
    model = models.TextField()
    price = models.DecimalField(null=False , decimal_places=2, max_digits=10)
    color = models.CharField(default='Unknown', max_length=50)
    available_inventory = models.IntegerField(default=0)
```
  
We will make the new migration file and using the “showmigrations” command, we see how it is represented in the output.

  
```python
python manage.py makemigrations
```
  

**RESULT**
![](https://lh3.googleusercontent.com/f9xhIJiFd1nnQgqkbHx9NSx_h-SBBbs8YXdqW_EPNjJQIFIwuhR9INpAnk2vcVh2lqGKkOYr6fIHs_TUTfMEGulXYc-wBlcamR4pytr2qhXYHP0aWM-DFmsx2tBrQBlm8iLhQpza)

  
```python
python manage.py showmigrations
```
  
![](https://lh5.googleusercontent.com/THhp_O6uhhHtZJyycHnxb6W1MzqMeVhKo0nC1W9RHpM1ErRDbb3C6ucKAjvH6HUBi6uWLQjiXjx1hFwz2iU9dOy-ZgLkwaJEPgM9xfk1_D393p5HiKih_bsE8x3jWDkfNuuAu6U0)

  
The output indicates that the migration has not been applied to the database as only the migrations applied to the database will be indicated with an “X”. Let us apply the migrations to the database and find out how it will be reflected in the “showmigrations” command.

```python
python manage.py migrate
```
  
**RESULT**
![](https://lh3.googleusercontent.com/XB9tuYsRwFAjnV76rwSNPdgE8SIAKWGeaLLBTqnmTaiFhj2WlGZsUCWaf59DNdsYFud2_ILfePTsZ6J_czMFdk2STp6vwfEjxMZbad0Qn6D2v3Ekoc8tzbHn0u5etsFAGsayW6OG)

  
```python
python manage.py showmigrations
```
  

![](https://lh6.googleusercontent.com/5aLg10SxDGdeZxq86wWFJQe8HtRwKGvLJWRZIKAukih-0x2dlO3hD8EwrAOFC6V9CyxGkD4wGJthdD4hhMenAbQUZP3wDAbQAiWTxVFF3DTaaGh2VOyz2f8sTQ_kL-SngqpXRImf)

  
### Rolling Back Migrations
Django Migrations provides a convenient way of rolling back migrations to previous versions. Rolling back migrations can be done by calling the migration command with the name of the app and the name of the migration before the migration you want to roll back to.

**Rollback syntax**

  
```python
python manage.py migrate <app name> <migration name>
```
  
The following example demonstrates how we can roll back from the 0003_vehicleinventory migration in the “vehicle_sales_history” app to the 0002_auto_20201205_0500 migration.

#### Identify the current database structure

(Migration - 0003_vehicleinventory)

  
```python
python manage.py dbshell
```

```python
.tables  
  
.schema --indent vehicle_sales_history_salespricehistory  
.schema --indent vehicle_sales_history_vehicleinventory
```
  

**RESULTS**
![](https://lh5.googleusercontent.com/j-KuG8hoNtJOrKN637_HrqYlzR6WVWvjJ7cNh5buFCw7zsKvtIn1rqwQVcPmNhi2CzOlJ57iaGKp7WcDKHxW5u28w21ouVoLJhc9UnGPN2dcNY0hs9qTCsXXWS5xaViXb9Zb5LJi)

![](https://lh3.googleusercontent.com/S2lJ8R3Msq6H93-0ieW5PIruS6upXEVjdvFp7cwJ01yAislYnbBP7JS7OSxmChmsB9c-9Ub_u9bxuqgLOGIfw6b1_sgF0Mh-AlByOqQpdakWNkK50LApuSbBNnvpOmiT5fRjlDha)

#### Roll Back the Migrations

(Roll Back Target - 0002_auto_20201205_0500)

  
```python
python manage.py migrate vehicle_sales_history 0002_auto_20201205_0500
```
  

**RESULT**
![](https://lh3.googleusercontent.com/Vernm7V3pCjNkQmIHVfQWQTUvFmkfXqNKgRtdovPmjei5-bZHPM8dVLfFj6Oohg3oXI00riEAHCqfOjTIo_eX_fkhoovphWXAT9nNI_cImDmdYM8YKUW9p1gZp6RCq2xBUfc5_PU)

  
#### Verify the rollback of migrations
```python
python manage.py dbshell
```
  
```python
.tables  
  
.schema --indent vehicle_sales_history_salespricehistory
```
  

**RESULT**

![](https://lh4.googleusercontent.com/MPNYk6ZvcDdIoC7l63MunxQveSPYcQ-nM4YYAri9g98_j4UDSunDxF_8AuWzyFl48yCZZPR-UXVYeOdQe9WSv6dC2F_0ThMGa_xTxWzJr9z0pOQ1QVuRn9VVhs6Bw2In-RGFnI6X)

  
From the above output, we can see that the “vehicle_sales_history_vehicleinventory” table has been removed and the database has been rolled back to its previous state. The “showmigrations” command will reflect the change by indicating that the “0003_vehicleinventory” migration has not been applied to the database.

  
```python
python manage.py showmigrations
```
  

**RESULT**
![](https://lh5.googleusercontent.com/2M5Lv2FTck9DF--LaC6Wo59Umyd-wrNLL6zym_GU6Nw3ICnTklVw39d3ACWCWlScNCkk3JW5IKhVAH4gbsTI5CdeEMKUFDmXm8RAcMgclCxmoCpYXqcOe988p4tCCn56Dng2u9mY)

There is an important thing to be remembered when rolling back migrations. Although most database operations can be reverted, if a field is removed from the model and the migrations are applied to the database, all the data within the column will be removed. Rolling back in this instance will not recover the data it will only create the removed field.

### Naming Migrations
In the earlier example, we allowed Django to manage the naming conversion of the migration files. However, Django provides the option to create custom names using the “--name” operator.

In the following example, we will remove the 0003_vehicleinventory file and recreate it with the custom name “create_table_vehicleinventory”.

#### Removing the file
```python
rm .\vehicle_sales_history\migrations\0003_vehicleinventory.py
```
  

**RESULT**
![](https://lh5.googleusercontent.com/tHoRn1TuyUA0y2K4vcWHYr55v2BqkNMJvCMADurgbcvbdnV8rLuBHFtHSJFtjv2LfmpLXr2jB9bRviKqCHCGNWLIkcryNwYX5iIC_b78xWhMdzVXNivUU-mukBRMH3khapDM7QjP)

  
#### Create a new migration file
  
```python
python manage.py makemigrations vehicle_sales_history --name create_table_vehicleinventory
```
  

**RESULT**
![](https://lh4.googleusercontent.com/Jd3SGGETsirNa2Mfc6N8C69gb7B1rtXzLGgMQj8Apv6v0BU1MCGjFjaw1zTsMxViArBbDyazPXLzc85Xbb0BmJ9l2n_Yu0kNM7yVUBrXD6SeuI7NZ9RzqGWdQa0YbOZ6pcuqWmH1)

  
#### Apply the migrations
```python
python manage.py migrate
```
  

**RESULT**
![](https://lh3.googleusercontent.com/ap2aDvb3oE6mdmS888O6MH4T_0s0WTBiHzXSOjTTE-ntNcmZYzns0JfBv1ZTW1HZmGFHh2RdphJxQaQp58jymoMxC_IEjGMaZXGwT9LJr2Udow3JoqdYzw2NbIgVXDDwMNRNPBXU)


#### Check the Migration
```python
python manage.py showmigrations
```
  

**RESULT**
![](https://lh5.googleusercontent.com/ClLecoXuD01H4vmymWgcEid1dZEAftekXJpbyCWPolWsh9oty8THFaoQUjFFNwch-227-nfu6jKjrVuNiCgoUXFTqm5eh_X6bjd32Y-CRgmik-XqcjJjG0eRgENpRMgL819lHCTv) 

## Conclusion

In this article, we learned how to effectively use migrations in a Django project. Migration is a way to create and alter tables in a database offered by the Django framework. Using migrations with models, allows the developers to forgo the use of SQL to manipulate a database, unless for specific advanced use cases. This reduces the workload of the developers and allows easy debugging of applications. Additionally, allowing the rollback of migrations acts as a version control system for the database helping developers to roll back changes in case of an error or for testing purposes.
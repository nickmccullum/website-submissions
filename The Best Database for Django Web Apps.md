# The Best Database for Django Web Apps

## What is Django and its ORM feature?

The Django framework is a free and open-source framework designed to develop web applications. This Python-based framework consists of different components like authentication, content management, database interactions that you can use to create any kind of web application.

One of the most powerful and useful features of Django is its Object-Relational Mapper (ORM). The ORM allows developers to map data between the application models and the database without having to write any SQL queries. The Object-Relational Mapper will map object attributes defined in Django model classes to the corresponding fields in the database and interact with the data as necessary from a given database. This allows developers to rapidly develop their applications, eliminating the need to write separate SQL queries for database transactions.

## Django Database Support
The Django framework Model-View-Template (MVT) architecture is designed so developers can change the frontend visual structure of an application without affecting the underlying backend logic. This is especially useful when interacting with databases. When a Django web application is configured, an SQLite database is automatically created by default. However, we can specify a different database by changing the database configuration in the setting.py file of the Django application.

  

Example Configuration using PostgreSQL.
```python
DATABASES={
   'default':{
      'ENGINE':'django.db.backends.postgresql_psycopg2',
      'NAME':'<Project Name>',
      'USER':'<Username>',
      'PASSWORD':'<Password>',
      'HOST':'<IP/URL>',
      'PORT':'<Port>',
   }
}
```

Django is a database-agnostic framework. Giving developers the freedom to select a backend database that best suits their application. Django officially supports the following databases.

-   PostgreSQL
-   MariaDB
-   MySQL
-   Oracle
-   SQLite
    
Additionally, Django supports CockroachDB, Firebird, and Microsoft SQL Server via [3rd party backends](https://docs.djangoproject.com/en/3.0/ref/databases/#third-party-notes). The important thing to note here is that not all ORM features are supported by 3rd party backends.

## Best Database for Django

The three most widely used Database Management Systems for Django are SQLite, MySQL, and PostgreSQL.
The  Django community and official Django documentation state PostgreSQL as the preferred database for Django Web Apps. The official Django documentation states the following about PostgreSQL.

“Django provides support for a number of data types which will only work with PostgreSQL. There is no fundamental reason why (for example) a contrib.mysql module does not exist, except that PostgreSQL has the richest feature set of the supported databases so its users have the most to gain.”

The Django framework supports PostgreSQL 9.5 and higher. The [psycopg2](https://www.psycopg.org) adapter version 2.5.4 or higher is required to establish a connection between Django and PostgreSQL databases. Django uses the “django.contrib.postgres” module to make database operations on PostgreSQL. Out of all the available databases, PostgreSQL provides the richest feature set and full compatibility for extended functionality such as GeoDjango to create geographic web applications.


## What is PostgreSQL?

PostgreSQL is an enterprise-grade free and open-source database management system. PostgreSQL uses and extends the SQL language with many features that allow this database to be used in complicated data workloads. The PostgreSQL database is well known for its proven architecture, reliability, data integrity, robust feature set, and extensibility. With its 30 years of active development and a dedicated open-source community, this has become a highly reliable DBMS.

The PostgreSQL database supports all major operating systems and has been [ACID](https://en.wikipedia.org/wiki/ACID)-compliant since 2001. This database supports SQL for relational and JSON for non-relational database queries.


Following are some of the features of PostgreSQL

-   Compatibility with various platforms, languages, and middleware
-   Robust access-control system and Multi-factor authentication support
-   Tablespaces
-   Nested transactions
-   Advanced Indexing options such as GiST, GIN, Bloom filters, etc…
-   Write-ahead Logging (WAL)
-   Custom Data Types
-   Proven Data Integrity
-   Standby server and high availability
-   Multi-version concurrency control
    
Let us take a look at the major differentiating factors between MySQL and PostgreSQL databases.

| MySQL                                                                                                         | PostgreSQL                                                                                                                  |
|---------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| MySQL is available under GNU Licence and other proprietary license agreements.                                | PostgreSQL is released under PostgreSQL License.                                                                            |
| MySQL offers paid versions with support from Oracle Corporation.                                              | Completely free and open-source solution.                                                                                   |
| MySQL ACID compliance depends on using the NDB and InnoDB cluster storage engines.                            | PostgreSQL is a complete ACID-compliant solution.                                                                           |
| MySQL has a speed advantage in OLAP (Online Analytical Processing) and OLTP (Online Transactional Processing) | PostgreSQL performs well in the execution of complex queries.                                                               |
| MySQL is best suited for BI (Business Intelligence) applications.                                             | While PostgreSQL works well with BI applications, it’s geared more towards Data analysis and Data Warehousing applications. |

### Advantages of PostgreSQL

-   PostgreSQL’s write-ahead feature for logging increases the fault-tolerant nature of the database.
-   The database has built-in support for geographic objects which make PostgreSQL the ideal choice for geographic data handling. This enables PostgreSQL to be used as a geospatial data (data containing geographical components like coordinates, addresses, etc...) store.
-   A large active community that leads to consistent database improvements.
-   PostgreSQL conforms to 170 out of 176 mandatory features of the SQL:2016 core conformance.
-   Easy administration and maintenance in both embedded and enterprise usage.
    

## Django specific functionality with PostgreSQL
Using the Django framework with the PostgreSQL database provides many benefits over other databases. In the below section, we will go through a high-level overview of PostgreSQL specific features in Django. Please refer to the official Django documentation for a comprehensive understanding of each feature using the provided links.
-   Django offers [PostgreSQL specific model fields](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/fields/) such as ArrayField where lists of data can be stored, HStoreField where we can store key-value pairs and JSONField to store JSON encoded data.

    **ArrayField Data Type**
    ```python
    from django.contrib.postgres.fields import ArrayField
    from django.db import models
     
    class VehicleDetails(models.Model):
        make = models.CharField(max_length=250, null=False)
        model = models.CharField(max_length=250, null=False)
        engine_numbers = ArrayField(
            ArrayField(models.CharField(max_length=15, blank=True), size=8,),
            size=8,
        )
    ```
    **JSONField Data Type**
    ```python
    from django.contrib.postgres.fields import JSONField
    from django.db import models
     
    class Personal_Information(models.Model):
        user_id = models.CharField(max_length=20, primary_key=True)
        name = models.CharField(max_length=200, null=False)
        data = JSONField()
     
        #Sample JSON Data Set
        # data = {
        #   'group' : 'admin',
        #   'other_permissions': {
        #       'file_access' : True,
        #       'object_access': False,
        #   },
        # }
     
        def __str__(self):
            return self.name
    ```

  

-   [PostgreSQL specific aggregation](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/aggregates/#aggregate-functions-for-statistics) provides functions for both General-purpose data aggregation and statistical analytics.
    
    **StringAgg function**
    ```python
    # String Aggregation
    UserDetails.objects.aggregate(result=StringAgg('name'))
     
    # String Aggregation using a delimiter
    UserDetails.objects.aggregate(result=StringAgg('name', delimiter=';'))
    ```
  

-   The [PostgreSQL specific database constraints](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/constraints/) allow developers to enforce rules on the type of data that can be inserted into the database. This increases overall data accuracy and reliability.
    
    **ExclusionConstraint**
    ```python
    from django.contrib.postgres.constraints import ExclusionConstraint
    from django.contrib.postgres.fields import DateTimeRangeField, RangeOperators
    from django.db import models
    from django.db.models import Q
     
    class ReservatonDetails(models.Model):
        reservation_id = models.IntegerField()
     
     
    class VehicleDetails(models.Model):
        reservation = models.ForeignKey('ReservatonDetails', on_delete=models.CASCADE)
        timespan = DateTimeRangeField()
        cancelled = models.BooleanField(default=False)
     
        class Meta:
            constraints = [
                ExclusionConstraint(
                    name='exclude_overlapping_reservations',
                    expressions=[
                        ('timespan', RangeOperators.OVERLAPS),
                        ('reservation', RangeOperators.EQUAL),
                    ],
                    condition=Q(cancelled=False),
                ),
            ]
    ```
  

-   Django framework provides [PostgreSQL specific form fields and widgets](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/forms/) using the “django.contrib.postgres.forms” module to enhance the functionality of Django forms and widgets.
    
    **SimpleArrayField for Forms**
    ```python
    from django import forms
    from django.contrib.postgres.forms import SimpleArrayField
     
    class OrderQuantity (forms.Form):
        orders = SimpleArrayField(forms.IntegerField(), delimiter=',')
    ```
  

-   [PostgreSQL specific database functions](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/functions/) such as TranscationNow that return the date and time of the database server when the current transaction started.
    
    **TranscationNow function**
    ```python
    from django.contrib.postgres.functions import TransactionNow
 
    UserDetails.objects.filter(lastmodified__lte=TransactionNow())
    ```
  

-   [PostgreSQL specific model indexes](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/indexes/) like BrinIndex, BTreeIndex, GinIndex provide the users with advanced indexing functionality that can help manage large datasets.
    
    **BrinIndex Index Creation**
    ```python
    from django.contrib.postgres.indexes import BrinIndex
 
    class Measurement(models.Model):
        class Meta:
            indexes = (
                BrinIndex(fields=['time']),
            )
     
        time = models.DateTimeField(
            'Time of measurement',
            null=True
        )
    ```
  

-   While Django offers a wide variety of built-in lookups for filtering, [PostgreSQL specific lookups](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/lookups/) extend this functionality further. One of the PostgreSQL specific lookups is Unaccent which enables accent-insensitive lookups.
    
    **Unaccent Lookup**
    ```python
    # Unaccent lookup for user first name
    UserDetails.objects.filter(first_name__unaccent__startswith='Barry')
    ```
  

-   PostgreSQL provides functionality to create PostgreSQL extensions in the database using Django [Database migration operations](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/operations/).
    
    **Installing BtreeGinExtension with a migration**
    ```python
    from django.contrib.postgres.operations import BtreeGinExtension
     
    class Migration(migrations.Migration):
        # Migration Commands
     
        operations = [
            BtreeGinExtension(),
            ...
        ]
    ```
  

-   PostgreSQL database supports [Full-text search](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/search/) functionality which enables searching natural language documents using Django.
    
    **SearchQuery**
    ```python
    from django.contrib.postgres.search import SearchQuery
     
    # Search as separate phrases
    # Default search_type=plain
    SearchQuery('Lex Corp') 
     
    # Search as a single phrase
    SearchQuery('Stark Industries', search_type='phrase')
    ```
  

-   The “django.contrib.postgres.validators” module provides additional [validators](https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/validators/) that are specific to PostgreSQL.
    
    **Range Validators**
    ```python
    from django.contrib.postgres.validators import RangeMinValueValidator, RangeMaxValueValidator
    from psycopg2.extras import NumericRange
     
    class UserDetails(models.Model):
        name = models.CharField(max_length=200, null=False)
        age_range = IntegerRangeField(
            default=NumericRange(1, 101),
            blank=True,
            validators=[
                RangeMinValueValidator(1), 
                RangeMaxValueValidator(100)
            ]
        )
    ```
  

# Conclusion
Django with its preferred database, PostgreSQL, enables developers to leverage all the advantages of PostgreSQL within a Django application. In this article, we gained an understanding of why PostgreSQL is the best database for a Django web app and the extended functionality it offers.
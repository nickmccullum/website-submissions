# How to Use Celery and Django to Handle Periodic Tasks

## What is Celery

Celery is a background job manager that can be used with Python. Celery is compatible with several message brokers like RabbitMQ and Redis. The core Django framework does not provide the functionality to run periodic and automated background tasks. Celery comes into play in these situations allowing us to schedule tasks using an implementation called Celery Beat which relies on message brokers.

Some examples of scheduled tasks are

-   Batch email notifications
-   Scheduled maintenance tasks
-   Generating periodic reports
-   Database and System snapshots

The Celery projects describe itself as follows.

> Celery is an asynchronous task queue/job queue based on distributed
> message passing. It is focused on real-time operations but supports
> scheduling as well. The execution units called tasks are executed
> concurrently on one or more worker servers using multiprocessing,
> Eventlet, or gevent. Tasks can execute asynchronously (in the
> background) or synchronously (wait until ready).

In this tutorial, we are going to take a look at how to configure a simple scheduled task in a Django project.


## Getting Started

First, We'll create a Python virtual environment and install the packages mentioned below in an Ubuntu environment. Then we will create a Django project called “simpletask”. 

-   Django Framework
-   Celery
-   Redis

  
**Creating a virtual environment**
 
```bash
python3 -m venv celerytest  
cd celerytest  
  
ls  
source ./bin/activate
```
  

**RESULT**
![](https://lh6.googleusercontent.com/Jxac6_a8ElnUq5jCG1yqE7hH_pkAdvSn2bXn3HH_awNU9z0gh8yaMtCwdrgVY8RcqrYMrWdtm1pzmVW56_8PLxqcGJ_VGk643sjuQ7gq0HhvBuPzDBaCKn-9KaO2p1iMTs9Vn71I)


**Installing Django framework**
  
```bash
pip3 install django
```
  
**RESULT**
![](https://lh5.googleusercontent.com/XvAU1ADO-c3KTC4pGC8-P79Z4_S8G-EeP9WVQ7C3MTNLNJ2uO16aINUa_bieICR75oxC98IPfZu2e1C1puUlfkbJOdsiKJqOPRgX3nIYEioStB8vU82TN-_TaijmrnfY5cEWq4wT)

**Installing Celery** 
```bash
pip3 install celery
```
  
**RESULT**
![](https://lh5.googleusercontent.com/WsuQslFtbr2SBCFe3PzSZH3Jlqrk7B_ZD8Y99p0fgpqR0O46gwhr1-ryIzp--fbqFb-GMCNwA5io6Fn6LYJ6K7r58921ixeDLedkPeG0DdkYfv8XCxwNIQzu5gEJddwXhQlNfc2k)

  
**Installing Redis**
Next, we will download the latest stable Redis package and build it.
  
```bash
wget http://download.redis.io/redis-stable.tar.gz  
tar xzf redis-stable.tar.gz  
cd redis-stable  
sudo make install
```
  

**RESULT**
![](https://lh6.googleusercontent.com/i6HX762DtwG2Ah7-1BRdCcSknZr_MBB_XYfIpWUZNUG57wLPpWHlg2HsugkZWlWdKVxEZ9tTeaA78l9PO8WjVayqt4V4sbM6sjbzr0ceo9HZ9iuonl7Ns-EQotA5p-Yn8E1iU4Mi)

  
After completing the make operation, we start the Redis server as a demon and test it. 
```bash
redis-server --daemonize yes  
redis-cli ping
```
  
**RESULT**
![](https://lh5.googleusercontent.com/uVILXpJhjvlu5ROzZFmVCdaKEai-PDBeF0d6YBEgjriAwdlGu-X5_huBkKfPObzMvASlEjr5PfV2PagLdNJJp6olHf6zHIHmIn6Udms-stXda8Fdbqa4fKRTfclBo7Tm6q6uv1dV)

Finally, let us install the Redis pip package
```bash
pip3 install redis
```
  
**RESULT**
![](https://lh3.googleusercontent.com/iaV8YTwCCd-UzjUznueYf65V62P0lH6jj4NA2qYZt1zeN-nJSpSbdfaEKdJopaZ6LccA6tTO1CeHGsKogsl6jYRqLnFGwnJPUa-EvYQ-00E4PNUPZYxcq79jmSg6MYIUuwW_KLzL)

  
**Creating the Django project**
```bash
django-admin startproject simpletask  
tree simpletask
```
  

**RESULT**
![](https://lh3.googleusercontent.com/_7DpiDrpLnar0O1PqAJs364AbEKyvnXgX41AJIcuft8pgyi9abS6ydNOrho6fyf95_c-q-_GpnJ2U3iKOFPKVQ-5chfF6J7reOX6Ri_y5ytsPG48ox4u9SiouX7vSoV7f2AjsRzO) 

## Setting up Django Project
In this section, we will cover how to incorporate Celery into the Django project “simpletask”.
Let us create a celery.py file in the main Django project directory. This module is used to define the celery instance.

**simpletask/celery.py**
```python
from __future__ import absolute_import, unicode_literals
import os
from celery import Celery

# set the default Django settings module for the 'celery' program.
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'simpletask.settings')

app = Celery('simpletask')

# Using a string here means the worker doesn't have to serialize
# the configuration object to child processes.
# - namespace='CELERY' means all celery-related configuration keys
#   should have a `CELERY_` prefix.

app.config_from_object('django.conf:settings', namespace='CELERY')


# Load task modules from all registered Django app configs.
app.autodiscover_tasks()

@app.task(bind=True)
def debug_task(self):
    print('Request: {0!r}'.format(self.request))
```
  
Then import the new Celery app to the initialization file so the Celery app will be loaded at the start of the Django project.

**simpletask/__init__.py**
```python
from __future__ import absolute_import

# This will make sure the app is always imported when
# Django starts so that shared_task will use this app.
from .celery import app as celery_app

__all__ = ('celery_app',)
```
  
To use the Celery Beat, we need to configure the Redis server in the Django projects settings.py file. As we have installed the Redis server on the local machine, we will point the URL to localhost. The CELERY_TIMEZONE variable must be correctly set to run the tasks at the intended times. Redis will act as the broker to pass messages between the Django project and the Celery workers. 

**simpletask/settings.py**
```python
# Celery Broker - Redis  
CELERY_BROKER_URL = 'redis://localhost:6379'  
CELERY_RESULT_BACKEND = 'redis://localhost:6379'  
CELERY_ACCEPT_CONTENT = ['application/json']  
CELERY_TASK_SERIALIZER = 'json'  
CELERY_RESULT_SERIALIZER = 'json'  
CELERY_TIMEZONE = "Asia/New_York"
```
  
We run the following command in the main project folder where manage.py file is located to test if the configuration is applied correctly. The -A option indicates the project name while the -l option indicates the log level.

  
```bash
celery -A simpletask worker -l info
```
  
**RESULT**
![](https://lh6.googleusercontent.com/CoKyiT63SlcNiKPbufAof1293oHmPrIn3QPobJWlS7rC0Tl1Y9YVMMuypLoDb6rx1JcHRuPxbcyUQ7W5IjaQO083yv26Shjdz4bAPcCdUgW3BvhaZFpC20ZSMoZipIjUJLzSahVj)

  
The above output indicates that the Celery Worker is ready to receive tasks. Next, let us check if the Celery task scheduler is ready. Terminate the Celery Worker and start the Celery Beat using the command below.

  
```bash
pkill -f "celery worker"  
celery -A simpletask beat -l info
```
  
**RESULT**
![](https://lh4.googleusercontent.com/9SimEm5tQJvQ51Jvd_UzPTjx8ohjCOE2JKqF2uSZk3vu5B1oqIbAno4M-A8naxOIQ5N2TTcbdMjippbm1DKd-cQ3xT_CgIszT9H56OTMggC611NF3zO5n7acjaUlKT2zuPBfjtir)


Before moving to the next section, please make sure that both these tasks are terminated.

  
## Celery Tasks
We will create a new Django app called “sendmessage” to add Celery tasks and register the app within the settings.py.

  
```bash
python manage.py startapp sendmessage
```
  
**RESULT** 
![](https://lh6.googleusercontent.com/yJMWpW_5AuvvmuMXpEbPFmbe64ItSvG0vvbPmccxmJf-JZy8T-_QUPzhAGNvdynsvpkiusPCsUMc0VUmmA-NUUod2OvNDyO9SP0T49Pa3aeAad7OVI2uDik8RFesdjO4sbo92kb9)

  
**simpletask/settings.py**
 
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'sendmessage',
]
```
  
Within the “sendmessage” application, we will create a tasks.py file to create Celery tasks. We will be using the @shared_task Python decorator so we can create simple tasks without having a concrete app instance.

  
**sendmessage/tasks.py**

```python
from __future__ import absolute_import, unicode_literals
from celery import shared_task
from datetime import datetime

@shared_task(name = "print_msg_main")
def print_message(message, *args, **kwargs):
  print(f"Celery is working!! Message is {message}")

@shared_task(name = "print_time")
def print_time():
  now = datetime.now()
  current_time = now.strftime("%H:%M:%S")
  print(f"Current Time is {current_time}")
  
@shared_task(name='get_calculation')
def calculate(val1, val2):
  total = val1 + val2
  return total
```
  

## Celery Worker
The Celery Worker creates a parent process to manage the running tasks. This process handles features like sending messages, registering tasks, tracking task status, etc…

In the following example, we run the Celery Worker for the Django project “simpletask”.

  
```bash
celery -A simpletask worker -l info
```
  
**RESULT**
![](https://lh4.googleusercontent.com/-4_RiPFN3elC26wn9NDrRvzorZ1y_kTWuKSiyoKfU06k_t4UyFm1f9eQZD7hIxBll8BBq6pI4zpBhrCycC2v7J90DZhx5d0J_5I_6Wcg3VCQDZ-fDBgFK3xCAKBrQiimEwHi1gSD)

  
The above output shows all the tasks we specified in  the tasks.py file in  the “sendmessage” application.While we can run the celery worker as the main process, this essentially makes the terminal unusable. To mitigate this issue, we can run the Celery worker as a background process using the `--detach` argument. Let us terminate the current worker using `CTRL+C` and restart the Celery worker as a detached process with a log file specified to capture the Celery logs.

  
```bash
celery -A simpletask worker -l info --logfile=celery.log --detach
```
  
**RESULT**
![](https://lh3.googleusercontent.com/EMjFhBDckVmBredMbzCSmKtzcGcVhaO0eUqJU-tcQ2efvqBwZknzjovpteXy-WwlO-Ybhsqjriyx6HgSp-4V1rpj7r4plmhJDpenYPla4ibluT15e8LL0rOVRph4_uTDbRDzRdgH)

  
### Testing the Tasks
We can test the tasks by using the Django shell to import the tasks module and call each function as shown below. The delay() method is used to call each task. The delay() method is pre-configured with default configurations and only requires arguments that need to be passed to each function.

```bash
python manage.py shell  
  
from sendmessage.tasks import print_message, print_time, calculate  
  
print_message.delay("Hello World")  
print_time.delay()  
calculate.delay(10,20)
```
  
**RESULT**
![](https://lh5.googleusercontent.com/8RQwQ-q87Jn0r5iYqgAFFVXFLs-rGTSZnCRjvvIOYtcPLnwxLIrVHzJaBU5TUxKRuEfGdzkl4RXAsW-dxmyj_3AU8bTFcCukGZVF9QM_sRv8VYPxm4S1Czq9HDvzWOJ1tH1hz_zx)


Now we will check the celery worker logs. These logs will indicate the successful task executions. Each task can be identified via the name specified with the @shared_task python decorator.

```bash
cat celery.log
```

**RESULT**  
![](https://lh3.googleusercontent.com/lWpz0POGFBu7T4rkj7u5Hj_yWiuUDuA0pgjiHppyDzCSupi3tgtq_Od1OyJl6wFVj8Ll-WN4hrticEJOAwvpXd1Ms6xMuuNMicpWF-5K4TrYPDmuQ2SKf7odYfl0HbvlDV5qnstn)

  
## Periodic Tasks
Using the celery Beat, we can configure tasks to be run periodically. This can be defined either implicitly or explicitly. The thing to keep in mind is to run a single scheduler at a time. Otherwise, this would lead to duplicate tasks. The scheduling depends on the time zone (CELERY_TIMEZONE = "Asia/New_York") configured in the settings.py

We can configure periodic tasks either by manually adding the configurations to the celery.py module or using the django-celery-beat package which allows us to add periodic tasks from the Django Admin by extending the Admin functionality to allow scheduling tasks.

### Manual Configuration
In the following example, we will modify the celery.py file in the simpletask app to do the following,

1.  Every ten seconds print the Hello message.
2.  Every twenty seconds print the current time.
3.  Every forty seconds calculate the total of 10 and 20.
    

**simpletask/celery.py**

```python
from __future__ import absolute_import, unicode_literals
import os
from celery import Celery

# Default Django settings module for Celery
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'simpletask.settings')

app = Celery('simpletask')

# Using a string here eliminates the need to serialize 
# the configuration object to child processes by the Celery worker.

# - namespace='CELERY' means all celery-related configuration keys
app.config_from_object('django.conf:settings', namespace='CELERY')


# Load task modules from all registered Django applications.
app.autodiscover_tasks()

@app.task(bind=True)
def debug_task(self):
    print('Request: {0!r}'.format(self.request))
    
    
app.conf.beat_schedule = {
    #Scheduler Name
    'print-message-ten-seconds': {
        # Task Name (Name Specified in Decorator)
        'task': 'print_msg_main',  
        # Schedule      
        'schedule': 10.0,
        # Function Arguments 
        'args': ("Hello",) 
    },
    #Scheduler Name
    'print-time-twenty-seconds': {
        # Task Name (Name Specified in Decorator)
        'task': 'print_time',  
        # Schedule      
        'schedule': 20.0, 
    },
    #Scheduler Name
    'calculate-forty-seconds': {
        # Task Name (Name Specified in Decorator)
        'task': 'get_calculation',  
        # Schedule      
        'schedule': 40.0,
        # Function Arguments 
        'args': (10,20) 
    },
}  
```
  
After modifying the celery.py file, let us start both the Celery Beat and Worker processes. First, we terminate any currently running workers and then start both services as shown below,

```bash
pkill -f "celery worker"  
celery -A simpletask beat -l info --logfile=celery.beat.log --detach  
celery -A simpletask worker -l info --logfile=celery.log --detach
```
  
**RESULT**
![](https://lh5.googleusercontent.com/cpD8WSX4Hsi0m5MTawAJlMbuYcnspCv-w75lh4Q8EFBRyMFqT2AR8Ov0JGeEJZ_CJxnM8EGYDKBbS2CKebjonS199qzuAQGX-rTuhxl1DeqO7Eg0KT_1bbFdbqg9T_Ax3VxXVaUl)

  
To terminate all running Celery processes, we can use the following command.

```bash
kill -9 $(ps aux | grep celery | grep -v grep | awk '{print $2}' | tr '\n'  ' ') > /dev/null 2>&1
```
  
If we check the log files for the Celery Worker and Beat, we can identify that the tasks are running periodically.

```bash
cat celery.beat.log
```
  

**RESULT**
![](https://lh4.googleusercontent.com/T5-Lsm683YlA7T2ugXQdxe3gHUuHcTI6-Q3BCfkVndJtRHcbmSM1mUUDAAq7-mz6O_xytMoysqMbKF9UHa-bMuQDxyJXJ_G3uu-X86P3IYRoGj3uE7K8IHu5zjLZfzJzfXlS0ruN)

  
```bash
cat celery.log
```
  

**RESULT**
![](https://lh4.googleusercontent.com/KFwY5uotQyKPw7VOjvTp175bmjIhZ5NblkFC8yCfy1jsFjc6z9VDeInYIlt8UZ3yjnHaZHKxiiUzT2qcjKh1q2iacpgZ1M2nq7TKNgHPdxwCq6WLUruOi16rLzOccwTC375_Ete7)

  
In the next example, we will create a function in our tasks file in the “sendmessage” app to check the network speed. Then we will modify the celery.py file to execute the task every 10 minutes using a cron job

**Install dependency**

```bash
pip3 install speedtest-cli
```
  

**sendmessage/tasks.py**

```python
from __future__ import absolute_import, unicode_literals
from celery import shared_task
import datetime
import speedtest
import time

@shared_task(name = "print_msg_main")
def print_message(message, *args, **kwargs):
  print(f"Celery is working!! Message is {message}")

@shared_task(name = "print_time")
def print_time():
  now = datetime.datetime.now()
  current_time = now.strftime("%H:%M:%S")
  print(f"Current Time is {current_time}")
  
@shared_task(name='get_calculation')
def calculate(val1, val2):
  total = val1 + val2
  return total


@shared_task(name='check_network_speed')
def check_speed_fortmat():  
    s = speedtest.Speedtest()
    number_of_times = 0
    while number_of_times < 2:
        time_now = datetime.datetime.now().strftime("%H:%M:%S")
        downspeed = round((round(s.download()) / 1048576), 2)
        upspeed = round((round(s.upload()) / 1048576), 2)
        print(f"time: {time_now}, downspeed: {downspeed} Mb/s, upspeed: {upspeed} Mb/s")
        time.sleep(60)
        number_of_times += 1
```
  
  
**simpletask/celery.py**
  
```python
from __future__ import absolute_import, unicode_literals
import os
from celery import Celery
from celery.schedules import crontab

# Default Django settings module for Celery
os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'simpletask.settings')

app = Celery('simpletask')

# Using a string here eliminates the need to serialize 
# the configuration object to child processes by the Celery worker.

# - namespace='CELERY' means all celery-related configuration keys
app.config_from_object('django.conf:settings', namespace='CELERY')


# Load task modules from all registered Django applications.
app.autodiscover_tasks()

@app.task(bind=True)
def debug_task(self):
    print('Request: {0!r}'.format(self.request))

app.conf.beat_schedule = {
    # Execute the Speed Test every 10 minutes
    'network-speedtest-10min': {
        'task': 'check_network_speed',
        'schedule': crontab(minute='*/10'),
    },
} 
```
  

**Stop all Celery processes**
  
```bash
kill -9 $(ps aux | grep celery | grep -v grep | awk '{print $2}' | tr '\n'  ' ') > /dev/null 2>&1
```
  

**Start the Celery beat and worker processes**
  
```bash
celery -A simpletask beat -l info --logfile=celery.beat.log --detach  
celery -A simpletask worker -l info --logfile=celery.log --detach
```
  

**Check the log files**
  
```bash
cat celery.beat.log
```
  

![](https://lh6.googleusercontent.com/uHr3slgl67z6vXP8B68PVLeJ2FarwXLnkNyI5AMqog0NyG9wcKliGK51SI28DJOS0IkiVOxsuKX-aXHxYbR2WUQauTwzV-yYp0TWd41MG3ClDJ8Coh7ZE6ZpEgWURenZor9LDTRV)

  
  
```bash
cat celery.log
```
  

![](https://lh4.googleusercontent.com/-rO0U7fZKe1qd3z9Aq_RAVyzKWSlgE1cjzkcnDd6qzlflVaJTIGe9YBjWfS1a8Q-iwblkooihKfLZ6FbVn87KJOMBDOCaL-iUZa9CtPieDJ-8KOv064H5GwdsmgAWULJG5PNn4Dl)

  
The output indicates that the “network-speedtest-10min” task is running every 10 minutes as defined in the cron job.

### Using django-celery-beat

This extension enables the user to store periodic tasks in a Django database and manage the tasks using the Django Admin interface. Use the following steps to install django-celery-beat in the simpletask project.


**Install the django-celery-beat using pip**

```bash
pip3 install django-celery-beat
```
  

**RESULT**
![](https://lh6.googleusercontent.com/uvDebvGs4Rr9SNS2bzqEUzPUVtq0JA1qrrWj7pe3eCcI9rr5wuVozD0yclCzvEScC2Fsxfloa-Q8UlBxuTYN8OwiigHO1xXZJqlCTykDQ2r9pvxymyFCWcwu-7KBSaPUKhUJ1SjG)

  
**Integrate the app**
Add the django_celery_beat app to the INSTALLED_APPS section in the setting.py file and configure ALLOWED_HOSTS to allow connections to this Django server.

**simpletask/settings.py**

```python
# Server IP address
ALLOWED_HOSTS = ['10.10.10.55']

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'sendmessage',
    'django_celery_beat',
]
```
  
**Run Migrations**
```python
python manage.py migrate
```
  

**RESULT**

![](https://lh6.googleusercontent.com/F490FRN_Yga6ZTTlZJAd1PpZQnXk2xgvCJ93bb1gr4UzkXm4oggBomqPLLIX3RpVfRb4lNLJHBmzdHjzCKXkMuaAi6gD-OJl3WDxoznimjxf4lBZL9pnqQoLF_fUGy0fdi-YrirN)
 

**Reset database scheduler**
Changing time zone related settings will not change the time zone settings in the database scheduler. We need to manually reset the database scheduler time zone settings to identify the changes we have made while migrating. To reset the time zone settings, we use the Django shell to run the following commands.

  
```python
python manage.py shell  
  
from django_celery_beat.models import PeriodicTask  
PeriodicTask.objects.update(last_run_at=None)  
exit()
```
  
**RESULT**
![](https://lh6.googleusercontent.com/7h47lpaMslfajQ12Yl5lOvvW5rkDVPcvVi7J5x6u6K0CyKP_Zn03FzVYFAsG586nv3Xz445Bj6ev1R7ZETtEG4P7S-oVYWVMlIPocnkyZgCXz4YY1MJshgJYYNhFri5z4ryvjn0q)

  
**Create Django Admin user**
  
```python
python manage.py createsuperuser
```
  
**RESULT**

![](https://lh6.googleusercontent.com/fjKbkpAQ0eHmJsneEZOKEaorzxK6Mu4NRDyHvltgnZw0ctvPINPzQXff6L5aMFMkAw7GwGRkO1yyMvVHx4LYIE9MNWCLhg6ffOBUWEpyBqbWusOFRKV1w_vNWl3k273Bs-NEPh94)

  
**Start the Django Server**
```python
python manage.py runserver 0.0.0.0:8000
```
  

**RESULT**
![](https://lh5.googleusercontent.com/61uUJ87sVsf1-sAIilPUpSFNYmly2jKlTBtwUDWPnZPf2-UsCFXpZhwyMo_2vquKpnoDbeg-fJAP8BGKXqMYQArR6N_IOsH9p4mn9gn2JJlsc5zIGsT6Q6gjTebV6FuKrh98Aeyo)

  
**Access the Admin interface**
Using the newly created credentials, we can access the Django admin interface. Then we add a periodic task called “Print time every 30 seconds” from the “Periodic Tasks” section. Any task we have defined in the tasks.py file will be automatically shown in the registered task dropdown.

**Add periodic task screen**
![](https://lh6.googleusercontent.com/cd2Gpw8yA1x_CL4CL_ZeIMaFEpHJwI3ZgVwGLMMzGE_DbfQJ_krhxfcaxubM7BFxZ-1H7IGmfh8E6_2DfVxbspsAFe2tYHeIO-Oa0TCTyU20yt2S14uOyCRMEv9Lc1eZEP3F0bGu)


**Periodic task list**
![](https://lh3.googleusercontent.com/WiA-5mHyGtg206MLtxU4nEiY1eUpyvu9LhSVC2cZFmauPF1XRAe5V2Q6-pr1jhRwE7Pn5LXs2uTuOlxkWWQEwrbs6jeru0xtnkuPE6O12EKkliaVFKvLVc92CFPYNhsH-QZt216z)


**Terminate any running Celery processes**

```bash
kill -9 $(ps aux | grep celery | grep -v grep | awk '{print $2}' | tr '\n'  ' ') > /dev/null 2>&1
```

**Start Celery worker and beat**
  
```bash
celery -A simpletask worker -l info --logfile=celery.log --detach
```
  
We will define the --scheduler argument to indicate that the scheduled tasks are within the database. We will be using a different terminal instance for these commands as we are currently running the Django server in the original terminal instance.

  
```bash
celery -A simpletask beat -l info --scheduler django_celery_beat.schedulers:DatabaseScheduler
```

**RESULT**
![](https://lh5.googleusercontent.com/A3SjWCJMPuBXS3Fu5MCEFAMHvgGO0JK0zGr1vk6pYK9fxllaW-w6vq4O6lAQZSxXGx8rGCjzPHSL7cKr-wq2mxfclIsUaGW4PHzatvWOx6mEQLnm1kpqUdBckbFTAnJDmHlNKCay)

  
**Check the Logs**

```bash
cat celery.log
```
  

**RESULT**
![](https://lh4.googleusercontent.com/NqGr3KqxExJXhSFi0JTrcORe2ItVrDVOqATlSY-sNjPU81lcdEDNx3HIJLJ7tKw3m-HvxYrfmpU8CreRrwYfMcczkgZPad0OK6VRCo9DiRNJYSAs_8S1_Gj35MhjtxKcte2WLgxD)

  
The above output shows us that the Periodic Task created from the Django Admin interface is being successfully executed every 30 seconds.

## Conclusion
In this tutorial, we gained a basic understanding of the Celery module functionality. When creating scalable web applications, Celery provides a task queue with real-time processing and task scheduling functionality, which are absent in the core Django framework. Celery modules Periodic Task functionality allows developers to automate repetitive tasks from within a Django project.
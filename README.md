# DjangoQuerySet-get
Django 
Django is a high-level Python web framework that enables the rapid development of secure and maintainable websites. It is free and open-source and follows the model-template-views (MTV) architectural pattern.

QuerySet API
In Django, QuerySet represents a collection of database records that Django retrieves, manipulates, and returns to the user. QuerySet provides a high-level, Pythonic interface for interacting with databases, allowing developers to perform powerful database operations without needing to write raw SQL queries.

A QuerySet is generated whenever a database query is made using Django's Object-Relational Mapping (ORM) layer. It acts as an abstraction layer between the developer and the database, providing a convenient and expressive way to retrieve, filter, sort, and aggregate data from the database.

QuerySet offers a rich set of methods and chaining capabilities that enable developers to easily query and manipulate data. With QuerySet, you can filter records based on specific criteria, perform complex lookups, order the results, paginate them, aggregate values, and much more. These operations are performed using a syntax similar to writing SQL queries but in a more Pythonic and object-oriented manner.

# To Use QuerySet in Django Follow Below Steps :

Step 1 : Make sure you installed Django in your Python environment
Install Python from https://www.python.org/downloads/
In your Windows PowerShell type 'pip install django' to install Django in your Python environment
#Note : Use IDE like Vs Code as code editor 
Python-and-Django-min
python and django installed

Step 2 : Setting up Django project
Create a new folder with project name in your local machine
Open project folder in your IDE ( Vs code )
Open new terminal and type 'django-admin startproject myproject' to set up new Django project. It will create all the necessary files and folders 
Creating-MyProject-min
myproject created
In terminal type 'python manage.py runserver' this will launch development server. If you click on link it will take you to Welcome page

Step 3 : Create a Django application within your project
In your terminal type 
1] 'cd myproject' 
2] 'python manage.py startapp myapp'
above steps will create a django application within your project
settings-min
myapp and myproject created

Step 4 : Creating Models in myapp
In my app click on 'models.py'
Create Models Accordingly. Here are some example Models I created
from django.db import models

# Create your models here.
class Blog(models.Model):
    name = models.CharField(max_length = 100)
    tagline = models.TextField()

    def __str__(self):
        return self.name

class Author(models.Model):
    name = models.CharField(max_length = 200)
    email = models.EmailField()

    def __str__(self):
        return self.name

class Entry(models.Model):
    blog = models.ForeignKey(Blog, on_delete = models.CASCADE)
    headline = models.CharField(max_length = 250)
    body_text = models.TextField()
    pub_date = models.DateField()
    authors = models.ManyToManyField(Author)
    rating = models.IntegerField()

    def __str__(self):
        return self.headline

models-min
models

Step 5 : Configure Database
In myproject click on settings.py in INSTALLED_APPS add 'myapp.apps.MyappConfig'
In myapp click on admin.py and import all Models by typing 'from .models import Your_Model_Names' . And type 'admin.site.register(Your_Model_Name)'.
and 'ctrl + s' to save changes

settings-min
settings.py

Step 6 : Creating Objects for Query
In terminal type 
1] 'python manage.py makemigrations' this will populate the database
2] 'python manage.py migrate' this will migrate to database
3] 'python manage.py createsuperuser' this will create super user

# You can create objects in following ways :

1] In local host http://127.0.0.1:8000/admin/ you can add or change the objects
django-administration-portal-min
admin portal
django-admin-min
add or change objects

2] In new terminal type 'python manage.py shell' this will open django shell where you can add or change objects
Django-shell-min
Django shell
Adding or Changing Objects in Django Shell : 
Import Model from myapp by typing 'from myapp.models import Model_Name'

Create a variable to store Model ' a = Blog(name=' ' ,tagline=' ') and to save it type 'a.save()'

How to use QuerySet in Django ?
In the django shell enter below lines of code :

# 1. Retrieve all objects :
from myapp.models import Blog

Retrieve all objects from the database
queryset = Blog.objects.all()
Output:
<QuerySet [<Blog: My blog>, <Blog: Food>, <Blog: second blog>, <Blog: third blog>, <Blog: fourth blog>]>

# 2. Filter objects based on specific criteria :

Filter objects based on a field value
queryset = Blog.objects.filter(field=value) #(tagline__startswith="this")

You can chain multiple filters together
queryset = Blog.objects.filter(field1=value1, field2=value2)
Output :
 <QuerySet [<Blog: My blog>, <Blog: Food>, <Blog: second blog>]>

# 3. Retrieve a single object :

Get a single object matching the query
object = Blog.objects.get(field=value)

# 4. Sort the queryset :

Order the queryset based on a field
queryset = Blog.objects.order_by('field')

Order by multiple fields
queryset = Blog.objects.order_by('field1', 'field2')

# 5. Limit the number of results :

Retrieve a specific number of objects
queryset = Blog.objects.all()[:5]  # Retrieves the first 5 objects

# 6. Perform aggregations :

from django.db.models import Count, Sum, Avg

Count the number of objects matching the query
count = MyModel.objects.filter(field=value).count()

Perform sum or average calculations on a field
total = MyModel.objects.aggregate(Sum('field'))
average = MyModel.objects.aggregate(Avg('field'))

# 7. Access related objects :

Access related objects using the relationship field
queryset = MyModel.objects.filter(related_model__field=value)

Retrieve related objects using reverse relationships
related_queryset = related_model_instance.my_model_set.all()

These are just a few examples of how to use QuerySets in Django. The ORM provides many more methods and options for querying, filtering, and manipulating data. For more information and detailed usage, refer to the Django documentation on QuerySets: 

https://docs.djangoproject.com/en/3.2/topics/db/queries/

# Web development

Python has several frameworks available for all of your various web development tasks. We will look at some of the more popular ones

With the content and the bulk of the computing hosted on a server, a web application can better guarantee a consistent experience for the end user. The popular Django framework provides a very complete environment of plugins and works on the DRY principle (Don't Repeat Yourself). Because of this, you should be able to build your web application very quickly. Since Django is built on Python, you should be able to install it with "sudo pip install Django". Most distributions should have a package for Django, too. Depending on what you want to do with your app, you may need to install a database like MySQL or postgresql to store your application data.

There are Django utilities available to automatically generate a starting point for your new project's code:

```
django-admin startproject newsite
```

This command creates a file named "manage.py" and a subdirectory named "newsite". The file "manage.py" contains several utility functions you can use to administer your new application. The newly created subdirectory contains the files "__init__.py", "settings.py", "urls.py" and "wsgi.py". These files and the subdirectory they reside in comprise a Python package that gets loaded when your web site is started up. The core configuration for your site can be found in the file "settings.py". The URL declarations, basically a table of contents for your site, are stored in the file "urls.py". The file "wsgi.py" contains an entry point for WSGI-compatible web servers.

Once your application is done, it should be hosted on a properly configured and hardened web server. But, this is inconvenient if you are in the process of developing your web application. To help you out, Django has a web server built into the framework. You can start it up by changing directory to the "newsite" project directory and running the following command:

![](bbox=[0.1, 0.7, 0.42, 0.95])

![](bbox=[0.42, 0.25, 0.88, 0.45])

Left Python interpreters work with your databases to power a web server

Bottom The Model-View-Controller architecture is often used for UIs

```
python manage.py runserver
```

This will start up a server listening to port 8000 on your local machine. Because this built in server is designed to be used for development, it automatically reloads your Python code for each request. This means that you don't need to restart the server to see your code changes.

All of these steps get you to a working project. You are now ready to start developing your applications. Within the "newsite" subdirectory, you can type:

```
python manage.py startapp newapp
```

This will create a new subdirectory named "newapp", with the files "models.py", "tests.py" and "views.py", among others. The simplest possible view consists of the code:

```
from django.http import HttpResponse
def index(request):
    return HttpResponse("Hello world!")
```

This isn't enough to make it available, however. You will also need to create a URLconf for the view. If the file "urls.py" doesn't yet exist.py, create it and then add the code:

```
from django.conf.urls import url
from   import views
urlpatterns = [ url(r'^*$', views.index,
    name='index'), ]
```

The last step is to get the URL registered within your project. You can do this with the code

```
from django.conf import include, url
from django.contrib import admin
urlpatterns = [ url(r'^newapp/',
    include('newapp.urls')),
]
```

# Virtual environments

When you start developing your own applications, you may begin a descent into dependency hell. Several Python packages depend on other Python packages. This is its strength, but also its weakness. Luckily, you have virtualenv available to help tame this jungle.

You can create new virtual Python packages depend on other Python packages. This is its strength, but also its weakness. Luckily, you have virtualenv available to help tame this jungle.

You can create new virtual Python environments for each of your projects. Thankfully with this, you create to capture all of the dependencies for your own package
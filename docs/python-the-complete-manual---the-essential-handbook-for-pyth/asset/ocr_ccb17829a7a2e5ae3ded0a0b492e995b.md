# Introducing Python

Make web apps with Python

# What you'll need…

Python 2.7:
https://www.python.org/download/
release-2.7/

Django version 1.4:
https://www.djangoproject.com/

# # Make web apps with Python

Python provides quick and easy way to build applications, including web apps. Find out how to use it to build a feature-complete web app

Python is known for its simplicity and capabilities. At this point it is so advanced that there is nothing you cannot do with Python, and conquering the web is one of the possibilities. When you are using Python for web development you get access to a huge catalogue of modules and community support – make the most of them.

Web development can be done in many different ways, right from using the plain old CGI modules to utilising groomed web frameworks. Using the latter is the most popular method of building web applications with Python, since it allows you to build applications without worrying about all that low-level implementation stuff. There are many web frameworks available for Python, such as Django, TurboGears and Web2Py. For this tutorial we will use our current preferred option, Django.

# ## The Django Project magazine issue tracker

01 The django-admin.py file is used to create new Django projects. Let's create one for our issue tracker project...

In Django, a project represents the site and its settings. An application, on the other hand, represents a specific feature of the site, like blogging or tagging. The benefit of this approach is that your application becomes

portable and can be integrated with other Django sites with very little effort.

```
$ django-admin.py startproject issueTracker
```

A directory will be created. This will also act as the root of your development web server that contains Django. Under the project directory you will find the following items:

**manage.py**: Python script to work with your project.

ludissueTracker: A Python package (a directory with __init__.py file for)

![](bbox=[0.293, 0.933, 0.323, 0.963])
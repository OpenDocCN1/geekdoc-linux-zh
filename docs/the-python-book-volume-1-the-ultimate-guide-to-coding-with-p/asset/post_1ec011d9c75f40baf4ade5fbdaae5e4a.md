
## Python essentials

### 07 Creating the public user interface for ludissues

At this point, the admin interface is working. But we need a way to display the data that we have added using the admin interface. But there is no public interface. Let’s create it now.

We will have to begin by editing the main urls.py (`ludissueTracker/urls.py`).

```python
urlpatterns = patterns('',
    (r'^', include('ludissues.urls')),
    (r'^admin/', include(admin.site.urls)),
)
```

This ensures that all the requests will be processed by `ludissues.urls` first.

### 08 Creating `ludissues.urls`

Create a `urls.py` file in the app directory (`ludissues/urls.py`) with the following content:

```python
from django.conf.urls import patterns, include, url
# use ludissues model
from models import ludissues
```

```python
# dictionary with all the objects in ludissues
info = {
    'queryset': ludissues.objects.all(),
}
```

```python
# To save us writing lots of Python code
# we are using the list_detail generic view

# list_detail is the name of the view we are using
urlpatterns = patterns('django.views.generic.list_detail',
    # issue-list and issue-detail are the template names
    # which will be looked in the default directories
    url(r'^$', object_list, info, name='issue-list'),
    url(r'^(?P<object_id>\d+)/$', object_detail, info, name='issue-detail'),
)
```

To display an issue list and details, we are using a Django feature called generic views. In this case we are using views called list and details. This allows us to create an issue list view and issue detail view. These views are then applied using the `issue_list.html` and `issue_detail.html` templates. In the following steps we will create the template files.

### 09 Setting up template and media directories

In this step we will create the template and media directories. We have already mentioned the template directory as `TEMPLATE_DIRS = (get_abs_path('templates'))`.

Which translates to `ludissueTracker/ludissueTracker/templates/`. Since we will be accessing the templates from the `ludissues` app, the complete directory path would be `ludissueTracker/ludissueTracker/templates/ludissues`. Create these folders in your project folder.

Also, create the directory `ludissueTracker/ludissueTracker/media/` for holding the CSS file. Copy the `style.css` file from the resources directory of the code folder.

To serve files from this folder we need to make it available publicly. To do that, open `settings.py` and add the following lines in `ludissueTracker/urls.py`:

```python
from django.conf.urls import patterns, include, url
from django.conf import settings
# Uncomment the next two lines to enable the admin:
from django.contrib import admin
admin.autodiscover()

urlpatterns = patterns('',
    (r'^', include('ludissues.urls')),
    (r'^admin/', include(admin.site.urls)),
    (r'^media/(?P<path>.*)$', 'django.views.static.serve',
        {'document_root': settings.MEDIA_ROOT}),
)
```

### Admin homepage

Click the Add button next to Issues. Here you will notice that you can enter Owner, Status and Summary for the issue, but what about the `opened_on` and `modified_on` fields that we defined while modelling the app? They are not here because they are not supposed to be entered by the user. `opened_on` will automatically be set to the date/time it is created and `modified_on` will automatically be set to the date/time on which an issue is modified.

Another cool thing is that the owner field is automatically populated with all the users inside the site.

We have defined our list view to show ID, name, status, owner and 'modified on' in the model. You can get to this view by navigating to `http://localhost:8000/admin/ludissues/issue/`.

### The 'Add issue' menu

### The list view for issues

![](img/3b256f430f51c98f1315671f6e4eec19_63_0.png)

![](img/3b256f430f51c98f1315671f6e4eec19_63_1.png)

![](img/3b256f430f51c98f1315671f6e4eec19_63_2.png)

### 10 Creating the template files

Templates will be loaded from the `ludissueTracker/ludissueTracker/templates` directory. In Django, we start with the `ludissueTracker/ludissueTracker/templates/base.html` template. Think of it as the master template which can be inherited by slave ones.

`ludissueTracker/ludissueTracker/templates/base.html`

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html>
<head>
<title>{% block title %}{% endblock %} | LUD Issues</title>
<link rel="stylesheet" href="{{ MEDIA_URL }}style.css" type="text/css" media="screen" />
</head>
<body>
<div id="hd">
<h1>LUD Issue Tracker</h1>
</div>
<div id="mn">
<ul>
<li><a href="{% url issue-list %}" class="sel">View Issues</a></li>
<li><a href="/admin/">Admin Site</a></li>
</ul>
</div>
<div id="bd">
{% block content %}
{% endblock %}
</div>
</body>
</html>
```

`{{ variableName }}` represents a Django variable. `{% block title %}` represents blocks. Contents of a block are evaluated by Django and are displayed. These blocks can be replaced by the child templates.

![](img/3b256f430f51c98f1315671f6e4eec19_64_0.png)

The magazine Issue Tracker in action – list of issues

Now we need to create the `issue_list.html` template. This template is responsible for displaying all the issues available in the system.

`ludissueTracker/ludissueTracker/templates/ludissues/issue_list.html`

```html
{% extends 'base.html' %}
{% block title %}View Issues - {% endblock %}
{% block content %}
<table cellspacing="0" class="column-options">
<tr>
<th>Issue</th>
<th>Description</th>
<th>Status</th>
<th>Owner</th>
</tr>
{% for issue in object_list %}
<tr>
<td><a href="{% url issue-detail issue.id %}">{{ issue.id }}</a></td>
<td><a href="{% url issue-detail issue.id %}">{{ issue.name }}</a></td>
<td>{{ issue.status }}</td>
<td>{{ issue.owner }}</td>
</tr>
{% endfor %}
</table>
{% endblock %}
```

Here we are inheriting the `base.html` file that we created earlier. `{% for issue in object_list %}` runs on the object sent by the `urls.py`. Then we are iterating on the `object_list` for `issue.id` and `issue.name`.

Now we will create `issue_detail.html`. This template is responsible for displaying the detail view of a case.

`ludissueTracker/ludissueTracker/templates/ludissues/issue_detail.html`

```html
{% extends 'base.html' %}
{% block title %}Issue #{{ object.id }} - {% endblock %}
{% block content %}
<h2>Issue #{{ object.id }} <span>{{ object.status }}</span></h2>
<div class="issue">
<h2>Information</h2>
<div class="date">
<p class="cr">Opened {{ object.opened_on }} ago</p>
<p class="last">Last modified {{ object.modified_on }} ago</p>
</div>
<div class="clear">&nbsp;</div>
<div class="block right">
<p class="ass title">Owner</p>
<p class="ass">{{ object.owner }}</p>
</div>
<div class="clear">&nbsp;</div>
<div class="block">
<p class="des title">Summary</p>
<p class="des">{{ object.summary }}</p>
</div>
</div>
{% endblock %}
```

And that's everything! The issue tracker app is now complete and ready to use. You can now point your browser at `localhost:8000` to start using the app.

# 10 Creating the template files

Templates will be loaded from the ludissueTracker/ludissueTracker/templates directory. In Django, we start with the ludissueTracker/ludissueTracker/templates/base.html template. Think of it as the master template which can be inherited by slave ones.

```
urls)),
(r'^media/(?P<path>.*)$', 'django.views.static.serve',
{'document_root': settings.MEDIA_ROOT})
```

```
ludissueTracker/ludissueTracker/templates/base.html
```

```
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

({{ variableName }}) represents a Django variable. {% block title %} represents blocks. Contents of a block are evaluated by Django and are displayed. These blocks can be replaced by the child templates.

![](bbox=[0.35, 0.27, 0.88, 0.52])

The magazine Issue Tracker in action – list of issues

Now we need to create the issue_list.html template. This template is responsible for displaying all the issues available in the system.

```
ludissueTracker/ludissueTracker/templates/ludissues/issue_list.html
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

Here we are inheriting the base.html file that we created earlier. {% for issue in object_list %} runs on the object sent by the urls.py. Then we are iterating on the object_list for issue.id and issue.name.

Now we will create issue_detail.html. This template is responsible for displaying the detail view of a case.

```
ludissueTracker/ludissueTracker/templates/ludissues/issue_detail.html
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
<div class="block #49 right">
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

And that's everything! The issue tracker app is now complete and ready to use. You can now point your browser at localhost:8000 to start using the app.
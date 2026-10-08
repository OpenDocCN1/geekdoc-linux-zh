# Introducing Python

# Make web apps with Python

objects in ludicules
info = {

```
  'queryset':ludicules.
objects.all(),
```

# We use lists out of
python code
# We are using the list-
det view generic

```
# listdetail is the name of
view we are using
urlpatterns =
patterns='django.views.generic.
list_detail',
#list-issue and issue-
#are the template names
# Which will be linked in the
default template
directories={
  'object_name':'object',
  list_name='list_info',
  url='<id>/<object>',
  detail_name='item-detail',
```

To display an list and details,
we are using a Django featured
generic views. In this case we
allow us to create an list and
detail view. These views are
then applied when using the list.html
and detail.html template. In the\following steps we will create the
template files.

# Setting up template and
media directories

09 In this step we will create the
template and media directories.
Have already mentioned the
template directory as
TEMPLATE_DIRS =

```
  getpath('templates')
```

Which translates to ludiscaletracker/
ludiscaletracker/templates/ Since
we are deicpled
will be accessing the templates
from the apps page, the
complete path would be
ludiscaletracker/ludiscaletracker/
Create these
folder in your project folder.
Also, create the
ludiscaletracker/ludiscaletracker/media/
for handling the CSS file. You can
serve css from resources directory
of the code folder. To serve files from
it, make it available by.
Open settings.py and add these lines in
ludiscaletracker/ludiscaletracker/urls.py:

```
In Django, we start with the
ludiscaletracker/ludiscaletracker/
tamples/base.html. Think of
is as the master template which can
enabled by slave owners.
ludiscaletracker/ludiscaletracker/
tamples.base
<!DOCTYPE HTML />
<HYPERLINK="http://
w.w3.org/TR/HTML1/Strict.EN"
dtd"="http://www.w3.org/
html1/xhtml1-strict.dtd">
<head>
<title>{%list block title
)%%block %LUD Issues%
</title>
<link rel="stylesheet"
href=((MEDIA_URL))}.style.class"
type="text/css" media="screen"
/>
</head>
<body>
<div id="head">
<h1>Issue
Tracker/<span></h1>\</div>
<div id="mn">
<ul>
<Li><a href="{% url list-issue
%}" class="View Issues
a</a></li>
</ul>
</div>
<div id="bd">
{% content block %}
</div>
</div>
</body>
</html>
```

# We connect the next
lines to enable the admin
from django.contrib import
admin.autodiscover(

```
urlpatterns = patterns(
(r'\(', include('ludicules.urls'))),
(r'admin/', include(admin.site.urls)),
(r'media/', static/\/(?P<path>.*), django.views.static.serve,

    'document_root': settings.
MEDIA_ROOT})
))
```

# Creating the template files

10 Templates will be loaded
from the ludiscaletracker/
ludiscaletracker/templates.

# “To display an list and details here,
we are using a Django featured called
generics”

![](bbox=[0.285, 0.932, 0.325, 0.972])
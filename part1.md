# Part 1: Requests and responses
Create Django Project.

```bash
django-admin startproject mysite
```

To run:
```bash
python manage.py runserver
```

To create a web app under the project

```bash
python manage.py startapp polls
```

> An app is a Web application that does something – e.g., a Weblog system, a database of public records or a simple poll app. A project is a collection of configuration and apps for a particular website. A project can contain multiple apps. An app can be in multiple projects.

## Creating a View based on function
Bottom Up Approach.

- Function that will be accessed from a View in a web app
- A `urls.py` file under the web app that will describe how it will route incoming requests to a function
- A `urls.py` file under the project that will describe how it will route incoming requests to a web app

Create a function under view that will be accessed as URL

```python
from django.http import HttpResponse
from django.shortcuts import render

# Create your views here.
def index(request):
    return HttpResponse("Hello World!")
```

For routing to web app functions:

```python
'''Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
'''
from django.conf.urls import url
from . import views

urlpatterns = [
    '''
    the first part is the regular expression that matches incoming request
    the second parameter describes which function to go to from view
    the third parameter describes the namespace of the URL for reverse usage. it is unclear as of now.
    '''
    url(r'^$', views.index, name='index'),
]

```

For routing to web app from project:

```python
'''
Including another URLconf
    1. Import the include() function: from django.conf.urls import url, include
    2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
'''
from django.conf.urls import url, include
from django.contrib import admin

urlpatterns = [
    url(r'^polls/', include('polls.urls')),
    url(r'^admin/', admin.site.urls),
]
```

Blog Project / blogs App 
========================================================

Create an app called blogs in the project.

* Quit the server with CONTROL-C. Create an app called blogs.
```shell
python manage.py startapp blogs
```

* Edit the settings file and add the blogs app 
```python3
# blog_prj/settings.py
INSTALLED_APPS = [
    "blogs",    # new
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
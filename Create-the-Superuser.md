Blog Project / Superuser 
========================================================

* Create a superuser for the project, and use the admin site to make a couple of short posts. 

```shell
python manage.py createsuperuser
```

* Register model 
```python3
# blogs/admin.py
from django.contrib import admin

from .models import BlogPost

admin.site.register(BlogPost)
```

* Run the Django development server again.
```shell
python manage.py runserver
```

* Use the admin site to make a couple of short posts.

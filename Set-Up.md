Blog Project / Set Up 
========================================================

Start a new Django project called blog. 

* Make a new directory called blog.

```shell
mkdir blog
```

* Create a virtual environment within this new directory. 

```shell
python -m venv .venv
```

* Activate the virtual environment called .venv
```shell
source .venv/bin/activate
```

* Install Django
```shell
pip install django
```

* Start a new Django project called blog_prj. Don't forget to add the period (or dot) . at the end!
```shell
django-admin startproject blog_prj .
```

* Create the database
```shell
python manage.py migrate
```

* Run the Django development server
```shell
python manage.py runserver
```

* Quit the server with CONTROL-C. 

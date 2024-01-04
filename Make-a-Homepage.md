Blog Project / Homepage
========================================================

* Make a home page that shows all posts in chronological order.

* Edit the urls.py in the project file
```python3
# blog_prj/urls.py
from django.contrib import admin
from django.urls import path, include  # new

urlpatterns = [
    path('admin/', admin.site.urls),
    path("", include("blogs.urls"))  # new
]
```

* Create a second urls.py file within the blogs folder.
```python3
# blogs/urls.py
from django.urls import path

from . import views

app_name = "blogs"

urlpatterns = [
    # Home page
    path("", views.index, name="index"),
    # Display all blog posts
    path("blogposts/", views.blog_posts, name="blog_posts"),
    # Display single blog post
    path("blogposts/<int:blog_post_id>/", views.blog_post, name="blog_post"),
]
```

* Write the views

```python3
# blogs/views.py
from django.shortcuts import render, get_object_or_404

from .models import BlogPost

def index(request):
    """The home page."""
    return render(request, "blogs/index.html")

def blog_posts(request):
    """Display all blog posts."""
    blog_posts = BlogPost.objects.order_by("date_added")
    context = {"blog_posts": blog_posts}
    return render(request, "blogs/blog_posts.html", context)

def blog_post(request, blog_post_id):
    blog_post = get_object_or_404(BlogPost, id=blog_post_id)
    blog_content = blog_post.text
    context = {"blog_post": blog_post, "blog_content": blog_content}
    return render(request, "blogs/blog_post.html", context)
```

* Write the template files. Inside the blogs folder, make a new folder called templates. Inside the templates folder, make another folder called blogs. 

```html
<!-- blogs/base.html -->
<!doctype html>
<html lang ="en">
  <head>
    <title>Blog</title>
  </head>
  <body>
 <p><a href="{% url 'blogs:index' %}">Home Page</a></p>
 <p><a href="{% url 'blogs:blog_posts' %}">Blog Posts</a></p>

{% block page_header %}{% endblock page_header %}

{% block content %}{% endblock content %}
        
</body>
</html>
```

```html
<!-- blogs/index.html -->
{% extends 'blogs/base.html' %}

{% block page_header %}
<h1>Blogs for All</h1>    
<p>This blog allows users to write about any subject they want.</p>
<p>Explore the <a href="{% url 'blogs:blog_posts' %}">Blog Posts.</a> </p>
{% endblock page_header %}
```
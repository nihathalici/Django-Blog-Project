Blog Project / Forms
========================================================

Create a form for making new posts and another for editing existing posts. Fill in your forms to make sure they work.

* Inside the blogs folder, create a new file forms.py

```python3
# blogs/forms.py
from django import forms

from .models import BlogPost

class BlogPostForm(forms.ModelForm):
    class Meta:
        model = BlogPost
        fields = ["title", "text"]
        labels = {"title": "", "text": ""}
        widgets = {"text":forms.Textarea(attrs={"cols":80})}
```

* Add the URL

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
    # Adding new blog post
    path("newblogpost/", views.new_blog_post, name="new_blog_post"),  # new
]
```

* Write the view
```python3
# blogs/views.py
from django.shortcuts import render, get_object_or_404, redirect  # new
from .forms import BlogPostForm  # new

def new_blog_post(request):
    """Add a new blog post."""
    if request.method != "POST":
        form = BlogPostForm()
    else:
        form = BlogPostForm(data=request.POST)
        if form.is_valid():
            form.save()
            return redirect("blogs:blog_posts")
    context = {"form": form}
    return render(request, "blogs/new_blog_post.html", context)
```

* Write the template
```html
# templates/blogs/new_blog_post.html
{% extends 'blogs/base.html' %}

{% block page_header %}
<h3>Add a new blog post:</h3>    
{% endblock page_header %}

{% block content %}
<form action="{% url 'blogs:new_blog_post' %}" method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button name="submit">Add new blog post</button>
</form>
{% endblock content %}
```

* Next step is creating another form for editing existing posts.

* Begin with adding the URL

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
    # Adding new blog post
    path("newblogpost/", views.new_blog_post, name="new_blog_post"),
    # Editing blog post
    path("blogposts/<int:blog_post_id>/editblogpost/", views.edit_blog_post, name="edit_blog_post"), 
]
```


* Write the view

```python3
# blogs/views.py

def edit_blog_post(request, blog_post_id):  # new
    """Editing blog post."""
    blog_post = BlogPost.objects.get(id=blog_post_id)
    if request.method != 'POST':
        form = BlogPostForm(instance=blog_post)
    else:
        form = BlogPostForm(instance=blog_post, data=request.POST)
        if form.is_valid():
            form.save()
            return redirect("blogs:blog_post", blog_post_id = blog_post.id)
    context = {"blog_post": blog_post, "form": form}
    return render(request, "blogs/edit_blog_post.html", context)
    ```

* Write the template
```html
# templates/blogs/edit_blog_post.html
{% extends 'blogs/base.html' %}

```
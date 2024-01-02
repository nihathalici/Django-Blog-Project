Blog Project / Model 
========================================================

* Create a model called BlogPost for the blogs app. The model should have fields like title, text, and date_added. 

```python3
from django.db import models

class BlogPost(models.Model):
    """App for adding new blog posts."""
    title = models.CharField(max_length=200)
    text = models.TextField()
    date_added = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        """Return a string representation of the model."""
        return self.title

```

* Refresh the database
```shell
python manage.py makemigrations blogs

python manage.py migrate 
```


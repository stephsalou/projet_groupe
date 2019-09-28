

### IMPORTATION
```python
from django.db import models
from django.contrib.auth.models import User
from [app/modelProfile] import Profile
```

### MODEL BLOG
- category
```python
class Category(models.Model):
    titre = models.CharField(max_length=250)
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)
      
    def __str__(self):
       return self.titre

    class Meta:
        verbose_name = 'Category'
        verbose_name_plural = 'Categories'
```
- tags
```python
class Tags(models.Model):
    titre = models.CharField(max_length=250)
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)
        
    def __str__(self):
        return self.titre

    class Meta:
        verbose_name = 'Tags'
        verbose_name_plural = 'Tags'
```
- auteur
```python
class Auteur(models.Model):
    Auteur = models.OneToOneField(User,on_delete= models.CASCADE,related_name="auteur")
    image = models.ImageField(upload_to="image_auteur")
    facebook = models.URLField()
    twitter = models.URLField()
    driblle = models.URLField()
    beef = models.URLField()
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)
      
    def __str__(self):
        pass

    class Meta:
       
        verbose_name = 'Auteur'
        verbose_name_plural = 'Auteurs'
```

- article
```python 
class Article(models.Model):
    auteur = models.ForeignKey(Auteur,on_delete= models.CASCADE, related_name="Auteur_article")
    titre = models.CharField(max_length=250)
    description = models.TextField()
    contenue = models.TextField()
    image = models.ImageField(upload_to="images_article")
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_uod = models.DateTimeField(auto_add=True)
        
      
    def __str__(self):
        return self.titre

    class Meta:
        verbose_name = 'Article'
        verbose_name_plural = 'Articles'
````

- souscription 
```python
class Souscription(models.Model):
    email = models.EmailField()
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    def __str__(self):
     return self.email

    class Meta:
        verbose_name = 'Souscription'
        verbose_name_plural = 'Souscriptions'
```


- Like
```python 

class Like(models.Model):
    user = models.ForeignKey('Profile',on_delete= models.CASCADE, related_name="profile_mike")
    article_id = models.ForeignKey(User,on_delete= models.CASCADE, related_name="Auteur_Like")
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)

    def __str__(self):
         return self.email

    class Meta:
        verbose_name = 'Like'
        verbose_name_plural = 'Likes'
```


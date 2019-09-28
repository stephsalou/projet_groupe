

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
    date_upd = models.DateTimeField(auto_add=True)
        
      
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
    date_upd = models.DateTimeField(auto_add=True)
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
    date_upd = models.DateTimeField(auto_add=True)
    def __str__(self):
         return self.email

    class Meta:
        verbose_name = 'Like'
        verbose_name_plural = 'Likes'
```

### MODELE ARCHITECTURE
- client
```python

class Client(models.Model):
    """Model definition for Client."""
    user = models.OneToOneField(User,on_delete= models.CASCADE,related_name="client")
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)
    

    class Meta:
        """Meta definition for Client."""

        verbose_name = 'Client'
        verbose_name_plural = 'Clients'

    def __str__(self):
        """Unicode representation of Client."""
        return '{}'.format(self.user ) # TODO


```

- category 
```python 


class Category(models.Model):
    """Model definition for Category."""
    titre = models.CharField(max_length=50)
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)

    class Meta:
        """Meta definition for Category."""

        verbose_name = 'Category'
        verbose_name_plural = 'Categories'

    def __str__(self):
        """Unicode representation of Category."""
        return '{}'.format(self.titre ) # TODO

```

- projet

```python

class Projet(models.Model):
    """Model definition for Projet."""
    image = models.ImageField(upload_to='projet_image')
    titre = models.CharField(max_length=50)
    description = models.TextField()
    content = HTMLField()
    client = models.ForeignKey(Client, on_delete=models.CASCADE,related_name='client_projet')
    date_debut = models.DateTimeField()
    date_fin = models.DateTimeField()
    architect = models.ForeignKey('Architect', on_delete=models.CASCADE,related_name='archotect_projet')
    lieux = models.CharField(max_length=50)
    lien = models.URLField(max_length=200)
    galerie = models.ForeignKey('Galerie', on_delete=models.CASCADE,related_name='galerie_projet')
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)

    class Meta:
        """Meta definition for Projet."""

        verbose_name = 'Projet'
        verbose_name_plural = 'Projets'
        
    def __str__(self):
        """Unicode representation of Projet."""
        return '{}'.format(self.titre ) # TODO

````

- architect

```python
class Architect(models.Model):
    """Model definition for Architect."""

    user =  models.OneToOneField(User,on_delete=models.CASCADE,related_name='architect')
    image = models.ImageField(upload_to='architect')
    job = models.ForeignKey('Poste', on_delete=models.CASCADE,related_name='architect_job')
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)
    class Meta:
        """Meta definition for Architect."""

        verbose_name = 'Architect'
        verbose_name_plural = 'Architects'

    def __str__(self):
        """Unicode representation of Architect."""
        return '{}'.format(self.user ) # TODO



class Poste(models.Model):
    """Model definition for Poste."""
    titre = models.CharField(max_length=50)
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)

    class Meta:
        """Meta definition for Poste."""

        verbose_name = 'Poste'
        verbose_name_plural = 'Postes'

    def __str__(self):
        """Unicode representation of Poste."""
        return '{}'.format(self. ) # TODO

```
- galerie
```python
class Galerie(models.Model):
    """Model definition for Galerie."""

    img_grand = models.ImageField(upload_to='galerie/img')
    img_petit_1 = models.ImageField(upload_to='galerie/img')
    img_petit_2= models.ImageField(upload_to='galerie/img')
    img_petit_3 = models.ImageField(upload_to='galerie/img')
    img_petit_4 = models.ImageField(upload_to='galerie/img')
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)
    class Meta:
        """Meta definition for Galerie."""

        verbose_name = 'Galerie'
        verbose_name_plural = 'Galeries'



```

### CONTACT


- message 

```python
# Create your models here.
class Message(models.Model):
    """Model definition for Message."""
    nom = models.CharField(max_length=250)
    prenoms = models.CharField(max_length=250)
    sujet = models.CharField(max_length=250)
    email = models.EmailField()
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)


    # TODO: Define fields here

    class Meta:
        """Meta definition for Message."""

        verbose_name = 'Message'
        verbose_name_plural = 'Messages'

```

- souscription

```python
class Souscription(models.Model):
    email = models.EmailField()
    status = models.BooleanField(default=True)
    date_add = models.DateTimeField(auto_now_add=True)
    date_upd = models.DateTimeField(auto_add=True)
    def __str__(self):
        return self.email

    class Meta:
        verbose_name = 'Souscription'
        verbose_name_plural = 'Souscriptions'
```

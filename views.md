### BLOG VIEWS

```python
from django.shortcuts import render
from .models import *
from django.core.paginator import Paginator
from django.utils.timezone import P_NOWAIT
# Create your views here.

def blog_home(request):
    q=request.GET.get('query',False)
    page = request.GET.get('page',False)
    if q:
        articles = Article.objects.filter(titre__contains=q)
    else:
        articles = Article.objects.filter(status=True)
    art_recent = Article.objects.filter(date_lt = now())

    category = Category.objects.filter(status=True)
    article = Paginator(articles,5)
    art = article.page(page)
    data = {
        'art_recent':art_recent,
        'category':category,
        'articles':article
    }
    return render(request, 'pages/blog/accueil_blog.html',data)


def single_blog(request,id):
    art_recent = Article.objects.filter(date_lt = now())
    tags = Tag.objects.filter(status=True)
    category = Category.objects.filter(status=True)
    article = Article.objects.get(pk=id)
    data={
        'art_recent':art_recent,
        'tags':tags,
        'category':category,
        'article':article
    }

    return render(request, 'pages/blog/single_blog.html',data)
 ```
 
 ### ARCHITECTURE VIEWS
 
 ```python 
 
 from django.shortcuts import render
from .models import *
from django.core.paginator import Paginator
# Create your views here.


def home(request):
    about = About.objects.filter(status=True)[:1]
    service = Service.objects.filter(status=True)[:1]
    Project = Project.objects.filter(status=True)[:6]
    post = Article.objects.filter(status=True)[:3]

    data= {
        'about':about,
        'service':service,
        'project':Project,
        'post':post
    }
    return render(request, 'pages/architectures/index.html',data)


def about_architec(request):
    about = About.objects.filter(status=True)[:1]
    post = Article.objects.filter(status=True)[:3]
    data= {
        'about':about,
        'post':post
    }
    return render(request, 'pages/architectures/abouts.html')

def project_architec(request):
    projet = Project.objects.filter(status=True)
    architect = Achitect.objects.filter(status=True)
    data = {
        'architect':architect,
        'projet':projet
    }
    return render(request, 'pages/architectures/project.html',data)

def single_architec(request):
    architect = Achitect.objects.filter(status=True)
    projet = Project.objects.filter(status=True)
    data = {
        'architect':architect,
        'projet':projet
    }
    return render(request, 'pages/architectures/single_project.html')

def service_architec(request):
    service = Service.objects.filter(status=True)[:6]
    data={
        'servcice':service
    }
    return render(request, 'pages/architectures/services.html',service)
 
 ```


### Profile views

```python

from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login, logout
from django.contrib.auth.decorators import login_required


def connexion(request):
    username = request.POST.get('username', False)
    password = request.POST.get('password', False)

    next = request.POST.get('next', False)
    user = authenticate(username=username, password=password)
    
    if user is not None and user.is_active:
        login(request, user)
        if next: 
            return redirect(next)
        else:
            return redirect('home')
    else:
        return render(request, 'pages/login.html')  # page login -----_____---- a travailler le .html
        

def deconnexion(request):
    logout(request)
    return redirect('mylogin') 
 
 ```
 
 ### CONTACT 
 - contact form 
 ```python
from django.forms import ModelForm
from .models import *


class ContactForm(ModelForm):
    class Meta:
        model = Contact
        fields = ['nom', 'prenoms', 'sujet','email','status','date_add','date_upd']


 
class NewsletterForm(ModelForm):
    class Meta:
        model = Comment
        fields = ['email',]
 
 ```
 
 
 ```python
 from django.shortcuts import render
from .models import *
from .fomrs import *

# Create your views here.

def message(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
            if form.is_valid():
                model = form.save()
                return redirect('/')
    return render(request, "my_template.html")



def newsletter(request):
    if request.method == 'POST':
        form = NewsletterForm(request.POST)
            if form.is_valid():
                model = form.save()
                return redirect('/')
    return render(request, "my_template.html")

    
 ```

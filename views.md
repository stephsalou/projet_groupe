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

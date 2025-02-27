**Documentation**

Use ORM to setup database structure and relationships.Perform CRUD operations too.

**Tech Stack**

Backend(Django)

Database(PostgreSQL)

**Project Structure**

myproject/

├── myproject/

│   ├── \_\_init\_\_.py

│   ├── asgi.py

│   ├── settings.py

│   ├── urls.py

│   ├── wsgi.py

├── myapp/

│   ├── migrations/

│   │   ├── \_\_init\_\_.py

│   │  └──

│   ├── \_\_init\_\_.py

│   ├── admin.py

│   ├── apps.py

│   ├── models.py

│   ├── tests.py

│   ├── views.py

├── manage.py

├── db.sqlite3(or your PostgreSQL database)

├──requirements.txt

├── .gitignore

**Step-By-Step Implementation**

1.     Define your application and Database in settings.py

Django settings for myprojectproject.

"""

from pathlib import Path

\# Build paths inside the project like this: BASE\_DIR /'subdir'.

BASE\_DIR = Path(\_\_file\_\_).resolve().parent.parent

\# Quick-start development settings - unsuitable forproduction

\# Seehttps://docs.djangoproject.com/en/5.1/howto/deployment/checklist/

\# SECURITY WARNING: keep the secret key used in productionsecret!

SECRET\_KEY ='django-insecure-\_t4s!aj\_yeej642hu742(q78%w#vcmnca!t00#-tfzuebi(r!!'

\# SECURITY WARNING: don't run with debug turned on inproduction!

DEBUG = True

ALLOWED\_HOSTS = \[\]

\# Application definition

INSTALLED\_APPS = \[

   'django.contrib.admin',

   'django.contrib.auth',

   'django.contrib.contenttypes',

   'django.contrib.sessions',

   'django.contrib.messages',

   'django.contrib.staticfiles',

    'myapp',

\]

MIDDLEWARE = \[

    'django.middleware.security.SecurityMiddleware',

   'django.contrib.sessions.middleware.SessionMiddleware',

   'django.middleware.common.CommonMiddleware',

   'django.middleware.csrf.CsrfViewMiddleware',

   'django.contrib.auth.middleware.AuthenticationMiddleware',

   'django.contrib.messages.middleware.MessageMiddleware',

   'django.middleware.clickjacking.XFrameOptionsMiddleware',

\]

ROOT\_URLCONF = 'myproject.urls'

TEMPLATES = \[

    {

        'BACKEND':'django.template.backends.django.DjangoTemplates',

        'DIRS': \[\],

        'APP\_DIRS':True,

        'OPTIONS': {

           'context\_processors': \[

               'django.template.context\_processors.debug',

               'django.template.context\_processors.request',

               'django.contrib.auth.context\_processors.auth',

               'django.contrib.messages.context\_processors.messages',

            \],

        },

    },

\]

WSGI\_APPLICATION = 'myproject.wsgi.application'

\# Database

\# https://docs.djangoproject.com/en/5.1/ref/settings/#databases

DATABASES = {

    'default': {

        'ENGINE':'django.db.backends.postgresql',

        'NAME':'Intern',

        'USER':'postgres',

        'PASSWORD':'Alish@123',

        'HOST':'localhost',

        'PORT': '5432',

    }

}

\# Password validation

#https://docs.djangoproject.com/en/5.1/ref/settings/#auth-password-validators

AUTH\_PASSWORD\_VALIDATORS = \[

    {

        'NAME':'django.contrib.auth.password\_validation.UserAttributeSimilarityValidator',

    },

    {

        'NAME':'django.contrib.auth.password\_validation.MinimumLengthValidator',

    },

    {

        'NAME':'django.contrib.auth.password\_validation.CommonPasswordValidator',

    },

    {

        'NAME':'django.contrib.auth.password\_validation.NumericPasswordValidator',

    },

\]

\# Internationalization

\# https://docs.djangoproject.com/en/5.1/topics/i18n/

LANGUAGE\_CODE = 'en-us'

TIME\_ZONE = 'UTC'

USE\_I18N = True

USE\_TZ = True

\# Static files (CSS, JavaScript, Images)

\# https://docs.djangoproject.com/en/5.1/howto/static-files/

STATIC\_URL = 'static/'

\# Default primary key field type

#https://docs.djangoproject.com/en/5.1/ref/settings/#default-auto-field

DEFAULT\_AUTO\_FIELD = 'django.db.models.BigAutoField'

2.     Create models in models.py

from django.db import models

class Author(models.Model):

    name =models.CharField(max\_length=100)

    email= models.EmailField()

class Books(models.Model):

    title =models.CharField(max\_length=200)

    publication\_date = models.DateField()

    author =models.ForeignKey(Author, on\_delete=models.CASCADE, related\_name='books')

3.     Register models in admin.py

from django.contrib import admin

from .models import Author, Books

admin.site.register(Author)

admin.site.register(Books)

4\. Assign models in Views.py

from django.shortcuts import render

from django.http import JsonResponse

from .models import Author

from django.http import HttpResponse

def home(request):

        returnHttpResponse("Welcome to the Homepage!")

def author\_list(request):

    authors =Author.objects.all().values()

    returnJsonResponse(list(authors), safe=False)

def author\_detail(request, id):

    try:

        author =Author.objects.get(id=id)

        returnJsonResponse({'id': author.id, 'name': author.name, 'email': author.email})

    exceptAuthor.DoesNotExist:

        returnJsonResponse({'error': 'Author not found'}, status=404)

4.     Set pattern in url.py

URL configuration for myproject project.

The \`urlpatterns\` list routes URLs to views. For moreinformation please see:

   https://docs.djangoproject.com/en/5.1/topics/http/urls/

Examples:

Function views

    1. Add animport:  from my\_app import views

    2. Add a URL tourlpatterns:  path('', views.home, name='home')

Class-based views

    1. Add animport:  from other\_app.views import Home

    2. Add a URL tourlpatterns:  path('', Home.as\_view(),name='home')

Including another URLconf

    1. Import theinclude() function: from django.urls import include, path

    2. Add a URL tourlpatterns:  path('blog/',include('blog.urls'))

"""

from django.contrib import admin

from django.urls import path, include

from myapp import views

urlpatterns = \[

    path('admin/',admin.site.urls),

    path('',views.home, name='home'),

    path('authors/',views.author\_list, name='author\_list'),

   path('author//', views.author\_detail,name='author\_detail'),

    \]

**Run the Project**

·      .venv\\Scripts\\activate

·      Runserver with python manage.py runserver

·      Access the server at [https://127.0.0.1:8000](https://127.0.0.1:8000)

·      Perfrom CRUD operations in python shell.py

**CRUD Operation**
![Image](https://github.com/user-attachments/assets/1aa3dad1-c08c-408e-a9f2-44a36b7a24cc)
![Image](https://github.com/user-attachments/assets/d4ceafbf-806c-43e9-aff4-3eb4531eed7a)


**Conclusion:**

This Django app creates arelationship an ER model and updates the database using CRUD.

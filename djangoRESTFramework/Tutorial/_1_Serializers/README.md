# Getting started

## 1. **Setting Django Project RESTframework :**

   * Setting up new Python Environment

      Before starting the project, make sure that you have set up a new Python environment. 

      - for linux
         ```bash
         python -m venv envName
         source envName/bin/activate
         ```

      - for windows
         ```bash
         python -m venv envName
         source envName\Scripts\activate
         ```

   * Create a Django Project :

      ```bash
      django-admin startproject projectNamecd
      cd projectName
      ```

   * Once the Django project is Created, create apps in Django Project Folder :

      ```bash
      django-admin startapp appName
      ```

   * Once apps are created, register all app and restframework in settings.py file inside INSTALLED_APPS list.

      ```py

      INSTALLED_APPS = [
         ...
         # project apps that are created
         'appName',

         # library apps that will be used in Project
         'restframework'
         ...
      ]
      ```
   * Create a model to work with

      Create a simple `appName` model that is used to store code snippets. Go ahead and edit the `appName/model.py` file.
      
      > [!NOTE] Good Programming pratices include comments.

      ```py
      from django.db import models
      from pygments.lexers import get_all_lexers
      from pygments.styles import get_all_styles

      LEXERS = [item for item in get_all_lexers() if item[1]]
      LANGUAGE_CHOICES = sorted([(item[1][0], item[0]) for item in LEXERS])
      STYLE_CHOICES = sorted([(item, item) for item in get_all_styles()])

      class Snap(models.Model):
         created = models.DateTimeField(auto_now_add=True)
         title = models.CharField(max_length=100, blank=True, default='')
         code = models.TextField()
         linenos = models.BooleanField(default=False)
         language = models.CharField(choices=LANGUAGE_CHOICES, default='python', max_length=100)
         style = models.CharField(choices=STYLE_CHOICES, default='friendly', max_length=100)

         def Meta:
            ordering = ['created']
      ```

      After create models, make Migrations and Migrate declared model to reflect changes.

      ```bash
      python manage.py makemigrations
      python manage.py migrate
      ```

## 2. **Using Serializer in Django project :**

   -  The first Thing we need to get started on our Web API is to provide a way of serializing and deserializing the snippet instances into representations such as `json`.

   -  We can do this by declaring serializers that work very similar to Django's forms.
   -  Create a file in the `appName` directory called `serializers.py` and add the Following.

   >  [!INFO]
   >  serializers.py
   
   ```py 
   from restframework import serializers
   
   # import any of the Model that declared and going to be used
   from .models import Snap, LANGUAGE_CHOICES, STYLE_CHOICES

   class Snap(serializers.Serializer):
      id = serializers.IntegerField(read_only=True)
      title = serializers.CharField(required=False, allow_blank=True, max_length=100)
      code = serializers.CharField(style={'base_template': 'textarea.html'})
      linenos = serializers.BooleanField(required=False)
      language = serializers.CharField(choices=LANGUAGE_CHOICES,default='python',max_length=100)
      style = serializers.ChoiceField(choices=STYLE_CHOICES, default='friendly')
   ```


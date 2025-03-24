# Getting started

1. **Setting Django Project RESTframework :**

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

   * Once app is created, register it in settings.py file.

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

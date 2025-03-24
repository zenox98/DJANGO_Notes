# Getting started

1. **Create a django project:**
   
   ```bash
   django-admin startproject projectNamecd
   cd projectName
   ```

2. **Create an App :**

    Once project is Created, create a app in Project Folder
    ```bash
    django-admin startapp appName
    ```
3. **Register Your App in settings :**

    Once app is created, register it in settings.py file
    ```python
    
    INSTALLED_APPS = [
        ...
        # project apps that are created
        'appName',

        # library apps that will be used in Project
        'restframework'
        ...
    ]
    ```

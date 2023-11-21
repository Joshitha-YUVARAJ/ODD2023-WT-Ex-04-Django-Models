# Ex-04-Django-Models
NAME   : Yuvaraj Joshitha

REG NO : 23011447

DEPT   : Artificial Intelligence and  Machine Learning

# AIM

     To create a django model with five users.

     1. Setting  email address for all users.

     2. setting first name and last name for all users.

# Design procedure

# Step1 : Create django project and app

Create django project and app using the following commands:

Django-admin startproject mymodels

Python manage.py startapp myapp

# Step 2: Create a user_profile models in model.py
Add the models in the admin interface using the code in admin.py


# Step 3: Define user creation view

Write the function based view to render the data from the models to the template in view.py

# Step 4: Setup the url 

In settings.py file add the app created.

# Step 5 Create template

Create a template within your app if it doesn't already exist. Inside this directory, create a template named 'user_profiles.html'.

# Step 6 Apply migrations

Now do the migrations process to initiate and save the models

Python mange.py makemigrations

Python manage.py migrate

# Step 7: Run the program 

Run the program using the command

Python manage.py runserver 8000

In the admin/ page you can view the models created

And  in the user_profile template page you can see the profile page of the user.

# CODE:
model.py
```
from django.db import models

from django.contrib.auth.models import User

class UserProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    first_name = models.CharField(max_length=100)
    last_name = models.CharField(max_length=100)
    email = models.EmailField()
```
admin.py
```
from django.contrib import admin

# Register your models here.
from .models import UserProfile

admin.site.register(UserProfile)
```
view.py
```
from django.shortcuts import render
from django.views import View
from django.contrib.auth.decorators import login_required

# Create your views here.
from .models import UserProfile
@login_required
def user_profile(request):
    user = request.user  # Get the currently logged-in user
    user_profile = UserProfile.objects.get(user=user)
    
    context = {
        'user': user,
        'user_profile': user_profile,
        'firstname' : user_profile.first_name,
        'lastname' : user_profile.last_name,
        'email' : user_profile.email ,
    }
    
    return render(request, 'myapp/user_profiles.html', context)
```

urls.py
```
from django.contrib import admin
from django.urls import path
from modelapp import views
from modelapp.views import user_profile

urlpatterns = [
    path('admin/', admin.site.urls),
    path ('profile/', views.user_profile, name='user_profile'),
]
```
template as user_profiles.html
```
<!DOCTYPE html>
<html>
<head>
    <title>User Profile</title>
</head>
<body>
    <h1>User Profile</h1>
    <p><strong>Username:</strong> {{ user.username }}</p>
    <p><strong>First Name:</strong> {{ firstname }}</p>
    <p><strong>Last Name:</strong> {{ lastname }}</p>
    <p><strong>Email:</strong> {{ user.email }}</p>
    <p><strong>Custom Profile Data:</strong> {{ user_profie.custom_field }}</p>
</body>
</html>
```
# Output
![Alt text](<Screenshot 2023-11-09 091722.png>)
# 🌐 Rosokua — Django Web Application

Rosokua is a beginner-friendly Django web application built while following a tutorial. This project serves as a foundational web setup using Django, complete with templates, static files, and app-based structure.

## 📦 Project Overview

- **Framework:** Django (Python)
- **Structure:** Single app (`core`) inside one project (`rosokua`)
- **Templates & Static Files:** Custom HTML, CSS, JS
- **Purpose:** Learn and build a working Django site with homepage (`index.html`)

## ⚙️ Project Setup

### ✅ Create Virtual Environment

```bash
python -m venv .venv
.venv\Scripts\Activate.ps1  # For PowerShell (Windows)
```

### ✅ Install Django

```bash
pip install django
python -m pip install --upgrade pip  # optional upgrade
```

## 🏗️ Create Django Project and App

```bash
django-admin startproject rosokua
cd rosokua
python manage.py startapp core
```

## 🧩 Configure Project Settings

### 🔹 settings.py

```python
# settings.py (partial)

import os
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

INSTALLED_APPS = [
    ...
    'core',
]

TEMP_DIR = BASE_DIR / "templates"
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [TEMP_DIR],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                ...
            ],
        },
    },
]

STATICFILES_DIRS = [BASE_DIR / "static"]
```

## 📁 Directory Structure

```
rosokua/
├── core/
│   ├── urls.py
│   ├── views.py
├── static/
│   └── css/
│       └── style.css
├── templates/
│   └── core/
│       └── index.html
├── rosokua/
│   └── urls.py
```

## 🌐 URLs Configuration

### 🔹 Project-Level `rosokua/urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('core.urls')),
]
```

### 🔹 App-Level `core/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

## 🧠 Views

### 🔹 `core/views.py`

```python
from django.shortcuts import render

def index(request):
    return render(request, 'core/index.html')
```

## 🖼️ Templates

### 🔹 `templates/core/index.html`

```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Rosokua</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <h1>Welcome to Rosokua</h1>
</body>
</html>
```

## 🧾 Static File Example

### 🔹 `static/css/style.css`

```css
body {
    background-color: #f9f9f9;
    font-family: Arial, sans-serif;
    text-align: center;
    padding: 40px;
}
```

## ▶️ Run Development Server

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000/`

## ❗ Common Errors

- `NameError: name 'views' is not defined` – Make sure `from . import views` is in `core/urls.py`
- `404 Page Not Found /index.html` – Your route is `/`, not `/index.html`

## 🏁 What’s Next?

- Add models, forms, and authentication
- Deploy to PythonAnywhere or Heroku

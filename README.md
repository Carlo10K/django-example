# Apuntes Django  
## Crear un entorno virtual
```sh 
python -m venv /home/carlo/Escritorio/Estudio/Curso-Python/djangoproject 
```
En este entorno es como crear una máquina virtual que trabajará con un Python aparte.

## Activar el entorno virtual
`source /home/carlo/Escritorio/Estudio/Curso-Python/djangoproject/bin/activate` 

Si en la paleta de comandos de Visual Studio Code buscamos `Python: Select Interpreter`, podemos seleccionar el Python del entorno virtual. Así, cuando abramos terminales, ya las abre desde el entorno virtual.

## Instalar Django

`pip install django` 

## Crear el proyecto
`django-admin startproject mysite .` 

El `.` es para que lo instale en la carpeta en la que estamos. Este proyecto será el core de la aplicación y tiene un archivo similar a `artisan` para manejar por comandos el proyecto llamado `manage.py`. Además, trae la base de datos SQLite por defecto.

## Iniciar el servidor

Para iniciar el servidor:

`python manage.py runserver` 

Si queremos cambiar el puerto, lo ponemos después de `runserver`.

## Estructura del proyecto

Django se divide por apps. Cada app sería como un módulo para manejar sus propios controladores dentro de un bloque para separar los mismos. Por ejemplo, una app sería `vehiculos` que contendrá sus propias migraciones, rutas y controladores, etc.

## Crear una app

Para crear una app llamada `blog`:

`python manage.py startapp blog` 

## Estructura de carpetas

/home/carlo/Escritorio/Estudio/Curso-Python/djangoproject/
│
├── bin/
├── include/
├── lib/
├── lib64/
├── mysite/                 		# Core de la app
│   ├── __pycache__/       	 # Contiene cache de la app
│   ├── __init__.py         		# Permite que funcione como módulo la app
│   ├── asgi.py             		# Para cuando se hace el despliegue
│   ├── settings.py         		# Configuraciones de la app
│   ├── urls.py             		# Rutas
│   └── wsgi.py            		 # Despliegue
├── db.sqlite3              # La base de datos
├── manage.py               # El manejador como artisan
└── pyenv.cfg


Si agregamos una app como `myapp`:

`python manage.py startapp myapp` 

La estructura del proyecto se verá así:

/home/carlo/Escritorio/Estudio/Curso-Python/djangoproject/
│
├── bin/
├── include/
├── lib/
├── lib64/
├── myapp/                  # Aplicación agregada, que es una parte del proyecto
│   ├── migrations/         # Contiene las migraciones
│   ├── __init__.py
│   ├── admin.py            # Registrar los modelos, y administrar
│   ├── apps.py             # Configurar la propia app
│   ├── models.py           # Crear los modelos
│   ├── tests.py            # Para testing
│   └── views.py            # Vistas
├── mysite/                 # Core de la app
│   ├── __pycache__/        # Contiene cache de la app
│   ├── __init__.py         # Permite que funcione como módulo la app
│   ├── asgi.py             # Para cuando se hace el despliegue
│   ├── settings.py         # Configuraciones de la app
│   ├── urls.py             # Rutas
│   └── wsgi.py             # Despliegue
├── db.sqlite3              # La base de datos
├── manage.py               # El manejador como artisan
└── pyenv.cfg
## Crear una vista en una app

Si creamos una función en `myapp/views.py` podemos retornar un response que se verá así:
```python

# Create your views here.
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def hello(request):
    return HttpResponse("<h1>hello world</h1>")
```

## Configurar las rutas

En la carpeta principal podemos llamar esta función creando una nueva ruta en `mysite/urls.py`:
```python
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.hello),
]` 
```
Así, en el navegador en la ruta principal nos mostraría el "hello world".

Asi podemos crear todas las funciones que queramos:
```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def hello(request):
    return HttpResponse("<h1>hello world</h1>")

def about(request):
    return HttpResponse('About')
```

y agregarlas a las rutas:
```python
from django.contrib import admin
from django.urls import path
from myapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.hello),
    path('about/',views.about)
]
```

# Desarrollo de ejercicios — Proyecto Django

## Introducción

En este documento se evidencia, paso a paso, la creación de un proyecto web utilizando **Django 5**, Python, un entorno virtual y Git/GitHub.

El proyecto se denomina `django_project` y contiene una aplicación llamada `core`, encargada de gestionar y mostrar un listado de objetos `Item`.

> **Importante:** cada apartado incluye un espacio para colocar la captura de pantalla correspondiente y una breve explicación de lo realizado.

---

# 1. Preparar el entorno de trabajo

## 1.1 Crear la carpeta del proyecto

Primero se creó la carpeta principal del proyecto llamada `django_project`.

```bash
mkdir django_project
cd django_project
```

**Explicación:**  
`mkdir django_project` crea la carpeta del proyecto y `cd django_project` permite ingresar a ella para trabajar desde ese directorio.

### Evidencia

**Captura 1 — Carpeta `django_project` creada**

> 📸 **Insertar aquí la captura de pantalla donde se observe la carpeta `django_project` y la terminal ubicada dentro de ella.**

---

## 1.2 Crear el entorno virtual

Dentro de `django_project` se creó un entorno virtual llamado `venv`.

```bash
python -m venv venv
```

**Explicación:**  
El comando `python -m venv venv` crea un entorno virtual independiente para instalar las dependencias del proyecto sin afectar las instalaciones globales de Python.

### Evidencia

**Captura 2 — Entorno virtual creado**

> 📸 **Insertar aquí la captura de pantalla donde se observe la carpeta `venv`.**

---

## 1.3 Activar el entorno virtual

En Windows PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

Si se utiliza CMD:

```cmd
venv\Scripts\activate
```

Al activarlo, la terminal debe mostrar `(venv)` al inicio de la línea.

**Explicación:**  
Activar el entorno virtual hace que los comandos `python` y `pip` utilizados en esta terminal trabajen con las dependencias aisladas del proyecto.

### Evidencia

**Captura 3 — Entorno virtual activado**

> 📸 **Insertar aquí la captura de pantalla donde aparezca `(venv)` en la terminal.**

---

## 1.4 Crear la carpeta `src`

Con el entorno virtual activado se creó la carpeta donde estará el código fuente.

```bash
mkdir src
```

**Explicación:**  
La carpeta `src` se utilizará para mantener separado el código fuente de otros archivos del proyecto, como el entorno virtual o archivos de configuración del repositorio.

### Estructura hasta este punto

```text
django_project/
├── venv/
└── src/
```

### Evidencia

**Captura 4 — Carpeta `src` creada**

> 📸 **Insertar aquí la captura de pantalla de VS Code donde se observe la estructura del proyecto.**

---

# 2. Instalar Django

## 2.1 Instalar Django 5

Con el entorno virtual activado se instaló Django utilizando `pip`.

```bash
pip install "Django>=5,<6"
```

**Explicación:**  
Se utiliza `pip` para instalar Django dentro del entorno virtual. La condición `>=5,<6` limita la instalación a la versión 5 de Django y evita instalar automáticamente una versión principal posterior.

### Evidencia

**Captura 5 — Instalación de Django**

> 📸 **Insertar aquí la captura de pantalla donde se observe la instalación exitosa de Django.**

---

## 2.2 Verificar la versión instalada

```bash
python -m django --version
```

**Explicación:**  
Este comando consulta directamente la versión de Django instalada en el entorno virtual. El resultado debe corresponder a una versión de la rama 5.x.

### Evidencia

**Captura 6 — Versión de Django**

> 📸 **Insertar aquí la captura de pantalla donde se observe el resultado de `python -m django --version`.**

---

# 3. Crear el proyecto con configuración separada

## 3.1 Crear el proyecto `config` dentro de `src`

Desde la carpeta `django_project` se ejecutó:

```bash
django-admin startproject config src
```

**Explicación:**  
El comando crea un proyecto Django llamado `config` dentro de `src`. De esta manera, `manage.py` queda directamente dentro de `src`, mientras que los archivos de configuración quedan dentro de `src/config`.

### Estructura resultante

```text
django_project/
├── venv/
└── src/
    ├── manage.py
    └── config/
        ├── __init__.py
        ├── asgi.py
        ├── settings.py
        ├── urls.py
        └── wsgi.py
```

### Evidencia

**Captura 7 — Proyecto Django creado**

> 📸 **Insertar aquí la captura de pantalla del explorador de VS Code mostrando `manage.py` dentro de `src` y `settings.py`, `urls.py`, etc. dentro de `src/config`.**

---

# 4. Crear y registrar la aplicación `core`

## 4.1 Crear la aplicación

Primero se ingresó a `src`, donde se encuentra `manage.py`.

```bash
cd src
```

Después se creó la aplicación:

```bash
python manage.py startapp core
```

**Explicación:**  
`manage.py` es el punto de entrada para ejecutar diferentes tareas administrativas de Django. `startapp core` genera la estructura inicial de una aplicación llamada `core`.

### Estructura

```text
src/
├── manage.py
├── config/
└── core/
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── migrations/
    ├── models.py
    ├── tests.py
    └── views.py
```

### Evidencia

**Captura 8 — Aplicación `core` creada**

> 📸 **Insertar aquí la captura donde se observe la carpeta `core` y sus archivos.**

---

## 4.2 Registrar `core` en `INSTALLED_APPS`

Se abrió:

```text
src/config/settings.py
```

y se agregó `core` a `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "core",
]
```

**Explicación:**  
`INSTALLED_APPS` indica a Django qué aplicaciones forman parte del proyecto. Al agregar `core`, Django podrá detectar sus modelos y ejecutar sus migraciones.

### Evidencia

**Captura 9 — Aplicación registrada**

> 📸 **Insertar aquí la captura de `settings.py` donde se observe `"core"` dentro de `INSTALLED_APPS`.**

---

# 5. Definir el modelo `Item`

## 5.1 Crear el modelo

Se editó:

```text
src/core/models.py
```

y se definió el modelo:

```python
from django.db import models


class Item(models.Model):
    name = models.CharField(max_length=200)
    description = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

**Explicación de los campos:**

- `name`: almacena el nombre del ítem como texto y tiene una longitud máxima de 200 caracteres.
- `description`: almacena una descripción de texto largo. `blank=True` permite dejar este campo vacío.
- `created_at`: almacena automáticamente la fecha y hora en que se crea el registro.
- `__str__`: permite mostrar el nombre del ítem de forma más clara en el administrador de Django.

### Evidencia

**Captura 10 — Modelo `Item`**

> 📸 **Insertar aquí la captura de `src/core/models.py` mostrando el modelo completo.**

---

## 5.2 Generar las migraciones

Desde `src`:

```bash
python manage.py makemigrations
```

**Explicación:**  
`makemigrations` analiza los cambios realizados en los modelos y genera archivos de migración que describen los cambios que deben aplicarse a la base de datos.

### Evidencia

**Captura 11 — Migración generada**

> 📸 **Insertar aquí la captura donde se observe que Django detectó el modelo `Item` y creó la migración.**

---

## 5.3 Aplicar las migraciones

```bash
python manage.py migrate
```

**Explicación:**  
`migrate` aplica las migraciones pendientes y crea/modifica las tablas necesarias en la base de datos.

### Evidencia

**Captura 12 — Migraciones aplicadas**

> 📸 **Insertar aquí la captura donde se observe que las migraciones se aplicaron correctamente.**

---

# 6. Crear la vista y las URLs

## 6.1 Crear la vista `item_list`

Se editó:

```text
src/core/views.py
```

con el siguiente código:

```python
from django.shortcuts import render

from .models import Item


def item_list(request):
    items = Item.objects.all()
    return render(request, "core/item_list.html", {"items": items})
```

**Explicación:**  
La vista consulta todos los objetos `Item` mediante `Item.objects.all()`. Después utiliza `render()` para enviar esos datos a la plantilla `core/item_list.html`.

### Evidencia

**Captura 13 — Vista `item_list`**

> 📸 **Insertar aquí la captura de `src/core/views.py` mostrando la implementación de `item_list`.**

---

## 6.2 Crear las URLs de `core`

Se creó:

```text
src/core/urls.py
```

con:

```python
from django.urls import path

from .views import item_list


urlpatterns = [
    path("", item_list, name="item_list"),
]
```

**Explicación:**  
Esta configuración conecta la URL raíz de la aplicación `core` con la vista `item_list`.

### Evidencia

**Captura 14 — URLs de `core`**

> 📸 **Insertar aquí la captura de `src/core/urls.py`.**

---

## 6.3 Enlazar las URLs de `core` con el proyecto

Se editó:

```text
src/config/urls.py
```

de la siguiente manera:

```python
from django.contrib import admin
from django.urls import include, path


urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include("core.urls")),
]
```

**Explicación:**  
`include("core.urls")` permite que el proyecto principal delegue las URLs relacionadas con la aplicación `core` a su propio archivo `urls.py`.

### Evidencia

**Captura 15 — URLs principales**

> 📸 **Insertar aquí la captura de `src/config/urls.py` donde se observe `include("core.urls")`.**

---

# 7. Crear las plantillas

## 7.1 Crear la estructura de templates

Se creó la siguiente estructura:

```text
src/
└── core/
    └── templates/
        ├── base.html
        └── core/
            └── item_list.html
```

**Explicación:**  
La plantilla `base.html` contendrá la estructura HTML general. La plantilla `item_list.html` heredará de ella y mostrará los datos específicos de la aplicación.

### Evidencia

**Captura 16 — Estructura de plantillas**

> 📸 **Insertar aquí la captura del explorador de VS Code mostrando `base.html` e `item_list.html`.**

---

## 7.2 Crear `base.html`

Archivo:

```text
src/core/templates/base.html
```

Contenido:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Mi proyecto Django{% endblock %}</title>
</head>
<body>
    <header>
        <h1>Lista de Items</h1>
    </header>

    <main>
        {% block content %}
        {% endblock %}
    </main>
</body>
</html>
```

**Explicación:**  
`base.html` funciona como plantilla principal. El bloque `title` permite cambiar el título desde otras plantillas y el bloque `content` permite insertar el contenido específico de cada página.

### Evidencia

**Captura 17 — Plantilla base**

> 📸 **Insertar aquí la captura de `base.html`.**

---

## 7.3 Crear `core/item_list.html`

Archivo:

```text
src/core/templates/core/item_list.html
```

Contenido:

```html
{% extends "base.html" %}

{% block title %}Items{% endblock %}

{% block content %}
    <h2>Items registrados</h2>

    <ul>
        {% for item in items %}
            <li>
                <strong>{{ item.name }}</strong>

                {% if item.description %}
                    <p>{{ item.description }}</p>
                {% endif %}

                <small>Creado: {{ item.created_at }}</small>
            </li>
        {% empty %}
            <li>No hay items registrados.</li>
        {% endfor %}
    </ul>
{% endblock %}
```

**Explicación:**  
La plantilla utiliza `{% extends %}` para heredar la estructura de `base.html`.

El bloque `{% for %}` recorre los objetos enviados por la vista. `{% empty %}` muestra un mensaje cuando no existen registros.

### Evidencia

**Captura 18 — Plantilla `item_list.html`**

> 📸 **Insertar aquí la captura de `core/item_list.html` mostrando el uso de `{% for %}` y `{% empty %}`.**

---

# 8. Configurar el administrador y cargar datos

## 8.1 Registrar `Item` en el administrador

Se editó:

```text
src/core/admin.py
```

con:

```python
from django.contrib import admin

from .models import Item


@admin.register(Item)
class ItemAdmin(admin.ModelAdmin):
    list_display = ("name", "created_at")
```

**Explicación:**  
El decorador `@admin.register(Item)` registra el modelo `Item` en el panel administrativo. `list_display` indica qué campos se mostrarán en la lista del administrador.

### Evidencia

**Captura 19 — Modelo registrado en Admin**

> 📸 **Insertar aquí la captura de `src/core/admin.py`.**

---

## 8.2 Crear el superusuario

Desde `src` se ejecutó:

```bash
python manage.py createsuperuser
```

Django solicitará los datos del usuario administrador, como nombre de usuario, correo y contraseña.

**Explicación:**  
El superusuario tendrá permisos para acceder al panel de administración de Django y gestionar los registros de `Item`.

### Evidencia

**Captura 20 — Superusuario creado**

> 📸 **Insertar aquí una captura que evidencie la creación exitosa del superusuario. No mostrar la contraseña.**

---

## 8.3 Ingresar al panel de administración

Se inició el servidor:

```bash
python manage.py runserver
```

Luego se ingresó desde el navegador a:

```text
http://127.0.0.1:8000/admin/
```

**Explicación:**  
El panel de administración permite gestionar los modelos registrados en Django. Después de iniciar sesión se debe poder observar la sección correspondiente a `Items`.

### Evidencia

**Captura 21 — Panel de administración**

> 📸 **Insertar aquí la captura del panel `/admin/` mostrando el modelo `Items`.**

---

## 8.4 Registrar dos ítems de prueba

Desde el administrador se registraron al menos dos ítems.

Ejemplo:

| Nombre | Descripción |
|---|---|
| Primer Item | Registro de prueba para comprobar el funcionamiento del proyecto. |
| Segundo Item | Segundo registro utilizado para verificar el listado. |

**Explicación:**  
Los registros se agregaron desde el panel administrativo para comprobar posteriormente que la vista pública puede recuperarlos desde la base de datos.

### Evidencia

**Captura 22 — Dos ítems registrados**

> 📸 **Insertar aquí la captura del administrador donde se observen al menos dos ítems creados.**

---

# 9. Verificar el funcionamiento

## 9.1 Ejecutar el servidor

Desde `src`:

```bash
python manage.py runserver
```

**Explicación:**  
`runserver` inicia el servidor de desarrollo incluido con Django. Por defecto, la aplicación queda disponible en `127.0.0.1:8000`.

### Evidencia

**Captura 23 — Servidor ejecutándose**

> 📸 **Insertar aquí la captura de la terminal mostrando que el servidor de desarrollo está ejecutándose.**

---

## 9.2 Comprobar la página principal

Se ingresó en el navegador a:

```text
http://127.0.0.1:8000/
```

La página debe mostrar los ítems registrados desde el administrador.

**Explicación:**  
La URL `/` utiliza `core.urls`, que llama a `item_list`. La vista obtiene los registros mediante el modelo `Item` y los envía a `item_list.html`.

### Evidencia

**Captura 24 — Listado de Items**

> 📸 **Insertar aquí una captura del navegador mostrando los dos o más ítems registrados.**

---

## 9.3 Comprobar el panel de administración

Se verificó nuevamente:

```text
http://127.0.0.1:8000/admin/
```

**Explicación:**  
El panel debe permitir iniciar sesión y visualizar/gestionar los objetos `Item` creados anteriormente.

### Evidencia

**Captura 25 — Administración funcionando**

> 📸 **Insertar aquí una captura del panel `/admin/` mostrando los registros existentes.**

---

# 10. Documentar y subir el proyecto

## 10.1 Generar `requirements.txt`

Con el entorno virtual activado se ejecutó:

```bash
pip freeze > requirements.txt
```

**Explicación:**  
Este comando guarda en `requirements.txt` las dependencias instaladas en el entorno virtual. Esto permite que otra persona pueda instalar las mismas dependencias en otro entorno.

### Evidencia

**Captura 26 — `requirements.txt`**

> 📸 **Insertar aquí la captura de `requirements.txt` mostrando Django y sus dependencias.**

---

## 10.2 Crear `README.md`

Se creó un archivo:

```text
README.md
```

con información sobre el proyecto, su estructura, instalación y ejecución.

### Contenido sugerido para `README.md`

```markdown
# Django Project

Proyecto desarrollado con Django 5.

## Requisitos

- Python 3
- pip
- Django 5

## Instalación

Clonar el repositorio:

```bash
git clone URL_DEL_REPOSITORIO
cd django_project
```

Crear el entorno virtual:

```bash
python -m venv venv
```

Activar el entorno virtual en Windows:

```powershell
.\venv\Scripts\Activate.ps1
```

Instalar las dependencias:

```bash
pip install -r requirements.txt
```

Ingresar a `src`:

```bash
cd src
```

Aplicar las migraciones:

```bash
python manage.py migrate
```

Crear un superusuario:

```bash
python manage.py createsuperuser
```

Ejecutar el servidor:

```bash
python manage.py runserver
```

## URLs

Página principal:

```text
http://127.0.0.1:8000/
```

Panel de administración:

```text
http://127.0.0.1:8000/admin/
```

## Estructura

```text
django_project/
├── venv/
├── src/
│   ├── manage.py
│   ├── config/
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── asgi.py
│   │   └── wsgi.py
│   └── core/
│       ├── admin.py
│       ├── models.py
│       ├── views.py
│       ├── urls.py
│       ├── migrations/
│       └── templates/
│           ├── base.html
│           └── core/
│               └── item_list.html
├── requirements.txt
└── README.md
```
```

**Explicación:**  
El README permite que otras personas comprendan el objetivo del proyecto, conozcan su estructura y puedan instalarlo y ejecutarlo correctamente.

### Evidencia

**Captura 27 — README**

> 📸 **Insertar aquí la captura de `README.md` mostrando la documentación del proyecto.**

---

## 10.3 Crear el repositorio Git

Desde la carpeta raíz `django_project`:

```bash
git init
```

**Explicación:**  
`git init` convierte la carpeta del proyecto en un repositorio Git local, permitiendo registrar los cambios realizados en el proyecto.

### Evidencia

**Captura 28 — Repositorio Git inicializado**

> 📸 **Insertar aquí la captura de la terminal donde se observe la inicialización del repositorio.**

---

## 10.4 Crear `.gitignore`

Se recomienda crear un archivo `.gitignore` para evitar subir archivos innecesarios o información local.

Contenido:

```gitignore
venv/
__pycache__/
*.py[cod]
db.sqlite3
.env
.vscode/
```

**Explicación:**  
El entorno virtual, archivos temporales de Python, la base de datos local y configuraciones personales de VS Code no deberían formar parte del repositorio.

### Evidencia

**Captura 29 — Archivo `.gitignore`**

> 📸 **Insertar aquí la captura del archivo `.gitignore`.**

---

## 10.5 Agregar los archivos al repositorio

```bash
git add .
```

**Explicación:**  
`git add .` prepara los archivos y cambios actuales para incluirlos en el próximo commit.

### Evidencia

**Captura 30 — Archivos preparados**

> 📸 **Insertar aquí la captura de la terminal después de ejecutar `git add .`.**

---

## 10.6 Crear el primer commit

```bash
git commit -m "Crear proyecto Django con aplicación core"
```

**Explicación:**  
El commit guarda una versión del proyecto en el historial de Git. El mensaje permite identificar qué cambios fueron registrados.

### Evidencia

**Captura 31 — Primer commit**

> 📸 **Insertar aquí la captura donde se observe el commit realizado correctamente.**

---

## 10.7 Conectar el proyecto con GitHub

Después de crear un repositorio vacío en GitHub, se vinculó el repositorio local con el repositorio remoto:

```bash
git remote add origin URL_DEL_REPOSITORIO
```

**Explicación:**  
`git remote add origin` establece la dirección del repositorio remoto de GitHub donde se almacenará el proyecto.

> **Nota:** reemplazar `URL_DEL_REPOSITORIO` por la URL real del repositorio.

### Evidencia

**Captura 32 — Repositorio remoto configurado**

> 📸 **Insertar aquí la captura de la terminal donde se observe la configuración del repositorio remoto.**

---

## 10.8 Subir el proyecto a GitHub

```bash
git branch -M main
git push -u origin main
```

**Explicación:**  
`git branch -M main` establece `main` como nombre de la rama principal.  
`git push -u origin main` envía los commits locales al repositorio remoto de GitHub.

### Evidencia

**Captura 33 — Proyecto subido a GitHub**

> 📸 **Insertar aquí una captura del repositorio de GitHub donde se observen los archivos del proyecto.**

---

# Conclusión

Se desarrolló un proyecto web utilizando Django 5 siguiendo una estructura organizada.

Durante el desarrollo se realizó lo siguiente:

1. Se creó el proyecto `django_project`.
2. Se creó y activó un entorno virtual.
3. Se instaló y verificó Django 5.
4. Se creó el proyecto Django `config` dentro de `src`.
5. Se creó y registró la aplicación `core`.
6. Se definió el modelo `Item`.
7. Se generaron y aplicaron las migraciones.
8. Se implementó la vista `item_list`.
9. Se configuraron las URLs.
10. Se crearon las plantillas utilizando herencia de templates.
11. Se registró `Item` en el administrador.
12. Se creó un superusuario y se agregaron datos de prueba.
13. Se verificó la página principal y el panel de administración.
14. Se generó `requirements.txt`.
15. Se documentó el proyecto mediante `README.md`.
16. Finalmente, se creó un repositorio Git y se subió el proyecto a GitHub.

## Resultado final

El proyecto cuenta con:

- Página principal con listado de `Item`.
- Panel de administración de Django.
- Base de datos con registros de prueba.
- Separación entre configuración (`config`) y aplicación (`core`).
- Entorno virtual para las dependencias.
- `requirements.txt`.
- `README.md`.
- Repositorio GitHub con el código fuente.

> 📸 **Captura final — Repositorio completo**

> Insertar una última captura del repositorio de GitHub mostrando la estructura general del proyecto.

# Django Project

Proyecto académico desarrollado con Django 5. La aplicación `core` administra y muestra un listado de objetos `Item` desde una página pública y el panel de administración de Django.

## Requisitos

- Python 3
- pip
- Django 5

## Instalación

Clonar el repositorio y entrar en la carpeta del proyecto:

```bash
git clone URL_DEL_REPOSITORIO
cd django_project
```

Crear el entorno virtual:

```bash
python -m venv venv
```

Activarlo en Windows PowerShell:

```powershell
.\venv\Scripts\Activate.ps1
```

Instalar las dependencias:

```bash
pip install -r requirements.txt
```

Entrar en la carpeta del código fuente y aplicar las migraciones:

```bash
cd src
python manage.py migrate
```

Crear el superusuario:

```bash
python manage.py createsuperuser
```

Ejecutar el servidor:

```bash
python manage.py runserver
```

## URLs

- Página principal: http://127.0.0.1:8000/
- Panel de administración: http://127.0.0.1:8000/admin/

## Estructura

```text
django_project/
├── .gitignore
├── README.md
├── requirements.txt
├── venv/
└── src/
    ├── manage.py
    ├── config/
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    └── core/
        ├── __init__.py
        ├── admin.py
        ├── apps.py
        ├── migrations/
        ├── models.py
        ├── tests.py
        ├── urls.py
        ├── views.py
        └── templates/
            ├── base.html
            └── core/
                └── item_list.html
```

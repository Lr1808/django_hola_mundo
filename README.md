
# Django Hola Mundo - Proyecto de ejemplo

Este repositorio contiene una aplicación mínima de Django llamada "Django Hola Mundo" creada como proyecto de ejemplo y aprendizaje. El objetivo es demostrar la estructura básica de un proyecto Django, cómo servir una plantilla simple y cómo organizar una aplicación pequeña (llamada `pages`) con sus vistas, URLs y plantillas.

## Objetivos del proyecto

- Proveer un proyecto Django funcional, sencillo y documentado para aprender los conceptos esenciales de Django.
- Mostrar la configuración básica del proyecto (ajustes, URLs, WSGI/ASGI).
- Incluir una aplicación (`pages`) que sirva una página principal (`home.html`).
- Facilitar la ejecución local, pruebas y despliegue básico.

## Contenido del repositorio

Estructura principal (resumida):

- `manage.py` - Script de administración de Django (migraciones, servidor de desarrollo, shell, etc.).
- `db.sqlite3` - Base de datos SQLite usada por defecto para desarrollo (incluida aquí como ejemplo/estado del proyecto).
- `requirements.txt` - Lista de dependencias del proyecto.
- `django_base/` - Paquete del proyecto Django que contiene la configuración global:
	- `settings.py` - Configuración del proyecto (INSTALLED_APPS, DATABASES, TEMPLATES, STATIC, etc.).
	- `urls.py` - Enrutamiento principal del proyecto.
	- `wsgi.py` / `asgi.py` - Entrypoints para despliegue WSGI/ASGI.
- `pages/` - Aplicación Django que contiene la lógica de la página principal:
	- `views.py` - Vistas (por ejemplo, la vista que renderiza `home.html`).
	- `urls.py` - URLs específicas de la app `pages`.
	- `models.py`, `admin.py`, `tests.py`, `apps.py` - archivos estándar de una app Django (algunos pueden estar vacíos o con código mínimo).
- `templates/` - Carpeta con plantillas HTML; incluye `home.html` usada por la vista principal.

## Requisitos

- Python 3.8+ (se recomienda usar 3.10 o 3.11 según el entorno).
- pip para instalar dependencias.
- Virtualenv/venv recomendado para entorno aislado.

Las dependencias se listan en `requirements.txt`. Para instalarlas:

```powershell
# Crear y activar un entorno virtual
python -m venv .venv; .\.venv\Scripts\Activate.ps1

# Instalar dependencias
pip install -r requirements.txt
```

Si `requirements.txt` está vacío o falta, instale al menos Django:

```powershell
pip install django
```

## Ejecución local (desarrollo)

1. Asegúrate de tener el entorno virtual activado e instalar dependencias (ver sección anterior).
2. Aplicar migraciones para crear la base de datos:

```powershell
python manage.py migrate
```

3. Ejecutar el servidor de desarrollo:

```powershell
python manage.py runserver
```

4. Abrir en el navegador: http://127.0.0.1:8000/ — deberías ver la plantilla `home.html` servida por la app `pages`.

## Estructura y explicación de archivos clave

- `manage.py`: Interfaz de línea de comandos para tareas de desarrollo y administración.
- `django_base/settings.py`: Aquí puedes configurar la base de datos, aplicaciones instaladas (`pages` debe aparecer en `INSTALLED_APPS`), middlewares, localización, directorios de plantillas y archivos estáticos.
- `django_base/urls.py`: Incluye las rutas principales y normalmente realiza `include('pages.urls')` para delegar las rutas de la aplicación.
- `pages/views.py`: Define las vistas que procesan la petición y devuelven respuestas (por ejemplo, `render(request, 'home.html')`).
- `templates/home.html`: Plantilla HTML que se usa para la página principal; puedes editarla para personalizar el contenido.

## Desarrollo y contribución

Si vas a trabajar en el proyecto o a contribuir:

1. Crea una rama para tu trabajo:

```powershell
git checkout -b feature/nombre-de-la-rama
```

2. Ejecuta tests (si existen) antes de abrir un PR:

```powershell
python manage.py test
```

3. Asegúrate de seguir las convenciones de estilo de Python (PEP8) y agrega docstrings donde sea necesario.

## Despliegue (nota rápida)

Para un despliegue simple en un servidor de producción:

- Usa una base de datos distinta a SQLite (PostgreSQL, MySQL).
- Configura variables de entorno para `SECRET_KEY`, `DEBUG=False`, `ALLOWED_HOSTS`.
- Usa un servidor de aplicaciones WSGI (Gunicorn) o ASGI (Uvicorn/Daphne) detrás de un servidor web (Nginx).
- Configura almacenamiento y entrega de archivos estáticos (collectstatic + servir por CDN o por Nginx).

Ejemplo mínimo de pasos:

```powershell
# Instalar gunicorn
pip install gunicorn

# Recopilar archivos estáticos
python manage.py collectstatic --noinput

# Ejecutar gunicorn (Linux/macOS; en Windows se usan alternativas de despliegue)
gunicorn django_base.wsgi:application
```

## Notas y recomendaciones

- Este proyecto es intencionalmente simple — ideal para aprender la anatomía de un proyecto Django.
- Mantén el `SECRET_KEY` fuera del repositorio y usa variables de entorno o un gestor de secretos.
- No uses SQLite en producción.
- Añade pruebas unitarias y de integración según crezca la aplicación.

## Licencia

Indica aquí la licencia del proyecto (por ejemplo MIT, Apache 2.0) o elimina esta sección si no aplica. Si quieres que añada una licencia, dime cuál prefieres y la agregaré.

## Contacto

Si necesitas asistencia o quieres compartir mejoras, abre un issue o un pull request en este repositorio.



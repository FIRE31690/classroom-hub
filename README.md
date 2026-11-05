# ClassroomHub

ClassroomHub es un sitio pequeño en Django construido en el **Laboratorio 6** para
practicar el flujo de una solicitud **URL → vista → plantilla → respuesta**. Tiene
una plantilla base compartida, navegación mediante nombres de rutas y recursos de
aprendizaje de ejemplo enviados desde las vistas.

## Requisitos

- Python 3.12 – 3.15
- Django 6.1.3 (versión fijada en `requirements.txt`)

> Con Python 3.10 u 3.11 utiliza `Django==5.2.19` y actualiza
> `requirements.txt` según corresponda.

## Instalación

```bash
python -m venv .venv
```

Activa el entorno:

- Windows PowerShell: `.\.venv\Scripts\Activate.ps1`
  (o ejecuta directamente `.\.venv\Scripts\python.exe`)
- Linux/macOS: `source .venv/bin/activate`

Instala las dependencias y verifica:

```bash
python -m pip install -r requirements.txt
python manage.py check
python manage.py test pages
python manage.py runserver
```

Abre <http://127.0.0.1:8000/>. (Es normal que aparezca un aviso de migraciones
pendientes: este laboratorio no utiliza la base de datos).

## Entorno virtual (`.venv`)

El proyecto utiliza un entorno virtual `.venv` para aislar sus dependencias del
Python instalado en el sistema. Así cada proyecto tiene sus propias versiones de
Django y de las demás librerías.

- **`.venv/` no se incluye en el repositorio.** Está excluido en `.gitignore`
  porque es pesado, depende del sistema operativo (un entorno creado en Windows
  no funciona en Linux) y puede reconstruirse en cualquier equipo.
- **`requirements.txt` sí se incluye**, porque registra las versiones exactas
  necesarias para recrear el entorno:

```bash
python -m venv .venv
python -m pip install -r requirements.txt
```

- Para comprobar que se está usando el Python del entorno:

```bash
python -c "import sys; print(sys.executable)"
```

  La ruta mostrada debe estar dentro de la carpeta `.venv`.

- Para ver las librerías instaladas en el entorno:

```bash
python -m pip list
```

- En Linux, si el comando `python` no existe, utiliza `python3` para crear el
  entorno; una vez activado, `python` apunta al intérprete del `.venv`.

Otros archivos excluidos en `.gitignore`: `__pycache__/`, `*.py[cod]`, `*.log`,
`.env` y `db.sqlite3`.

## Rutas públicas

| URL           | Vista       | Plantilla                |
|---------------|-------------|--------------------------|
| `/`           | `home`      | `pages/home.html`        |
| `/resources/` | `resources` | `pages/resources.html`   |
| `/about/`     | `about`     | `pages/about.html`       |

Cualquier otra dirección devuelve `404 Not Found`.

## Estructura del proyecto

- `config/` – configuración del proyecto y URLconf principal (`include("pages.urls")`).
- `pages/` – aplicación con vistas, URLs, pruebas y plantillas en
  `pages/templates/pages/`. Todas las páginas heredan de `base.html`.

## Pruebas

`python manage.py test pages` ejecuta 5 pruebas (`SimpleTestCase`, sin base de datos):
códigos de estado, plantillas, datos de ejemplo, navegación y 404.

## Funcionalidades pendientes

- Modelos, persistencia en base de datos o migraciones propias (Laboratorio 7)
- Administración de recursos desde el panel de administración
- Formularios, entradas de usuario e inicio de sesión/autenticación
- Crear, editar y eliminar (CRUD) recursos
- Archivos estáticos y despliegue en producción

Los recursos son datos de ejemplo definidos en `pages/views.py`, por lo que vuelven
a sus valores iniciales cada vez que se inicia el servidor.

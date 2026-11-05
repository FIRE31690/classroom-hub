# ClassroomHub

ClassroomHub es un sitio pequeño en Django construido en el **Laboratorio 6** para
practicar el flujo de una solicitud **URL → vista → plantilla → respuesta**. Tiene
una plantilla base compartida, navegación mediante nombres de rutas y recursos de
aprendizaje de ejemplo enviados desde las vistas.

## Requisitos

- Python 3.12 – 3.15 (el proyecto se desarrolló con Python 3.14.2)
- Django 6.1.3 (versión fijada en `requirements.txt`)

> Con Python 3.10 u 3.11 utiliza `Django==5.2.19` y actualiza
> `requirements.txt` según corresponda.

## Instalación

Clona el repositorio y entra en la carpeta:

```bash
git clone https://github.com/FIRE31690/classroom-hub.git
cd classroom-hub
```

Crea el entorno virtual:

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
  porque es pesado, depende del sistema operativo y puede reconstruirse en
  cualquier equipo a partir de `requirements.txt`.
- **`requirements.txt` sí se incluye**, porque registra las versiones exactas
  necesarias para recrear el entorno:

```text
asgiref==3.13.0
Django==6.1.3
sqlparse==0.6.1
tzdata==2026.6
```

### Entorno de Windows

El `.venv` original del proyecto se creó en **Windows con Python 3.14.2**.
Contiene la carpeta `Scripts\` y el ejecutable `python.exe`, por lo que solo
funciona en Windows:

```powershell
.\.venv\Scripts\Activate.ps1
python manage.py runserver
```

### Entorno de Linux

Un entorno virtual no se puede trasladar entre sistemas operativos: el `.venv`
creado en Windows no funciona en Linux. Para ejecutar el proyecto en Linux, sin
borrar el entorno de Windows, se crea un segundo entorno llamado `.venv-linux`
(también excluido en `.gitignore`):

```bash
python3 -m venv .venv-linux
source .venv-linux/bin/activate
python -m pip install -r requirements.txt
python manage.py runserver
```

En Linux el comando del sistema es `python3`; una vez activado el entorno,
`python` apunta al intérprete del entorno virtual.

### Comprobaciones útiles

Verificar que se está usando el Python del entorno (la ruta debe estar dentro de
`.venv` o `.venv-linux`):

```bash
python -c "import sys; print(sys.executable)"
```

Ver las librerías instaladas en el entorno activo:

```bash
python -m pip list
```

Ver las librerías del `.venv` de Windows desde Linux (sin ejecutarlo):

```bash
ls .venv/Lib/site-packages | grep dist-info
```

Archivos excluidos en `.gitignore`: `.venv/`, `.venv-linux/`, `__pycache__/`,
`*.py[cod]`, `*.log`, `.env` y `db.sqlite3`.

## Rutas públicas

| URL           | Vista       | Plantilla                |
|---------------|-------------|--------------------------|
| `/`           | `home`      | `pages/home.html`        |
| `/resources/` | `resources` | `pages/resources.html`   |
| `/about/`     | `about`     | `pages/about.html`       |

Cualquier otra dirección devuelve `404 Not Found`.

## Estructura del proyecto

```text
classroom-hub/
├── .gitignore
├── README.md
├── requirements.txt
├── manage.py
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
└── pages/
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── migrations/
    │   └── __init__.py
    ├── models.py
    ├── tests.py
    ├── urls.py
    ├── views.py
    └── templates/
        └── pages/
            ├── base.html
            ├── home.html
            ├── resources.html
            └── about.html
```

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

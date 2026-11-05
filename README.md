# ClassroomHub

ClassroomHub is a small Django site built in **Lab 6** to practise the
request flow **URL → view → template → response**. It has a shared base
template, named-route navigation and example learning resources sent from
the views.

## Requirements

- Python 3.12 – 3.15
- Django 6.1.3 (pinned in `requirements.txt`)

> With Python 3.10 or 3.11 use `Django==5.2.19` instead and update
> `requirements.txt` accordingly.

## Setup

```bash
python -m venv .venv
```

Activate the environment:

- Windows PowerShell: `.\.venv\Scripts\Activate.ps1`
  (or call `.\.venv\Scripts\python.exe` directly)
- Linux/macOS: `source .venv/bin/activate`

Install dependencies and verify:

```bash
python -m pip install -r requirements.txt
python manage.py check
python manage.py test pages
python manage.py runserver
```

Open <http://127.0.0.1:8000/>. (A warning about unapplied migrations is
expected: this lab does not use the database.)

## Public routes

| URL           | View        | Template                 |
|---------------|-------------|--------------------------|
| `/`           | `home`      | `pages/home.html`        |
| `/resources/` | `resources` | `pages/resources.html`   |
| `/about/`     | `about`     | `pages/about.html`       |

Any other address returns `404 Not Found`.

## Project structure

- `config/` – project settings and main URLconf (`include("pages.urls")`).
- `pages/` – application with views, URLs, tests and templates in
  `pages/templates/pages/`. Every page extends `base.html`.

## Tests

`python manage.py test pages` runs 5 tests (`SimpleTestCase`, no database):
status codes, templates, example data, navigation and 404.

## Not included yet

- Models, database persistence or migrations of our own (Lab 7)
- Admin management of resources
- Forms, user input, login/authentication
- Create/edit/delete (CRUD) of resources
- Static files and production deployment

Resources are example data defined in `pages/views.py`, so they reset every
time the server starts.

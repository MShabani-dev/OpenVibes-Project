# OpenVibes-Project

A simple blog web app built with Django, featuring user authentication. It was my first project, and it includes a deployment setup for Platform.sh.

**Description:** A simple Django blog with user authentication. Users create personal topics (Overall) and add entries (Explain) with per-user access control.

---

## Features

- User registration, login, and logout (Django auth)
- Each user has a personal list of topics (`Overall`) and can add entries (`Explain`)
- Users can only view and edit their own content (ownership checks)
- Edit existing entries
- Bootstrap 5 UI via `django-bootstrap5`
- Custom 404 and 500 pages
- Deployment configuration for Platform.sh (PostgreSQL, gunicorn)

## Tech Stack

- Python 3.13
- Django 5.2
- django-bootstrap5
- SQLite (local) / PostgreSQL (production)
- gunicorn, psycopg (remote)

## Project Structure

```
blog/            # project settings, root urls, wsgi/asgi
accounts/        # login, register (templates in accounts/templates/registration)
blogs/           # models, views, forms, urls, templates, migrations
templates/       # 404.html, 500.html
manage.py
requirements.txt
requirements_remote.txt
```

## Data Models

- **Overall**: `name`, `date_added`, `owner` (User). A user's topic.
- **Explain**: `esm` (Overall), `name` (text), `date_added`, `owner`. An entry under a topic.
- **Individaul** and **Explain2**: additional models used in earlier migrations.

## Getting Started

```bash
git clone https://github.com/MShabani-dev/OpenVibes-Project.git
cd OpenVibes-Project
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Open `http://127.0.0.1:8000/`.

## URLs

| URL | Description |
|---|---|
| `/` | Home page |
| `/accounts/login/` | Login |
| `/accounts/register/` | Register |
| `/overall/` | Your topics (login required) |
| `/overall/<id>/` | Topic detail and its entries |
| `/new_overall/` | Create a topic |
| `/new_explain/<overall_id>/` | Add an entry to a topic |
| `/edit_overall/<explain_id>/` | Edit an entry |
| `/admin/` | Django admin |

## Deployment

`blog/settings.py` detects Platform.sh and switches to PostgreSQL, `DEBUG = False`, and the Platform.sh host. For remote installs, use `requirements_remote.txt`.

## Security Notes

Before publishing or deploying:

- Move `SECRET_KEY` out of `settings.py` and into an environment variable.
- Set `DEBUG = False` outside local development.
- Do not commit `db.sqlite3` or the `__pycache__` folders. Add them to `.gitignore`.

## Roadmap

- Move the secret key and debug flag to environment variables
- Add tests (`blogs/tests.py` and `accounts/tests.py` are still empty)
- Edit and delete for topics
- Better templates for entries

## License

MIT

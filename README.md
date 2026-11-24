# Weblab — Course and Learning Management Prototype

Django coursework project for managing courses, lessons and student enrollment, with browser-facing pages and Django REST Framework endpoints.

## Current status

**Development prototype; not currently deployed.** There is no current public live demo. Feature verification, cleanup and deployment preparation remain follow-up work; the repository is not presented as a finished production service.

## Features visible in the source

- Course catalogue, details, creation and update/delete routes
- Lessons with optional video URLs
- Student enrollment and course-student views
- Registration, login/logout and profiles
- Course-list/detail and enrollment API routes
- Models for enrolled courses and completed lessons

These describe the existing source structure; this README update did not perform end-to-end feature testing.

## Stack

Python, Django, Django REST Framework, SQLite, Pillow, WhiteNoise and Gunicorn. The tracked `requirements.txt` pins Django 5.1.7 and related packages; the original pins have not been reviewed for current production suitability.

## Repository layout

| Path | Purpose |
| --- | --- |
| `weblab/` | Settings, project URL configuration and WSGI/ASGI entry points |
| `courses/` | Models, views, forms, serializers, templates and migrations |
| `requirements.txt` | Existing pinned dependencies |
| `static/`, `media/` | Static assets and uploaded content |
| `manage.py` | Django management entry point |
| `Procfile` | Deployment process declaration |

## Local setup

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Before starting:

1. Review `weblab/settings.py` and configure a fresh development secret and a local database. The current code must be adapted if you want it to read secrets from environment variables.
2. Use a new database populated with synthetic records, not an unreviewed committed database. Back up existing data privately before changing the local database path/file.
3. The checked-in settings use `DEBUG = False`; local uploaded media is only appended to routes when DEBUG is enabled. Deliberately configure local development behavior and static/media serving.
4. Restrict allowed hosts appropriately before any deployment.

Then run:

```powershell
python manage.py check
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Open `http://127.0.0.1:8000/`. Admin is at `/admin/`. A clean installation and database migration were not re-run for this documentation change.

## Routes

The project includes course URLs at both the root and `/courses/`. Example routes under the root include:

| Route | Purpose |
| --- | --- |
| `/` | Course list |
| `/<id>/` | Course detail |
| `/register/`, `/login/`, `/profile/` | Account pages |
| `/api/courses/` | Course-list API |
| `/api/courses/<id>/` | Course-detail API |
| `/api/enroll/` | Enrollment API route |

Consult `courses/urls.py`, views and serializers for supported HTTP methods, payloads and authentication requirements. These endpoints were not exercised during this update.

## Limitations and follow-up work

- Source contains duplicate list/detail URL declarations; simplify after checking routing behavior.
- Confirm authorization rules for course/lesson modification and enrollment.
- Review dependency/security updates before public deployment.
- Document synthetic fixtures, screenshots and API request/response examples.
- Add meaningful workflow/permission tests; existing test-file names alone are not evidence of coverage.
- Review committed database/media content and move deployment-used secrets out of source.

Student models can hold names and emails; the contents of the committed database were not examined for this README. No hosted demo or production readiness is claimed, and no project-wide licence is asserted.

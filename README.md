[README.md](https://github.com/user-attachments/files/32169181/README.md)
# Movies Store

A Django web application for browsing movies, reading and writing reviews, and purchasing movies through a shopping cart. Built with Django 5.0.

## Features

- **Movie catalog** — browse all movies and search by name (`movies` app)
- **Movie details & reviews** — view a movie's details, read reviews from other users, and post, edit, or delete your own review
- **Review reporting** — flag a review as inappropriate, which logs it as a `Report` for moderators
- **User accounts** — sign up, log in, and log out (`accounts` app, built on Django's built-in auth)
- **Shopping cart & checkout** — add movies to a session-based cart, adjust quantities, clear the cart, and complete a purchase to create an `Order`
- **Order history** — logged-in users can view their past orders
- **Admin site** — manage movies, reviews, reports, orders, and cart items via the built-in Django admin

## Tech stack

- [Django](https://www.djangoproject.com/) 5.0 (Python)
- SQLite (default development database)
- Bootstrap 5, Font Awesome, and Google Fonts (Poppins) for styling, loaded via CDN in `moviesstore/templates/base.html`

## Project structure

```
moviesstore/
├── accounts/     # Sign up, login, logout, order history
├── cart/         # Session-based cart, orders, and order items
├── home/         # Landing page and About page
├── movies/       # Movie catalog, reviews, and review reports
├── moviesstore/  # Project settings, root URLs, shared templates/static files
├── media/        # Uploaded movie images
└── manage.py     # Django's command-line utility
```

## Getting started

### Prerequisites

- Python 3.11+
- pip

### Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/andrewlangie/moviesstore.git
   cd moviesstore
   ```

2. Create and activate a virtual environment (recommended):

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # on Windows: venv\Scripts\activate
   ```

3. Install dependencies:

   ```bash
   pip install django
   ```

   > This project doesn't currently ship a `requirements.txt`. Django 5.0 is the only third-party dependency; everything else is served from CDNs in the templates.

4. Apply database migrations:

   ```bash
   python manage.py migrate
   ```

5. (Optional) Create an admin user so you can add movies through Django admin:

   ```bash
   python manage.py createsuperuser
   ```

6. Run the development server:

   ```bash
   python manage.py runserver
   ```

7. Visit `http://127.0.0.1:8000/` in your browser. Visit `http://127.0.0.1:8000/admin/` to log in as the superuser and add movies (each movie needs a name, price, description, and image).

## Key routes

| URL | Description |
|---|---|
| `/` | Home page |
| `/about` | About page |
| `/movies/` | Movie catalog (supports `?search=` query) |
| `/movies/<id>/` | Movie details and reviews |
| `/cart/` | Shopping cart |
| `/cart/purchase/` | Checkout (requires login) |
| `/accounts/signup` | Create an account |
| `/accounts/login/` | Log in |
| `/accounts/orders/` | Order history (requires login) |
| `/admin/` | Django admin site |

## Notes

- The included `db.sqlite3` and `SECRET_KEY` in `moviesstore/settings.py` are for local development only — do not use them in production. Generate a fresh secret key and use a production-grade database (e.g. PostgreSQL) before deploying.
- `DEBUG = True` is set for development; set it to `False` and configure `ALLOWED_HOSTS` before deploying publicly.

# Post CRUD API (Django REST Framework)

A simple CRUD API built with Django and Django REST Framework. It exposes a `Post` model (title, description, image, publish status, and timestamps) over a RESTful API.

## Features

- Full CRUD operations on `Post` resources
- Browseable API powered by DRF
- Media (image) upload support
- Environment-based configuration via `python-decouple`

## Tech Stack

- Python 3.10
- Django 5.2
- Django REST Framework
- Pillow (image handling)
- Pipenv (dependency management)

## Project Structure

```
lab3/
├── config/            # Django project settings & root URLs
│   ├── settings.py
│   └── urls.py
├── main/              # Main app (model, serializer, viewset, urls)
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   └── urls.py
├── media/             # Uploaded images (created at runtime)
├── Pipfile            # Project dependencies
└── manage.py
```

## Getting Started

### Prerequisites

- Python 3.10+
- Pipenv installed (`pip install pipenv`)

### Installation

1. Clone the repository and navigate to the project directory:

   ```bash
   cd lab3
   ```

2. Install dependencies:

   ```bash
   pipenv install
   ```

3. Create a `.env` file from the example:

   ```bash
   cp .env_example .env
   ```

   Then set your values:

   ```ini
   DEBUG=True
   SECRET_KEY=your-secret-key-here
   ALLOWED_HOSTS=localhost,127.0.0.1
   ```

   > For development, `DEBUG=True` enables the browsable API and media serving.

4. Apply database migrations:

   ```bash
   pipenv run python manage.py migrate
   ```

5. (Optional) Create a superuser to access the Django admin:

   ```bash
   pipenv run python manage.py createsuperuser
   ```

6. Run the development server:

   ```bash
   pipenv run python manage.py runserver
   ```

The API will be available at `http://127.0.0.1:8000/`.

## API Endpoints

All endpoints are served under the `/api/` prefix.

| Method   | Endpoint             | Description            |
| -------- | -------------------- | ---------------------- |
| `GET`    | `/api/posts/`        | List all posts         |
| `POST`   | `/api/posts/`        | Create a new post      |
| `GET`    | `/api/posts/<id>/`   | Retrieve a post        |
| `PUT`    | `/api/posts/<id>/`   | Update a post (full)   |
| `PATCH`  | `/api/posts/<id>/`   | Update a post (partial)|
| `DELETE` | `/api/posts/<id>/`   | Delete a post          |

You can also browse the interactive API at `http://127.0.0.1:8000/api/`.

### Post Model Fields

| Field          | Type            | Notes                              |
| -------------- | --------------- | ---------------------------------- |
| `id`           | integer         | Auto-generated primary key         |
| `title`        | string          | Max 200 characters                 |
| `description`  | text            |                                    |
| `post_img`     | image           | Uploaded to `media/post_imgs/`     |
| `is_published` | boolean         |                                    |
| `created_at`   | datetime        | Auto-set on creation               |
| `updated_at`   | datetime        | Auto-updated on save               |

## Example Requests

### Create a post

```bash
curl -X POST http://127.0.0.1:8000/api/posts/ \
  -F "title=My First Post" \
  -F "description=Hello world" \
  -F "is_published=true" \
  -F "post_img=@/path/to/image.jpg"
```

### List posts

```bash
curl http://127.0.0.1:8000/api/posts/
```

### Retrieve, update, delete

```bash
curl http://127.0.0.1:8000/api/posts/1/
curl -X PATCH http://127.0.0.1:8000/api/posts/1/ -H "Content-Type: application/json" -d '{"is_published": false}'
curl -X DELETE http://127.0.0.1:8000/api/posts/1/
```

## Admin Panel

Visit `http://127.0.0.1:8000/admin/` and log in with your superuser account to manage posts via the Django admin interface.

## Notes

- Uploaded images are stored in the `media/` directory (served only when `DEBUG=True`).
- Never commit your `.env` file or the generated `db.sqlite3` and `media/` contents to version control.

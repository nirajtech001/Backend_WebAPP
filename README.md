

# Traveller Website Backend - Django Framework

Traveller is a web platform where users can explore and manage their favorite travel destinations. It provides personalized travel experiences and collaboration opportunities with travel agencies, helping users plan their trips while businesses can promote curated experiences and services.

## Features
- **User Registration and Login**: Users can create accounts, log in, and manage their profiles.
- **Travel Plans**: Users can view and manage their travel plans.
- **Admin Controls**: Only admins can add or remove destination data.
---

## Tech Stack
- **Backend**: Django Framework
- **Frontend**: Basic HTML, CSS, and JavaScript
- **Database**: PostgreSQL
- **Deployment**: Hosted on Render

---

## Setup Instructions

### Prerequisites
- Python 3.x
- pip (Python package manager)
- PostgreSQL (if running in production)
- Virtual environment (optional but recommended)

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd Backend_WebAPP-main
   ```

2. Create a virtual environment and activate it:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Linux/Mac
   venv\Scripts\activate   # On Windows
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Apply migrations:
   ```bash
   python manage.py migrate
   ```

5. Create a superuser (for admin access):
   ```bash
   python manage.py createsuperuser
   ```

6. Run the development server:
   ```bash
   python manage.py runserver
   ```

### Deployment on Render
1. Push your code to a Git repository.
2. Connect the repository to Render and configure the environment variables (such as database credentials).
3. Deploy the web service and apply migrations.

---

## Database Schema

### Models
The project includes three main models:
![image](https://github.com/user-attachments/assets/9f355cc6-32f0-4b4e-8085-ad8835e01a25)


1. **User (accounts/models.py)**:
   - Fields: `username`, `email`, `password`, `is_admin`
   - Relationships: Handles user authentication and assigns admin privileges.
   ![image](https://github.com/user-attachments/assets/14ff14a6-fc4a-411e-8102-6e18e187cb6c)

   ```python
   from django.contrib.auth.models import AbstractUser
   
   class User(AbstractUser):
       is_admin = models.BooleanField(default=False)
   ```

2. **Destination (travello/models.py)**:
   - Fields: `name`, `description`, `image`, `price`, `offer`
   - Admin users can add or delete destinations.
     ![image](https://github.com/user-attachments/assets/bbeea412-3db6-4326-8f3b-7426c64b7b97)

   
   ```python
   from django.db import models

   class Destination(models.Model):
       name = models.CharField(max_length=100)
       description = models.TextField()
       image = models.ImageField(upload_to='images/')
       price = models.DecimalField(max_digits=10, decimal_places=2)
       rating = models.FloatField()
   ```
![image](https://github.com/user-attachments/assets/1f905e49-aaef-4432-a8b1-9f005a82a4a6)


## Backend Routes

The backend routes are handled through Django views:

- **Registration/Login** (`accounts/views.py`):
   - `/register/` and `/login/` endpoints for user management.

   ```python
   def register(request):
       # Logic for user registration
       return render(request, 'register.html')

   def login(request):
       # Logic for user login
       return render(request, 'login.html')
   ```

- **Destination Management** (`travello/views.py`):
   - `/destinations/`: List all destinations.
   - `/destinations/add/`: Add a new destination (admin-only).

   ```python
   def add_destination(request):
       if request.user.is_admin:
           # Logic for adding a destination
           return render(request, 'add_destination.html')
   ```

- **Travel Plans** (`WebApp/views.py`):
   - `/plans/`: View and manage user travel plans.

---

## Middleware

Middleware used includes Django's built-in middleware for:

- Authentication (`django.contrib.auth.middleware.AuthenticationMiddleware`)
- Session management (`django.contrib.sessions.middleware.SessionMiddleware`)

To add custom middleware:

```python
class CustomMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        # Custom logic before view execution
        response = self.get_response(request)
        # Custom logic after view execution
        return response
```

## Project Structure
- `manage.py`: Django management script.
- `requirements.txt`: Python dependencies.
- `db.sqlite3`: Local development database (SQLite).
- `WebApp/`, `accounts/`, `travello/`: Main Django apps handling different aspects of the project.
- `static/` and `media/`: Static and media files.

---

## Demonstration 
![image](https://github.com/user-attachments/assets/f10bbb5d-33d2-46fd-be3b-bd750749253c)
![image](https://github.com/user-attachments/assets/90a006fd-c623-418e-bc6d-b607433cbe72)



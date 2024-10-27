
# Blog API Project

This project is a Django REST API for managing a blog, which includes features like user authentication, role-based access, and PostgreSQL integration. It allows users to create, read, update, and delete blog posts, with different permissions based on user roles.

## Table of Contents
- [Requirements](#requirements)
- [Installation](#installation)
- [Setup](#setup)
- [Running the Project](#running-the-project)
- [API Endpoints](#api-endpoints)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## Requirements
- Python 3.8 or higher
- Django 3.x or higher
- PostgreSQL 12 or higher
- Django REST Framework
- psycopg2 (PostgreSQL adapter for Python)

## Installation

### 1. Clone the Repository:
   ```bash
   git clone <repository-url>
   cd blog_api_project
   ```

### 2. Set up a Python Virtual Environment:
   To keep dependencies isolated, create and activate a virtual environment:
   ```bash
   python3 -m venv env
   source env/bin/activate    # On Windows: `env\Scripts\activate`
   ```

### 3. Install the Required Dependencies:
   Inside the project directory, run the following to install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### 4. Set Up PostgreSQL:
   Install PostgreSQL and create a new database and user for the project. You can use the following SQL commands in the PostgreSQL shell:
   ```sql
   CREATE DATABASE blogdb;
   CREATE USER bloguser WITH PASSWORD 'yourpassword';
   ALTER ROLE bloguser SET client_encoding TO 'utf8';
   ALTER ROLE bloguser SET default_transaction_isolation TO 'read committed';
   ALTER ROLE bloguser SET timezone TO 'UTC';
   GRANT ALL PRIVILEGES ON DATABASE blogdb TO bloguser;
   ```

### 5. Configure Database Settings:
   Open `settings.py` inside the project directory and update the `DATABASES` section with your PostgreSQL credentials:
   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.postgresql',
           'NAME': 'blogdb',
           'USER': 'bloguser',
           'PASSWORD': 'yourpassword',
           'HOST': 'localhost',
           'PORT': '5432',
       }
   }
   ```

### 6. Apply Migrations:
   Once the database is set up, apply the migrations to create the required tables:
   ```bash
   python manage.py migrate
   ```

### 7. Create a Superuser:
   To access the admin dashboard, create a superuser account:
   ```bash
   python manage.py createsuperuser
   ```

## Running the Project

1. Start the development server:
   ```bash
   python manage.py runserver
   ```

2. Access the API at:
   ```
   http://127.0.0.1:8000/
   ```

3. Access the Django admin interface:
   ```
   http://127.0.0.1:8000/admin/
   ```

## API Endpoints

- **Authentication:**
  - `POST /api/token/`: Obtain a JWT token for authentication.
  - `POST /api/token/refresh/`: Refresh an existing JWT token.

- **Blog Management:**
  - `GET /api/posts/`: List all blog posts.
  - `POST /api/posts/`: Create a new blog post (requires admin access).
  - `GET /api/posts/{id}/`: Retrieve details of a specific post by ID.
  - `PUT /api/posts/{id}/`: Update a blog post (requires admin access).
  - `DELETE /api/posts/{id}/`: Delete a blog post (requires admin access).

- **User Management:**
  - `POST /api/register/`: Register a new user.
  - `GET /api/users/`: Retrieve a list of users (requires admin access).

## Testing

To run the tests for this project:
1. Ensure that all dependencies are installed and the project is set up correctly.
2. Run the tests using Django's test runner:
   ```bash
   python manage.py test
   ```

## Contributing

Feel free to contribute to this project by submitting issues or creating pull requests. Follow the standard GitHub workflow to fork the repository, create a feature branch, and submit a pull request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

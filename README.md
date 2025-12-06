# Little Lemon Web Application

## Introduction

This is the final project for the [Meta Back-End Developer Capstone](https://www.coursera.org/learn/back-end-developer-capstone/) course. This web application is a restaurant booking and menu management system built with Django, Django REST Framework (DRF), Djoser, and MySQL.

There is a simple static page for the restaurant available at `http://localhost:8000/restaurant/`.

## Features

*   View and manage menu items.
*   Book tables at the restaurant.
*   User authentication with different permissions for customers and administrators.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

*   Python 3.8+
*   pip (Python package installer)
*   MySQL

## Installation

1.  **Clone the repository:**

    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Create a virtual environment and activate it:**

    ```bash
    # For Windows
    python -m venv venv
    .\venv\Scripts\activate

    # For macOS/Linux
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Install the required dependencies:**

    ```bash
    pip install -r requirements.txt
    ```
    *(Note: You may need to create a `requirements.txt` file if it doesn't exist by running `pip freeze > requirements.txt` after installing the necessary packages like Django, djangorestframework, djoser, mysqlclient, etc.)*

4.  **Configure the database:**

    Open the `settings.py` file in your project and update the `DATABASES` setting with your MySQL credentials:

    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'littlelemon',
            'USER': '<your-mysql-user>',
            'PASSWORD': '<your-mysql-password>',
            'HOST': 'localhost',
            'PORT': '3306',
        }
    }
    ```

5.  **Run database migrations:**

    ```bash
    python manage.py migrate
    ```

## Running the Application

1.  **Start the development server:**

    ```bash
    python manage.py runserver
    ```

2.  **Access the application:**

    You can access the web application at `http://localhost:8000/`. The static restaurant page is at `http://localhost:8000/restaurant/`.

## API Endpoints

### Menu API

*   `restaurant/api/menu`
    *   **GET:** Allows all authenticated users to view the menu items.
    *   **POST:** Allows only admin users to post a new item.
        *   **Fields:**
            *   `title` (string, required)
            *   `price` (decimal, required)
            *   `featured` (boolean, optional, default: `0`)

*   `restaurant/api/menu/<int:pk>`
    *   **GET:** Allows all authenticated users to view a single menu item.
    *   **PUT/PATCH/DELETE:** Allows only admin users to update or delete a single menu item.

### Booking API

*   `restaurant/api/book`
    *   **GET:** Authenticated users can obtain all their bookings.
    *   **POST:** Allows authenticated users to create a new booking. The `name` field must be the same as the username.
        *   **Fields:**
            *   `name` (string, required, must be the same as the username)
            *   `guest_number` (integer, optional, default: `1`)
            *   `date` (date, required, format: "YYYY-MM-DD")
            *   `comment` (text, optional)

*   `restaurant/api/book/<int:pk>`
    *   **GET/DELETE:** Allows only admin users to view or delete a single booking.

## User Credentials

Here are some default user credentials for testing:

### Superuser/Admin

*   **Username:** `admin`
*   **Password:** `123`

### Customer

*   **Username:** `customer1`
*   **Password:** `lemon@123!`
<br>
*   **Username:** `customer2`
*   **Password:** `lemon@123!`
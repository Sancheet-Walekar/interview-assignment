

# User Management System

A Laravel-based user management API.

## Project Setup

1. **Clone the repository**

git clone https://github.com/Sancheet-Walekar/interview-assignment.git

2. **Install dependencies**

   composer install

3. **Environment Setup**

   cp .env.example .env
   php artisan key:generate
   Configure your database details in .env

4. **Run Migrations**

   php artisan migrate

5. **Serve**

   php artisan serve

## Architecture Overview

*   **Controller**: Handles HTTP requests and response formatting.
*   **Service Layer**: Orchestrates logic, handles caching, and communicates with BO and DAO.
*   **Business Object (BO)**: Encapsulates business rules like data preparation and password hashing.
*   **Data Access Object (DAO)**: Manages direct database interactions using Eloquent.

## API Endpoints

*   `POST /api/users` - Create a new user.
*   `PUT /api/users/{id}` - Update an existing user.
*   `GET /api/users` - List all users.
*   `GET /api/users/{id}` - Show a specific user.

## How Caching Works

*   **Read**: User data is retrieved from `users.{id}` cache key if available. Full user list is cached at `users.all`.
*   **Write**:
    *   Creating a user invalidates the `users.all` list cache.
    *   Updating a user invalidates both the specific `users.{id}` cache and the `users.all` list cache.

## API Testing

The User Management APIs were tested locally using Postman.

### Base URL
http://127.0.0.1:8000

### Create User
POST /api/users

Request Body:
json
{
  "name": "Sancheet Walekar",
  "email": "sa@gmail.com",
  "password": "password123"
}

Expected Result:

Returns HTTP 201
User is created with encrypted password

Update User
PUT /api/users/{id}

Request Body:
json

{
  "name": "Sancheet Updated",
  "email": "sa.updated@gmail.com",
  "password": "newpassword123"
}

Expected Result:

Returns HTTP 200
User details are updated
Cache is invalidated

Returns HTTP 200
Returns list of users

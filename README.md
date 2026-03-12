# perfect-esthetic-api

REST API backend for a beauty/esthetic business. Built with Laravel 12 and secured with token-based authentication via Laravel Sanctum.

## Tech Stack

- **PHP** 8.2
- **Laravel** 12
- **Laravel Sanctum** — token-based authentication
- **MySQL** — relational database
- **Laravel Storage** — local image management

## Features

- Admin and Staff authentication (register / login via Sanctum tokens)
- Before & After content management — create, update, and delete transformation posts with image uploads
- Role-based access control (`ADMIN` / `STAFF`)
- Public endpoint to list Before & After content
- Image storage and replacement with automatic cleanup of old files

## Project Structure

```
app/
├── Http/
│   └── Controllers/
│       ├── API/
│       │   └── BeforeAfterController.php
│       └── Auth/
│           └── AuthController.php
├── Models/
│   ├── User.php
│   └── BeforeAfter.php
database/
└── migrations/
```

## API Endpoints

### Auth
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/v1/register` | Register admin/staff user | No |
| POST | `/api/v1/login` | Login and receive token | No |

### Before & After
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/v1/before-after` | List all transformations | No |
| POST | `/api/v1/before-after` | Upload new before/after post | Yes |
| PUT | `/api/v1/before-after/{id}` | Update post or images | Yes |
| DELETE | `/api/v1/before-after/{id}` | Delete post and images | Yes |

## Getting Started

### Requirements

- PHP 8.2+
- Composer
- MySQL

### Installation

```bash
# Clone the repository
git clone https://github.com/karol-cc/perfect-esthetic-api.git
cd perfect-esthetic-api

# Install dependencies
composer install

# Set up environment
cp .env.example .env
php artisan key:generate

# Configure your database in .env
# DB_DATABASE=perfectesthetic
# DB_USERNAME=your_username
# DB_PASSWORD=your_password

# Run migrations
php artisan migrate

# Link storage for image access
php artisan storage:link

# Start the server
php artisan serve
```

The API will be available at `http://localhost:8000`.

## Environment Variables

Create a `.env` file from `.env.example` and configure:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=perfectesthetic
DB_USERNAME=root
DB_PASSWORD=your_password
```

> ⚠️ Never commit your `.env` file. It is already excluded in `.gitignore`.

## Authentication

Protected routes require a Bearer token in the request header:

```
Authorization: Bearer {token}
```

The token is returned upon successful login.

# 🚀 Laravel API Starter Kit

A production-ready Laravel REST API boilerplate that saves you 2-3 days of development time. Built with Laravel 12, Sanctum authentication, Spatie permissions, rate limiting, and comprehensive error handling.

## ✨ Features

- **🔐 Authentication** - Laravel Sanctum token-based authentication
- **👥 Roles & Permissions** - Spatie Laravel Permission package pre-configured
- **🚦 Rate Limiting** - Configurable rate limits for different route groups
- **🛡️ Error Handling** - Consistent JSON error responses across the entire API
- **🗂️ API Versioning** - Built-in versioning structure (v1)
- **📝 Request Validation** - Form Request classes with custom error messages
- **📦 API Resources** - Laravel API Resources for clean data transformation
- **🔄 Soft Deletes** - User soft deletion implemented
- **📮 Postman Collection** - Ready-to-import Postman collection for testing

## 📋 Requirements

- PHP 8.4+
- Composer
- MySQL/PostgreSQL
- Laravel 12

## 🚀 Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/laravel-api-starter.git
cd laravel-api-starter
```

### 2. Install dependencies

```bash
composer install
```

### 3. Install required packages

```bash
composer require laravel/sanctum
composer require spatie/laravel-permission
```

### 4. Publish vendor assets

```bash
php artisan vendor:publish --provider="Laravel\\Sanctum\\SanctumServiceProvider"
php artisan vendor:publish --provider="Spatie\\Permission\\PermissionServiceProvider"
```

### 5. Environment setup

```bash
cp .env.example .env
php artisan key:generate
```

Configure your database in `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=your_database
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

### 6. Run migrations

```bash
php artisan migrate
```

### 7. Seed the database

```bash
php artisan db:seed
```

This will create:
- Roles: `admin`, `user`, `moderator`
- Permissions: `view users`, `edit users`, `delete users`, `manage roles`
- Admin user: `admin@example.com` / `password`

### 8. Start the development server

```bash
php artisan serve
```

Your API will be available at `http://localhost:8000`

## 📡 API Endpoints

### Authentication

| Method | Endpoint | Description | Rate Limit |
|--------|----------|-------------|------------|
| POST | `/api/v1/auth/register` | Register a new user | 10/min |
| POST | `/api/v1/auth/login` | Login user | 10/min |
| POST | `/api/v1/auth/logout` | Logout user | - |
| GET | `/api/v1/auth/me` | Get authenticated user | - |
| POST | `/api/v1/auth/refresh` | Refresh token | 5/min |

### Users

| Method | Endpoint | Description | Auth | Permission |
|--------|----------|-------------|------|------------|
| GET | `/api/v1/users` | List all users | Required | admin |
| GET | `/api/v1/users/{id}` | Get single user | Required | - |
| PUT | `/api/v1/users/{id}` | Update user | Required | - |
| DELETE | `/api/v1/users/{id}` | Soft delete user | Required | - |

## 📮 Postman Collection

Import the `postman_collection.json` file into Postman to test all endpoints.

1. Open Postman
2. Click Import
3. Select `postman_collection.json`
4. Set environment variable `base_url` to `http://localhost:8000`

## 🧪 Testing

### Register a user

```bash
curl -X POST http://localhost:8000/api/v1/auth/register \\
  -H "Content-Type: application/json" \\
  -d '{
    "name": "Test User",
    "email": "test@example.com",
    "password": "password123",
    "password_confirmation": "password123"
  }'
```

### Login

```bash
curl -X POST http://localhost:8000/api/v1/auth/login \\
  -H "Content-Type: application/json" \\
  -d '{
    "email": "admin@example.com",
    "password": "password"
  }'
```

## 📝 JSON Response Format

All API responses follow this consistent format:

```json
{
  "success": true,
  "message": "Success message",
  "data": {
    "key": "value"
  },
  "errors": {},
  "meta": {
    "timestamp": "2026-03-04T12:00:00.000000Z",
    "version": "v1"
  }
}
```

## ⚙️ Configuration

### Rate Limiting

Edit `config/api.php` to adjust rate limits:

```php
'rate_limits' => [
    'api' => 60,      // General API routes
    'auth' => 10,     // Login/Register routes
    'strict' => 5,    // Sensitive routes
],
```

### Token Expiry

```php
'token_expiry' => 60 * 24 * 7, // 7 days in minutes
```

### Pagination

```php
'pagination' => [
    'default' => 15,
    'max' => 100,
],
```

## 🗂️ Project Structure

```
app/
├── Exceptions/
│   └── Handler.php              # Global exception handler
├── Http/
│   ├── Controllers/
│   │   └── Api/V1/
│   │       ├── AuthController.php
│   │       └── UserController.php
│   ├── Middleware/
│   │   └── ForceJsonResponse.php
│   ├── Requests/Api/
│   │   ├── LoginRequest.php
│   │   └── RegisterRequest.php
│   └── Resources/
│       └── UserResource.php
├── Models/
│   └── User.php
└── Traits/
    └── ApiResponseTrait.php      # Consistent API responses
config/
└── api.php                       # API configuration
database/
└── seeders/
    ├── RoleSeeder.php
    └── AdminUserSeeder.php
routes/
└── api.php                       # API routes (versioned)
```

## 🔒 Security

- Token-based authentication via Sanctum
- Rate limiting to prevent brute force attacks
- JSON-only middleware for API endpoints
- Validation on all input
- Soft deletes for data retention

## 📚 Documentation

For more details on specific features:

- [Laravel Sanctum](https://laravel.com/docs/sanctum)
- [Spatie Laravel Permission](https://spatie.be/docs/laravel-permission)
- [Laravel Rate Limiting](https://laravel.com/docs/routing#rate-limiting)

## 🤝 Contributing

This is a starter kit/boilerplate. Feel free to customize it for your needs!

## 📄 License

This project is open-sourced software licensed under the MIT license.

## 💰 Support

If you find this starter kit helpful, consider:
- ⭐ Starring the repository
- 🐛 Reporting bugs
- 💡 Suggesting new features

---

**Happy Coding! 🚀**

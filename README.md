# Laravel Admin Panel
An admin panel for managing users, roles, permissions & crud.

### Requirements
    Laravel >=5.5
    PHP >= 7.0

## Features
- User, Role & Permission Manager
- CRUD Generator
- Activity Log
- Page CRUD
- Settings

## Installation

1. Run
    ```
    composer require voope/laravel-admin
    ```

2. Install the admin package.
    ```
    php artisan laravel-admin:install
    ```
    > Service provider will be discovered automatically.
3. Make sure your user model's has a ```HasRoles``` trait **app/User.php**.
    ```php
    class User extends Authenticatable
    {
        use Notifiable, HasRoles;

        ...
    ```

4. You can generate CRUD easily through generator tool now.


## Usage

1. Create some permissions.

2. Create some roles.

3. Assign permission(s) to role.

4. Create user(s) with role.

5. For checking authenticated user's role see below:
    ```php
    // Add roles middleware in app/Http/Kernel.php
    protected $routeMiddleware = [
        ...
        'roles' => \App\Http\Middleware\CheckRole::class,
    ];
    ```

    ```php
    // Check role anywhere
    if (Auth::check() && Auth::user()->hasRole('admin')) {
        // Do admin stuff here
    } else {
        // Do nothing
    }

    // Check role in route middleware
    Route::group(['namespace' => 'Admin', 'prefix' => 'admin', 'middleware' => ['auth', 'roles'], 'roles' => 'admin'], function () {
       Route::get('/', ['uses' => 'AdminController@index']);
    });
    ```

6. For checking permissions see below:

    ```php
    if ($user->can('permission-name')) {
        // Do something
    }
    ```

Learn more about ACL from [here](https://laravel.com/docs/master/authorization)

For activity log please read `spatie/laravel-activitylog` [docs](https://docs.spatie.be/laravel-activitylog/v2/introduction)

## Author

[Paulo Rodrigues] email: [Email Me](mailto:paulo@voope.com.br)

## License

This project is licensed under the MIT License - see the [License File](LICENSE) for details

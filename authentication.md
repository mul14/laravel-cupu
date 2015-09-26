---
currentMenu: authentication
---

Autentikasi
===========

Laravel 4.x
-----------

Di [Laravel 4](http://laravel.com/docs/4.2/security), anda dapat dengan mudah membuat login dengan menambahkan beberapa code. Kira-kira seperti ini di `app/routes.php`

```php
Route::get('login', function()
{
    return View::make('login');
});

Route::post('login', function()
{
    $credentials = Input::only('email', 'password');
    $remember = Input::get('remember');
    
    if (Auth::attempt($credentials, $remember))
    {
        return Redirect::intended('/');
    }
    
    return Redirect::back()->withMessage('Invalid Credentials');
});
```

Laravel 5.0
-----------
Jika anda menggunakan [Laravel 5.0](http://laravel.com/docs/5.0/authentication), fitur Autentikasi bisa anda gunakan *out-of-the-box*. Cukup masuk ke http://localhost:8000/auth/login. Begitu juga dengan registrasi anda bisa masuk ke http://localhost:8000/auth/register.


Laravel 5.1 (LTS)
-----------------

Pada [Laravel 5.1](http://laravel.com/docs/5.1/authentication), view, routes sudah dibuang dari 5.0. Tapi Controller dan trait untuk authentikasi sudah disiapkan. Untuk menggunakannya tambahkan code berikut pada `app/Http/routes.php`

```php
Route::controller('auth', 'Auth\AuthController');
Route::controller('password', 'Auth\PasswordController');
```
Anda bisa buka url berikut 

* http://localhost:8000/auth/login (GET, POST) - Untuk login 
* http://localhost:8000/auth/register (GET, POST) - Untuk registrasi
* http://localhost:8000/password/email (GET, POST) - Request password reset
* http://localhost:8000/password/reset (GET, POST) - Untuk reset password

Setelah routes anda tambahkan, jangan lupa buat view-nya.

Ini contoh view untuk login di `resources/views/auth/login.blade.php`

```php
<form method="POST" action="/auth/login">
    {!! csrf_field() !!}

    <div>
        Email
        <input type="email" name="email" value="{{ old('email') }}">
    </div>

    <div>
        Password
        <input type="password" name="password" id="password">
    </div>

    <div>
        <input type="checkbox" name="remember"> Remember Me
    </div>

    <div>
        <button type="submit">Login</button>
    </div>
</form>
```

Untuk registrasi, tambahkan code berikut pada `resources/views/auth/register.blade.php`

```php
<form method="POST" action="/auth/register">
    {!! csrf_field() !!}

    <div>
        Name
        <input type="text" name="name" value="{{ old('name') }}">
    </div>

    <div>
        Email
        <input type="email" name="email" value="{{ old('email') }}">
    </div>

    <div>
        Password
        <input type="password" name="password">
    </div>

    <div>
        Confirm Password
        <input type="password" name="password_confirmation">
    </div>

    <div>
        <button type="submit">Register</button>
    </div>
</form>
```

Class `Auth\AuthController` by default akan melakukan pengecekan authentikasi dengan menggunakan email dan password. Jika anda ingin menggunakan kombinasi antara `user_id` dan password tambahkan property berikut pada `app/Http/Auth/AuthController.php`.

```
protected $username = 'user_id';
```

### Redirect

Khusus di [Laravel 5.1](http://laravel.com/docs/5.1/authentication#included-authenticating), jika menggunakan `Auth\AuthController` default maka anda bisa mengubah redirect url. Tambahkan property berikut pada `app/Http/Auth/AuthController.php`

```php
/** 
 * Setelah berhasil login, user akan diarahkan kesini
 */ 
protected $redirectPath = '/dashboard';

/** 
 * Ini juga berfungsi sama dengan $redirectPath.
 * Bila $redirectPath telah di-set, maka ini akan diabaikan.
 */ 
protected $redirectTo = '/dashboard';

/** 
 * Jika user belum login, lalu mengakses halaman yang harus
 * login terlebih dahulu, maka akan di-redirect kesini
 */ 
protected $loginPath = '/login';

/** 
 * Setelah logout, user akan diarahkan kesini
 */ 
protected $redirectAfterLogout = '/';
```

### Throttles Logins

Jika user mencoba beberapa kali login dan gagal sebanyak 5 kali, maka fitur login tidak akan bisa digunakan selama 60 detik. Untuk mengubah behaviour ini tambahkan di `app/Http/Auth/AuthController.php` property berikut

```php
protected $maxLoginAttempts = 10;

protected $lockoutTime = 120;
```

### Authentikasi Manual

Jika anda ingin menggunakan cara manual untuk authentikasi, anda bisa mengganti routing dan controller default. Contoh pada `app/Http/routes.php`

```php
Route::get('login', function()
{
    return view('login');
});

Route::post('login', function()
{
    $credentials = request()->only('email', 'password');
    $remember = request('remember');
    
    if (auth()->attempt($credentials, $remember))
    {
        return redirect()->intended('/');
    }
    
    return redirect()->back()->withMessage('Invalid Credentials');
});
```

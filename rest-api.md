---
currentMenu: rest-api
---

REST API
========

Disini kita akan bahas secara singkat cara membuat REST API dengan output berupa JSON. Yang pertama kita butuhkan adalah membuat routing baru dan kita asumsikan base url untuk REST API ini adalah `/api`.

Buat basic routing untuk REST API.

```php
Route::group(['prefix' => 'api'], function() {

    Route::get('/', function() {
        // Jika ada yang mengakses http://localhost:8000/api
        // tampilkan dokumentasi.
        return View::make('api/docs');
    });

});
```

Setelah itu kita tambahkan routing untuk mengambil data dari seorang user. Tambahkan ini di dalam group.

```php
Route::get('user', function($id) {
    return App\User::find($id);
});
```

Sekarang kita bisa *hit* http://localhost/api/user/1 untuk mendapatkan semua data dari user tersebut. Semua data user akan tampil, kecuali yang dimasukkan ke `$hidden` pada `User` model. Jika kita lihat di `app/User.php`, di sana ada 

```php
protected $hidden = ['password', 'remember_token'];
```

Transformation
--------------

 Kadangkala anda membutuhkan transformasi sebelum data dijadikan JSON. Misalnya JSON output yang tampil adalah:

 ```json
{
    "username"   : "mul14",
    "name"       : "Mulia Arifandi Nasution",
    "age"        : "14",
    "last_login" : "2015-12-13 12:34:56",
    "created_at" : "2015-08-14 11:22:33",
    "updated_at" : "2015-10-30 01:02:03"
}
 ```

Jika kita perhatikan `age` yang muncul berupa string. Saya ingin `age` ini berupa integer. Dan saya tidak butuh `created_at` dan `updated_at`. Saya asumsikan pada `User` model `last_login` sudah ditambahkan pada `$dates`. Sekarang kita lakukan transformasi.

```php
Route::get('user', function($id) {
    
    $user = App\User::find($id);

    $user->transform(function($u) {

        return [
            'name'       => $u->name,
            'username'   => $u->username,
            'email'      => $u->email,
            'age'        => (int) $u->age, // Integer type casting 
            'last_login' => $u->last_login->diffForHuman(),
        ];
    
    });

    return $user;

});
```

Sekarang data yang tampil akan menjadi seperti ini

```json
{
    "name"       : "Mulia Arifandi Nasution",
    "username"   : "mul14",
    "email"      : "mul14@ganteng.com",
    "age"        : 14,
    "last_login" : "4 months ago"
}
```

As simple as that ;)

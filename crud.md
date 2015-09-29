---
currentMenu: authentication
---

CRUD - Query Builder
====================

Untuk melakukan proses CRUD di Laravel sangat mudah. Pertama hal yang perlu kita
persiapkan adalah konfigurasi database. Anda bisa edit file `.env` atau edit
file `config/database.php`. Sesuaikan konfigurasi dengan database anda.

Setelah konfigurasi selesai, anda bisa buat table baru dengan menggunakan
database client seperti PhpMyAdmin, SequelPro, pgAdmin, Chrome MySQL Admin, dll.
Atau anda juga bisa membuat migration.

Pada contoh disini saya menggunakan migration bawaan Laravel yang akan membuat
table `users`. Setelah konfigurasi database, jalankan artisan.

```bash
php artisan migrate
```

Setelah itu, anda bisa buat routing baru. Misalnya

```php
Route::get('user', function(){

    // Code operasi CRUD disini

});
```

(**C**)reate
------------

Memasukkan data baru ke database.

```php
DB::table('users')->insert([
    'name' => 'kumis',
    'email' => 'kumis@example.com',
    'password' => bcrypt('p4$sw0Rd'),
    'created_at' => Carbon\Carbon::now(),
    'updated_at' => Carbon\Carbon::now(),
]);

// Sama dengan
// INSERT INTO `users` (name, email, password, created_at, updated_at)
// VALUES ('Kumis', 'kumis@example.com', 'password', NOW(), NOW());
```

Karena kita tidak menggunakan Eloquent, data `created_at` dan `updated_at` harus
kita masukkan secara manual.

### Batch insert - Memasukkan beberapa data baru sekaligus

```php
$users = [
    [
        'name' => 'Jenggot',
        'email' => 'jenggot@example.com',
        'password' => bcrypt('p4$sw0Rd'),
        'created_at' => Carbon\Carbon::now(),
        'updated_at' => Carbon\Carbon::now(),
    ],
    [
        'name' => 'Jambang',
        'email' => 'jambang@example.com',
        'password' => bcrypt('p4$sw0Rd'),
        'created_at' => Carbon\Carbon::now(),
        'updated_at' => Carbon\Carbon::now(),
    ],
    [
        'name' => 'alis',
        'email' => 'alis@example.com',
        'password' => bcrypt('p4$sw0Rd'),
        'created_at' => Carbon\Carbon::now(),
        'updated_at' => Carbon\Carbon::now(),
    ],
];

DB::table('users')->insert($users);

// Sama dengan
// INSERT INTO `users` (name, email, password, created_at, updated_at)
// VALUES
// ('Jenggot', 'jenggot@example.com', 'password', NOW(), NOW()),
// ('Jambang', 'jambang@example.com', 'password', NOW(), NOW()),
// ('Alis', 'alis@example.com', 'password', NOW(), NOW());
```

(**R**)ead
------------

### Mengambil semua data

```php
return DB::table('users')->all();

// Sama dengan
// SELECT * FROM `users`;
```

> Semua collection atau array yang di-"return" dari suatu routing, otomatis akan
diubah menjadi JSON.

### WHERE - AND

```php
    return DB::table('users')
             ->where('name', 'kumis')
             ->where('email', 'kumis@example.com')
             ->get();

    // Sama dengan
    // SELECT * FROM `users`
    // WHERE name = 'kumis' AND email = 'kumis@example.com';
```

### WHERE - OR

```php
    return DB::table('users')
             ->where('name', 'kumis')
             ->orWhere('name', 'jenggot')
             ->get();

    // Sama dengan
    // SELECT * FROM `users`
    // WHERE name = 'kumis' OR name = 'jenggot';
```

### WHERE - LIKE

```php
return DB::table('users')
         ->where('name', 'LIKE', '%j%')
         ->get();

// Sama dengan
// SELECT * FROM `users`
// WHERE name LIKE '%j%';
```

(**U**)pdate
------------

Coming soon

(**D**)elete
------------

```php
DB::table('users')
  ->where('id', 1)
  ->delete();

// Sama dengan
// DELETE FROM `users` WHERE id = '1';
```

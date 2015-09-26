XAMPP
=====

Bagaimana cara menghilangkan `public`?
--------------------------------------

### Overview

Pertanyaan ini sering dilontarkan pengguna XAMPP. XAMPP pada dasarnya menggunakan Apache HTTPD sebagai web server-nya. Untuk development, sebenarnya anda tidak harus menggunakan Apache HTTPD. Anda bisa menggunakan php built-in web server untuk development. Detailnya anda bisa baca artikel di blog saya tentang [You don't need XAMPP](https://mul14.wordpress.com/2015/05/01/you-dont-need-xampp/).

Laravel meletakkan file `index.php`, file yang akan dibaca pertama kali oleh web server di folder `public`. Itulah mengapa, ketika menggunakan web server dengan konfigurasi default XAMPP, anda perlu menambahkan `public`.

Sebenarnya ini bukan hanya dilakukan oleh Laravel. Ini juga dilakukan oleh PHP Framework lain seperti Symfony 2, CakePHP, Yii.

* CakePHP meletakkan file `index.php` pada folder `webroot` https://github.com/cakephp/app/tree/master/webroot

* Yii 2 Basic meletakkan file `index.php` pada folder `web` https://github.com/yiisoft/yii2-app-basic/tree/master/web

* Yii 2 Advanced meletakkan file `index.php` pada folder `frontend/web` dan `backend/web` https://github.com/yiisoft/yii2-app-advanced/tree/master/frontend/web, https://github.com/yiisoft/yii2-app-advanced/tree/master/backend/web

* Symfony 2 akan membaca file `app.php` pertama kali pada folder `web` https://github.com/symfony/symfony-standard/tree/2.8/web

### Solusi #1 - Gunakan Artisan Serve

Gunakan perintah `php artisan serve` dan buka http://localhost:8000

Port 8000 digunakan karena port 1-1023 membutuhkan privileges di level OS. By default Apache HTTPD menggunakan port 80. Itulah mengapa jika anda menggunakan Windows, setiapkali mengaktifkan web server, anda masuk ke [UAC](https://en.wikipedia.org/wiki/User_Account_Control). Dan jika menggunakan XAMPP for Linux anda juga harus menggunakan `sudo`.


### Solusi #2 - Pindahkan folder public

Pindahkan isi folder `public` ke tempat lain.

```
D:
└── xampp
    └── htdocs
        └── aplikasiku
            ├── app
            ├── bootstrap
            ├── config
            ├── ...
            └── public
```

Keluarkan aplikasiku ke tempat lain.

```
D:
├── xampp
|   └── htdocs
└── aplikasiku
    ├── app
    ├── bootstrap
    ├── config
    ├── ...
    └── public
```

Masukkan public ke htdocs

```
D:
├── xampp
|   └── htdocs
|       └── public
└── aplikasiku
    ├── app
    ├── bootstrap
    ├── config
    └── ...
```

Lalu ubah file isi `public/index.php`

```php
require __DIR__.'/../bootstrap/autoload.php';
// MENJADI
require 'd:/aplikasiku/bootstrap/autoload.php';

$app = require_once __DIR__.'/../bootstrap/app.php';
// MENJADI
$app = require_once 'd:/aplikasiku/bootstrap/app.php';
```

Sekarang anda bisa buka http://localhost/public.

Lalu ubah nama `public` menjadi `aplikasiku`, dan sekarang kita bisa buka http://localhost/aplikasiku

### Solusi #3 - Gunakan Symlink

Anda menggunakan *nix? Well, anda lebih beruntung daripada pengguna Windows. Karena kita bisa menggunakan symlink.

Saya asumsikan project anda ada di `~/Code/aplikasiku`, dan anda menggunakan XAMPP for Linux. Lokasi `htdocs` pada XAMPP for Linux ada di `/opt/lampp/htdocs`. Mari kita buat symlink

```
ln -s ~/Code/aplikasiku/public /opt/lampp/htdocs/aplikasiku
```

### Solusi #4 - Gunakan Homestead

Silahkan baca dokumentasi http://laravel.com/docs/master/homestead

### Solusi #5 - Apache HTTPD Virtual Host

Coming Soon

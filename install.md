# Instalasi

Laravel dibangun dengan menggunakan Composer. Jadi Composer wajib ada di sistem anda. Silahkan download composer di http://getcomposer.org.

Anda bisa memilih salah satu cara instalasi berikut

## Install dengan composer

Gunakan perintah berikut pada Terminal atau Command Prompt anda.

```
composer create-project laravel/laravel [folder_anda]
```

Misalnya saya mau membuat suatu website dengan nama ngintip. Maka ketik di Terminal

```
composer create-project laravel/laravel ngintip
```

Bila anda lupa bagaimana cara menggunakan composer untuk membuat project Laravel, cukup ketik `composer`, maka akan muncul informasi bantuan. Disana anda bisa lihat ada perintah `create-project`. Gunakan 

```
composer create-project --help
```

Untuk melihat informasi cara menggunakan perintah `create-project`. 

Anda juga bisa menyingkat perintah, cukup dengan

```
composer create
```

atau 

```
composer cr
```

Composer akan memilih perintah yang paling dekat dan tidak ambigu.

## Install dengan Laravel Installer

Untuk menggunakan Laravel Installer, anda juga butuh composer. Mari kita install Laravel Installer

```
composer global require "laravel/installer=~1.1"
```

Setelah proses instalasi selesai, kita bisa gunakan perintah `laravel` di Terminal. Gunakan command `new` untuk membuat project Laravel yang baru.

```
laravel new [folder_anda]
```

Pada dasarnya Laravel installer ini akan men-download file dari http://cabinet.laravel.com/latest.zip, lalu di-extract dan jalankan composer script.

## Install dengan cara download released file

Anda bisa juga download file zip langsung dari GitHub https://github.com/laravel/laravel/releases. Di sana anda bisa memilih download file zip atau tarball.

Setelah download file ini, anda tetap harus menjalankan `composer install` untuk men-download Laravel core. Karena sebenarnya yang anda download di GitHub itu adalah project skeleton-nya Laravel, tanpa folder `vendor`.

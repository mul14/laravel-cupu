# Shared Hosting

## Minimum Requirement

Pastikan shared hosting yang anda pilih sudah memenuhi mininum system requirement-nya Laravel. Informasi paling up-to-date dapat anda lihat di [dokumentasi resmi](http://laravel.com/docs/master)

Untuk versi 5.1 LTS berikut minimum kebutuhannya:

* PHP >= 5.5.9
* OpenSSL PHP Extension
* PDO PHP Extension
* Mbstring PHP Extension
* Tokenizer PHP Extension

Anda selalu bisa bertanya pada tempat shared hosting yang akan anda pilih melalui email, fasilitas chat, maupun open ticket. Minta tunjukkan `phpinfo()`. Dari sana anda bisa dapat informasi apakah shared hosting yang akan anda pilih bisa digunakan oleh Laravel.

## Deploy

Untuk men-deploy Laravel ke shared hosting, intinya adalah folder `public` yang akan dibaca oleh web server pertama kali. Yang mana folder `public` ini didalamnya ada file `index.php`

Jadi bila shared hosting anda membaca folder `public_html`, maka seharusnya ada file `index.php` milik Laravel disana.

Anda bisa mengubah beberapa parameter yang ada di dalam file `public/index.php` untuk menyesuaikan path-nya.

> Cara ini sebenarnya bukan hanya diterapkan oleh Laravel, PHP framework lain seperti Symfony 2, CakePHP, Yii 2 juga menerapkan hal yang sama. Karena cara ini lebih aman. Tidak seharusnya file aplikasi anda bisa diakses langsung melalui suatu url.

### FTP Client

Anda bisa menggunakan FTP client seperti FileZilla, WinSCP, CuteFTP, Transmit, gFTP, ataupun ftp command line untuk melakukan proses deploy.

Silahkan gunakan search engine seperti Google, Bing, Yahoo untuk mencari informasi FTP client apa yang cocok anda gunakan.

### Git FTP

Jika anda menggunakan [git version control](http://git-scm.org), anda dapat menggunakan [git-ftp](https://github.com/git-ftp/git-ftp) untuk melakukan deploy. File-file yang di-upload melalui FTP **hanya file-file yang mengalami perubahan**.

Untuk informasi cara instalasi dan penggunaan git-ftp, dapat anda lihat di https://github.com/git-ftp/git-ftp

### IDE

Biasanya di IDE ada fitur untuk melakukan upload ke FTP. Anda bisa lihat dokumentasi cara setup dan deploy menggunakan IDE pada website resmi IDE yang anda gunakan.

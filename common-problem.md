# Problem Umum

Disini kita akan bahas masalah yang sering dihadapi pengguna Laravel pemula. 

## Command Not Found

Misalnya saat ketik `composer` muncul error message "command not found", atau jika anda menggunakan Windows, error message yang dikeluarkan akan seperti ini

> 'composer' is not recognized as an internal command or external command, operable program or batch file.

Itu artinya perintah `composer` tidak dikenali di sistem anda. Sebenarnya jika anda ketik apapun, pasti error message yang keluar juga sama. Misalnya anda ketik `kumis`, `jenggot`, `jambang`.

Solusinya adalah dengan memanggil perintahnya dimana file itu berada. Atau cara yang lebih mudah dengan menambahkan environment variable `PATH`.

Pada **nix-like system* seperti Linux, BSD atau Mac OS X anda bisa menambahkan ini pada file `~/.bashrc`

```bash
export PATH=$HOME/bin/composer:$PATH
```

Pada Windows, jika anda menggunakan instalasi `composer-setup.exe`, masalah ini seharusnya tidak ada, karena installer akan otomatis menambahkan lokasi file composer ke `%PATH%`.

# Lab8Web

# Pertama buatlah folder dengan nama "latihan1" setelah itu buatlah table.

`Untuk codenya bisa menggunakan dibawah ini:`

```html
<?php

include("koneksi.php");

$id = $_GET["id"];
$query = "DELETE FROM data_barang WHERE id_barang = $id ";

mysqli_query($conn, $query);
header("location: index.php");
```

`Note` 

Nyalakan Apache dan Mysql pada app XAMPP terlebih dahulu


`Selanjutnya Menambahkan Data`


Untuk codenya bisa mengggunakan dibawah ini:

```html
<?php

include("koneksi.php");

$id = $_GET["id"];
$query = "DELETE FROM data_barang WHERE id_barang = $id ";

mysqli_query($conn, $query);
header("location: index.php");

```
Untuk hasilnya akan seperti ini:

![tampilan menambah data](https://github.com/MikaelRivaldo/Lab8Web/assets/115770247/886fb989-7ce0-4506-8e5e-b9ad62ba1f56)

`Selanjutnya Membuat Program CRUD`

Buat folder baru dengan nama lab8_php_database dan simpan pada directory web server

Kemudian untuk mengakses direktory tersebut pada web server dengan mengakses URL:
http://localhost/lab8_php_database/

![tampilan crud](https://github.com/MikaelRivaldo/Lab8Web/assets/115770247/d57ae73f-35f3-4afd-aa13-4699256af602)


`Selantnya Membuat file koneksi database
Buat file baru dengan nama koneksi.php`

Untuk codenya bisa menggunakan dibawah ini:

```html
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db = "latihan1";
$conn = mysqli_connect($host, $user, $pass, $db);
if ($conn == false)
{
echo "Koneksi ke server gagal.";
die();
} #else echo "Koneksi berhasil";
?>
```

Untuk hasilnya akan seperti ini:

![tapilan koneksi berhasil](https://github.com/MikaelRivaldo/Lab8Web/assets/115770247/10085817-84c5-4896-933e-4407f75d7977)



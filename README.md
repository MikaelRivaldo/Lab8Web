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

`Selantnya Membuat file index untuk menampilkan data (Read)
Buat file baru dengan nama index.php

Untuk codenya bisa menggunakan dibawah ini:

```html
<?php
include("koneksi.php");
// query untuk menampilkan data
$sql = 'SELECT * FROM data_barang';
$result = mysqli_query($conn, $sql);
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Data Barang</title>

</head>
<body>
    <div class="container">
        <h1>Data Barang</h1>
        <a href="plus.php"> Tambah Barang</a>
        <div class="main">
            <table>
            <tr>
                <th>Gambar</th>
                <th>Nama Barang</th>
                <th>Katagori</th>
                <th>Harga Jual</th>
                <th>Harga Beli</th>
                <th>Stok</th>
                <th>Aksi</th>
            </tr>
            <?php if($result): ?>
            <?php while($row = mysqli_fetch_array($result)): ?>
            <tr>
                <td><img src="gambar/<?= $row['gambar'];?>" alt="<?=$row['nama'];?>"></td>
                <td><?= $row['nama'];?></td>
                <td><?= $row['kategori'];?></td>
                <td><?= $row['harga_beli'];?></td>
                <td><?= $row['harga_jual'];?></td>
                <td><?= $row['stok'];?></td>
                <td><a href="ubah.php?id=<?= $row['id_barang']; ?>">ubah</a>
                <a href="hapus.php?id=<?= $row['id_barang']; ?>">hapus</a></td>
            </td>
            </tr>
            <?php endwhile; else: ?>
            <tr>
                <td colspan="1">Belum ada data</td>
            </tr>
            <?php endif; ?>
            </table>
        </div>
    </div>
</body>
</html>
```
Untuk hasilnya akan seperti ini:

![data barang](https://github.com/MikaelRivaldo/Lab8Web/assets/115770247/5a94a4ae-cc4e-42a7-bf0e-5e232257c8bb)

`Selantnya Membuat file Mengubah Data (Update)
Buat file baru dengan nama ubah.php

Untuk codenya bisa menggunakan dibawah ini:


```html
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';
if (isset($_POST['submit'])) {
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;
    if ($file_gambar['error'] == 0) {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . '/gambar/' . $filename;
        if (move_uploaded_file($file_gambar['tmp_name'], $destination)) {
            $gambar = 'gambar/' . $filename;;
        }
    }
    $sql = 'INSERT INTO data_barang (nama, kategori,harga_jual, harga_beli,
stok, gambar) ';
    $sql .= "VALUE ('{$nama}', '{$kategori}','{$harga_jual}',
'{$harga_beli}', '{$stok}', '{$gambar}')";
    $result = mysqli_query($conn, $sql);
    header('location: index.php');
}

?>
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Tambah Barang</title>
</head>

<body>
    <div class="container">
        <h1>Tambah Barang</h1>
        <div class="main">
            <form method="post" action="tambah.php" enctype="multipart/form-data">
                <div class="input">
                    <label>Nama Barang</label>
                    <input type="text" name="nama" />
                </div>
                <div class="input">
                    <label>Kategori</label>
                    <select name="kategori">
                        <option value="Komputer">Komputer</option>
                        <option value="Elektronik">Elektronik</option>
                        <option value="Hand Phone">Hand Phone</option>
                    </select>
                </div>
                <div class="input">
                    <label>Harga Jual</label>
                    <input type="text" name="harga_jual" />
                </div>
                <div class="input">
                    <label>Harga Beli</label>
                    <input type="text" name="harga_beli" />
                </div>
                <div class="input">
                    <label>Stok</label>
                    <input type="text" name="stok" />
                </div>
                <div class="input">
                    <label>File Gambar</label>
                    <input type="file" name="file_gambar" />
                </div>
                <div class="submit">
                    <input type="submit" name="submit" value="Simpan" />
                </div>
            </form>
        </div>
    </div>
</body>

</html>
```

Untuk hasilnya akan seperti ini:

![ubah](https://github.com/MikaelRivaldo/Lab8Web/assets/115770247/11199dab-a867-4811-9871-cc1136d54ab1)

# Selanjutnya Menghapus Data (Delete)
Buat file baru dengan nama hapus.php

Untuk codenya bisa menggunakan dibawah ini:

```html
<?php
include_once 'koneksi.php';
$id = $_GET['id'];
$sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
header('location: index.php');
?>
```







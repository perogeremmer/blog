# Part 6 — Menampilkan Data Pada Select

# Overview

Sekarang kita akan mencoba melakukan menampilkan data kategori pada select.

## Buat Tabel Category

Pertama kita memerlukan tabel user dengan query berikut:

```sql
CREATE TABLE `inventory`.`category` (
    `id` INT NOT NULL AUTO_INCREMENT , 
    `name` VARCHAR(260) NOT NULL , `description` TEXT NOT NULL , `created_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP , `updated_at` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP , 
    PRIMARY KEY (`id`)
);
```

## Tambahkan Relasi

Karena kita sudah memiliki kolom `category_id` pada table `inventory`, kita hanya perlu menambahkan relasi.

```sql
ALTER TABLE `inventory` ADD FOREIGN KEY (`category_id`) REFERENCES `category`(`id`) ON DELETE RESTRICT ON UPDATE RESTRICT;
```

## Tambah data Dummy

Terakhir kita tambah data Dummy agar memiliki default data:

```sql
INSERT INTO `category` (
    `id`, `name`, `description`, `created_at`, `updated_at`) 
    VALUES (
        NULL, 'Peralatan Mandi', 'Peralatan Mandi', current_timestamp(), current_timestamp()
    ), (
        NULL, 'Makanan', 'Makanan', current_timestamp(), current_timestamp()
    )
```

## Tambah File Category

Pada folder `database`, kita buat file baru bernama `category.php` masukkan kode berikut:

```php
<?php

    class Category {

        function __construct()
        {
            $this->db = new ConnectionDatabase();
        }

        function getAll(){
            $query = "SELECT * FROM category";
            $data = mysqli_query($this->db->connection, $query);
            
            $res = [];
    
            while($item = mysqli_fetch_array($data)) {
                $res[] = $item;
            }

            $this->db->closeConnection();
    
            return $res;
        }

    }
?>
```

Lalu kita modifikasi sedikit file inventory.php pada folder database dengan kode berikut:

```php
<?php
    include('connection.php');
    include('category.php');

    class Inventory {
        .
        .
        .
```

Sekarang kita melakukan include terhadap class category pada file inventory.

## Ubah file `create.php`

Sekarang kita ubah file `create.php` agar menjadi seperti ini:

```php
<!doctype html>
<html lang="en">
<head>
    <?php include('components/header.php') ?>
</head>

<body>
    <?php include('components/navbar.php') ?>

    <main role="main " class="container">
        
        <?php include('components/welcome_message.php') ?>

        <?php 
            include('database/inventory.php');

            $category = new Category();
        ?>

        <div class="container mt-5">
            <div class="row mb-4">
                <div class="col-12">
                    <h5 class="mb-4">Create Inventory</h5>
                    <form action="controller/inventory.php?action=store" method="POST">
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Product Name</label>
                            <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Input product name" name="name">
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Stock</label>
                            <input type="number" class="form-control" id="exampleFormControlInput1" placeholder="Input product stock" name="stock">
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Category</label>
                            <select class="form-control" name="category">
                                <?php foreach($category->getAll() as $item) { ?>
                                    <option value="<?= $item['id'] ?>"> <?= $item['name'] ?></option>
                                <?php } ?>
                            </select>
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Expired at</label>
                            <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Input product expired at" name="expired_at">
                        </div>
                        <div class="mb-3">
                            <button type="submit" class="btn btn-primary">
                                Submit
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </main>

    <?php include('components/footer.php') ?>

    <?php include('components/scripts.php') ?>
</body>

</html>
```

Kalau kamu perhatikan, perubahan yang jelas terdapat pada:

```php
<?php 
    include('database/inventory.php');

    $category = new Category();
?>
```

dan bagian berikut:

```php
<div class="mb-3">
    <label for="exampleFormControlInput1" class="form-label">Category</label>
    <select class="form-control" name="category">
        <?php foreach($category->getAll() as $item) { ?>
            <option value="<?= $item['id'] ?>"> <?= $item['name'] ?></option>
        <?php } ?>
    </select>
</div>
```

Kita ingin menambahkan bagian baru supaya seluruh data category bisa masuk pada saat membuat data baru.

## Ubah file `edit.php`

Ubah juga file `edit.php` agar menjadi seperti ini:

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <?php include('components/header.php') ?>
</head>

<body>
    <?php include('components/navbar.php') ?>

    <main role="main " class="container">
        
        <?php include('components/welcome_message.php') ?>
        
        <?php 
            include('database/inventory.php');
            $id =  $_GET['id'];

            $data = new Inventory();
            $data = $data->show($id);
            
            $category = new Category();
        ?>

        <div class="container mt-5">
            <div class="row mb-4">
                <div class="col-12">
                    <h5 class="mb-4">Detail Product <?= $data['name'] ?></h5>
                    <form action="controller/inventory.php?id=<?= $data['id'] ?>&action=update" method="POST">
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Product Name</label>
                            <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Input product name" name="name" value="<?= $data['name'] ?>">
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Stock</label>
                            <input type="number" class="form-control" id="exampleFormControlInput1" placeholder="Input product stock" name="stock" value="<?= $data['stock'] ?>"">
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Category</label>
                            <select class="form-control" name="category">
                                <?php foreach($category->getAll() as $item) { ?>
                                    <option value="<?= $item['id'] ?>" 
                                        <?= ($item['id'] == $data['category_id'] ? "selected='selected'" : "" ) ?> > 
                                            <?= $item['name'] ?>
                                    </option>
                                <?php } ?>
                            </select>
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Expired at</label>
                            <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Input product expired at" name="expired_at" value="<?= $data['expired_at'] ?>">
                        </div>
                        <div class="mb-3">
                            <button type="submit" class="btn btn-primary">
                                Submit
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </main>

    <?php include('components/footer.php') ?>

    <?php include('components/scripts.php') ?>
</body>

</html>
```

Perhatikan kode berikut:

```php
<div class="mb-3">
    <label for="exampleFormControlInput1" class="form-label">Category</label>
    <select class="form-control" name="category">
        <?php foreach($category->getAll() as $item) { ?>
            <option value="<?= $item['id'] ?>" 
                <?= ($item['id'] == $data['category_id'] ? "selected='selected'" : "" ) ?> > 
                    <?= $item['name'] ?>
            </option>
        <?php } ?>
    </select>
</div>
```

Pada bagian ini agak sedikit beda, karena kita menggunakan kondisi sebagai berikut:

```php
<?= ($item['id'] == $data['category_id'] ? "selected='selected'" : "" ) ?>
```

Apabila id item dari `category` yang sedang di-looping sama dengan `category_id` yang berada pada nilai inventory, maka kita cetak tulisan `"selected='selected'"`. Hal ini bertujuan agar nilai yang sama, agar menjadi kursor utama pada saat data ingin diubah.

## Ubah Controller

Terakhir, kita ubah `inventory.php` pada folder `controller` dengan kode berikut:

```php
<?php

include '../database/inventory.php';

$inventory = new Inventory();

$action =  $_GET['action'];

if ($action == "store") {
    $inventory->store(
        $_POST['name'],
        $_POST['stock'],
        $_POST['expired_at'],
        $_POST['category']
    );
    return header("location:../");
}
else if ($action == "update") {
    $inventory->update(
        $_GET['id'],
        $_POST['name'],
        $_POST['stock'],
        $_POST['expired_at'],
        $_POST['category']
    );
    return header("location:../");
}
else if ($action == "delete") {
    $inventory->delete(
        $_GET['id']
    );
    return header("location:../");
}

?>
```

Yap, kita hanya menambahkan satu parameter baru untuk memasukkan `category`.

Sekarang coba jalankan dan lihat hasilnya!
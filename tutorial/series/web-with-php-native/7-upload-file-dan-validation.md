# Part 7 — Upload file dan Validation

# Overview

Sekarang kita akan mencoba melakukan menampilkan data kategori pada select.

## Tambahkan Kolom Gambar

Pertama, kita menambahkan tabel baru dengan query berikut:

```sql
ALTER TABLE `inventory` ADD `image` VARCHAR(300) NULL DEFAULT NULL AFTER `category_id`;
```

Sekarang, kita tambahkan beberapa method baru pada `database/inventory.php`:

```php
function process_upload($image) {
    $target_dir = dirname(getcwd()) . DIRECTORY_SEPARATOR . 'uploads' . DIRECTORY_SEPARATOR;

    if (!is_dir($target_dir)) {
        mkdir($target_dir, 0777, true);
    }

    $imageFileType = strtolower(pathinfo($image['name'], PATHINFO_EXTENSION));

    $uniqueId = uniqid();
    $newFileName = $uniqueId . '.' . $imageFileType;
    $fileNameWithFolder = DIRECTORY_SEPARATOR . 'uploads' . DIRECTORY_SEPARATOR . $uniqueId . '.' . $imageFileType;

    $target_file = $target_dir . $newFileName;
    if ($image["size"] > 500000) {
        return array("errors" => true, "values" => "Sorry, your file is too large.");
    }

    $allowedTypes = array("jpg", "jpeg", "gif", "png");
    if (!in_array($imageFileType, $allowedTypes)) {
        return array("errors" => true, "values" => "Sorry, only JPG, JPEG, PNG & GIF files are allowed.");
    }

    if (move_uploaded_file($image["tmp_name"], $target_file)) {
        return array("errors" => false, "values" => $fileNameWithFolder);
    } else {
        return array("errors" => true, "values" => "Sorry, there was an error uploading your file. Please check permissions for the target directory.");
    }
}
```

Kita bedah kodenya:

- `$target_dir = dirname(getcwd()) . DIRECTORY_SEPARATOR . 'uploads' . DIRECTORY_SEPARATOR;`: Artinya kita mau dapetin directory supaya jadinya kaya gini contohnya: C:\xampp\htdocs\inventory\uploads
- `mkdir($target_dir, 0777, true);`: Kalo misalnya directorynya gak ada atau foldernya belum kebuat, kita buatin foldernya dengan permission 0777 artinya semua user yang berjalan pada komputer kita boleh mengakses, membaca, membuka, dan mengeksekusi file apapunya ada di folder itu.
- `$imageFileType = strtolower(pathinfo($image['name'], PATHINFO_EXTENSION));`: Artinya kita kecilin huruf dari nama file yang kita upload, tapi kita ambil extensionnya aja, misalnya .png, atau .jpg
- `$fileNameWithFolder = DIRECTORY_SEPARATOR . 'uploads' . DIRECTORY_SEPARATOR . $uniqueId . '.' . $imageFileType;`: Artinya kita bikin string baru yang hasilnya mirip-mirip gini `\uploads\unique-id.extension`. Tujuannya karena kita mau nyimpen nilai ini di database.
- `$image["size"] > 500000`: Kita cek apakah ukuran file yang kita upload lebih besar dari 5 megabytes. Ohiya, kenapa ukurannya yang diperiksa adalah 500000 karena ukuran aslinya adalah `bytes`.
- `!in_array($imageFileType, $allowedTypes)`: Kita meriksa, ada gak sih extension yang kita upload ini masuk ke tipe extension yang diizinkan gak.
- `move_uploaded_file($image["tmp_name"], $target_file)`: Kita pindahin file yang mau diupload, dengan nama temporary tadi, ke tempat yang kita inginkan, misal nama file awalnya adalah foto.jpg, nah foto.jpg ini akan pindah ke directory uploads dengan nama baru, misalnya ua2841.jpg. Tujuannya supaya nama filenya unique dan gak niban file satu sama lain.



Sekarang kita juga perbaiki method `store` dan `update`:

```php
function store($name, $stock, $expired_at, $category_id, $image=null){
    $query = "INSERT INTO `inventory` (`name`, `stock`, `expired_at`, `category_id`, `image`) VALUES (?,?,?,?, ?)";

    $process = $this->database->connection->prepare($query);

    if($process) {
        if ($image) {
        $upload = $this->process_upload($image);

        if ($upload['errors']) {
            return $upload;
        }
        
        }
        $process->bind_param('sssss', $name, $stock, $expired_at, $category_id, $upload['values']);
        $process->execute();
    } else {
        $error = $this->database->connection->errno . ' ' . $this->database->connection->error;
        echo $error;
    }
    
    $process->close();
    $this->database->closeConnection();            

    return true;
}

function update($id, $name, $stock, $expired_at, $category_id, $image=null){
    $query = "UPDATE `inventory` SET `name` = ?, `stock` = ?, `expired_at` = ?, `category_id` = ?, `image` = ? WHERE id = ?";
    $process = $this->database->connection->prepare($query);

    if($process) {
        if ($image) {
            $upload = $this->process_upload($image);
            
            if ($upload['errors']) {
                return $upload;
            }
            
            }

        $process->bind_param('ssssss', $name, $stock, $expired_at, $category_id, $upload['values'], $id);
        $process->execute();
    } else {
        $error = $this->database->connection->errno . ' ' . $this->database->connection->error;
        echo $error;
    }
    
    $process->close();
    $this->database->closeConnection();            

    return true;
}
```

Sekarang kita ubah `controller/inventory.php`:

```php
<?php

session_start();

include '../database/inventory.php';

$inventory = new Inventory();
$action =  $_GET['action'];

if ($action == "store") {
    $store = $inventory->store(
        $_POST['name'],
        $_POST['stock'],
        $_POST['expired_at'],
        $_POST['category'],
        $_FILES["image"],
    );

    if($store['errors']) {
        $_SESSION['errors'] = true;
        $_SESSION['values'] = $store['values'];
        return header("location:../create.php");
    }
    
    return header("location:../");
}
else if ($action == "update") {
    $update = $inventory->update(
        $_GET['id'],
        $_POST['name'],
        $_POST['stock'],
        $_POST['expired_at'],
        $_POST['category'],
        $_FILES["image"],
    );

    if ($update['errors']) {
        return header("location:../create.php");
    }
    
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

Kalau diperhatikan, biasanya kita pake `$_POST`, tapi untuk file sendiri beda, kita pakenya `$_FILES` karena format file ini biasanya diambil dari binary.


Sekarang kita ubah create.php, agar bisa melakukan upload file:

```html
<!doctype html>
<html lang="en">
<head>
    <?php include('components/header.php') ?>
</head>

<body>
    <?php session_start(); ?>
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
                    <?php include('components/errors.php') ?>

                    <h5 class="mb-4">Create Inventory</h5>
                    <form action="controller/inventory.php?action=store" method="POST" enctype="multipart/form-data">
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
                            <label for="exampleFormControlInput1" class="form-label">Image</label>
                            <input type="file" name="image" id="image">
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

Sekarang ubah file index.php pada bagian tbody dengan kode berikut:

```php
<tbody> 
    <?php foreach($data->getAll() as $item) { ?> 
    <tr>
      <td> <?= $item['name'] ?> </td>
      <td> <?= $item['stock'] ?> </td>
      <td> <?= $item['category_name'] ?> </td>
      <td> <img src="/belajarphp/<?= $item['image'] ?>" width=100 /> </td>
      <td> <?= $item['expired_at'] ?> </td>
      <td> <?= $item['created_at'] ?> </td>
      <td> <?= $item['updated_at'] ?> </td>
      <td>
        <div class="btn-group " role="group " aria-label="Basic example ">
          <a href="edit.php?id=<?= $item['id'] ?>" class="btn btn-info text-white ">
            <i class="bx bx-pencil"></i>
          </a>
          <form onsubmit="return confirm('Do you really want to delete item?')" 
       action="controller/inventory.php?id=<?= $item['id'] ?>&action=delete" 
       method="POST">
            <button type="submit" class="btn btn-danger text-white">
              <i class="bx bx-trash"></i>
            </button>
          </form>
        </div>
      </td>
    </tr> 
    <?php } ?> 
</tbody>
```

> [!NOTE]
> Ganti src="/belajarphp/" dengan nama folder projekmu.


Sekarang kita ganti `edit.php` dengan kode berikut:

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
                
                <?php include('components/errors.php') ?>

                <h5 class="mb-4">Detail Product <?= $data['name'] ?></h5>
                    <form action="controller/inventory.php?id=<?= $data['id'] ?>&action=update" method="POST" enctype="multipart/form-data">
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Product Name</label>
                            <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Input product name" name="name" value="<?= $data['name'] ?>">
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Stock</label>
                            <input type="number" class="form-control" id="exampleFormControlInput1" placeholder="Input product stock" name="stock" value="<?= $data['stock'] ?>">
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
                            <?php if(isset($data['image'])) { ?>
                                <p>Gambar saat ini</p>
                                <img src="/belajarphp/<?= $data['image'] ?>" />
                                <br />
                            <?php } ?>
                            <label for="exampleFormControlInput1" class="form-label">Image</label>
                            <input type="file" name="image" id="image" />
                            <input type="hidden" name="oldImage" value="<?= $data['image'] ?>" >
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

Sekarang coba jalankan dan coba tambahkan, atau ubah gambar.
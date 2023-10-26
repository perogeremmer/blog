# Part 2 — Templating

# Overview

Setelah belajar dasar PHP kita akan membuat templating menggunakan template mirip dari sini: [Download template](https://github.com/perogeremmer/template-todo-list)

Silahkan clone template di atas lalu siapkan projeknya.

# Mulai Templating

Sekarang ubah file `index.php` menjadi seperti berikut:

```php
<!doctype html>
<html lang="en">
<head>
    <?php include('header.php') ?>
</head>

<body>
    <?php include('navbar.php') ?>

    <main role="main " class="container">
        <?php include('welcome_message.php') ?>

        <div class="container mt-5">
            <div class="row mb-4">
                <div class="col-12">
                    <h5 class="mb-4">Judul Halaman</h5>

                    <table class="table table-hover ">
                        <thead>
                            <tr>
                                <th scope="col ">Title</th>
                                <th scope="col ">Description</th>
                                <th scope="col ">Created At</th>
                                <th scope="col ">Status</th>
                                <th scope="col ">Action</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Membeli Sayur</td>
                                <td>Membeli sayur di pasar kebayoran</td>
                                <td>2 Juli 2021 - 09:00:45</td>
                                <td>
                                    <span class="badge badge-info text-white ">Done</span>
                                    <span class="badge badge-danger text-white ">Pending</span>
                                </td>
                                <td>
                                    <div class="btn-group " role="group " aria-label="Basic example ">
                                        <a href="# " class="btn btn-primary text-white ">
                                            <i class='bx bx-check'></i>
                                        </a>
                                        <a href="# " class="btn btn-info text-white ">
                                            <i class='bx bx-pencil'></i>
                                        </a>
                                        <a href="# " class="btn btn-danger text-white ">
                                            <i class='bx bx-trash'></i>
                                        </a>
                                    </div>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </main>

    <?php include('footer.php') ?>

    <?php include('scripts.php') ?>
</body>

</html>
```

Sekarang buatlah file bernama `header.php` lalu masukkan kode berikut:

```html
<!-- Required meta tags -->
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">

<!-- Bootstrap CSS -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
<link rel="stylesheet" href="css/main.css">
<link href='https://unpkg.com/boxicons@2.0.9/css/boxicons.min.css' rel='stylesheet'>

<title>Hello, world!</title>
```

Sekarang buatlah file bernama `navbar.php` lalu masukkan kode berikut:

```html
<header>
        <!-- Fixed navbar -->
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top">
            <a class="navbar-brand" href="#">Hudya</a>
            <!-- Navbar brand yo -->
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarTop" aria-controls="navbar" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="collapse navbar-collapse" id="navbarTop">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item"><a class="nav-link" href="#about">Menu 1</a> </li>
                </ul>
            </div>
        </nav>
    </header>
```

Sekarang buatlah file bernama `scripts.php` lalu masukkan kode berikut:

```html
<!-- Optional JavaScript -->
<!-- jQuery first, then Popper.js, then Bootstrap JS -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.6/umd/popper.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
```

Sekarang buatlah file bernama `welcome_message.php` lalu masukkan kode berikut:

```html
<div class="container">
    <h1 class="mt-5 ">Welcome to Belajar Bareng Hudya</h1>
    <p class="lead mb-5">Which is more difficult, coding or counting? Not both of them, the difficult one is sharing your knowledge with people without asking for the payment. <br/> <small>- Hudya</small></p>
    <p>Kunjungi blog belajar bareng Hudya dengan akses gratis <a href="https://hudya.xyz ">disini</a>.</p>
</div>
```

Sekarang buatlah file bernama `footer.php` lalu masukkan kode berikut:

```html
<footer class="footer ">
    <div class="container ">
        <span class="text-muted ">Place sticky footer content here.</span>
    </div>
</footer>
```

Sekarang buatlah folder css dan buat file `main.css` didalamnya lalu masukkan kode berikut:

```css
/* Sticky footer styles
-------------------------------------------------- */

html {
    position: relative;
    min-height: 100%;
}

body {
    /* Margin bottom by footer height */
    margin-bottom: 60px;
}

.footer {
    position: absolute;
    bottom: 0;
    width: 100%;
    /* Set the fixed height of the footer here */
    height: 60px;
    line-height: 60px;
    /* Vertically center the text there */
    background-color: #f5f5f5;
}

/* Custom page CSS
  -------------------------------------------------- */

/* Not required for template or sticky footer method. */

body>.container {
    padding: 60px 15px 0;
}

.footer>.container {
    padding-right: 15px;
    padding-left: 15px;
}

code {
    font-size: 80%;
}
```

Sekarang kita lihat hasilnya:

![Alt text](image.png)
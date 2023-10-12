# Part 5 — Membuat Sebuah Form

# Overview

Pada materi kali ini kita akan membuat form pada Bootstrap. Akan ada dua form yang kita bangun, yaitu halaman log-in dan halaman pendaftaran kontak.

# Formulir Pendaftaran Produk

Cobalah kode berikut untuk melihat formulir pendaftaran produk:

```html
<!doctype html>
<html lang="en">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">

    <title>Hello, world!</title>

    <style>
        .line-outside {
            border: 1px solid #000;
        }
    </style>
</head>

<body>
    <div class="container mt-5">
        <div class="row">
            <div class="col-12 col-md-8 offset-md-2 mb-5">
                <h1>Formulir Pendaftaran Kontak</h1>
            </div>

            <div class="col-12 col-md-8 offset-md-2 mb-5">
                <form method="GET">
                    <div class="mb-3">
                        <label class="form-label">Nama</label>
                        <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Masukkan nama pengguna" required>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Email</label>
                        <input type="email" class="form-control" id="exampleFormControlInput1" placeholder="Masukkan email. Contoh: name@example.com" required>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Pilih produk</label>
                        <select class="form-control">
                            <option value="1">Skin care</option>
                            <option value="1">Diskon Dufan</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Pilih jenis pembayaran</label>

                        <div class="form-check">
                            <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1" checked>
                            <label class="form-check-label" for="flexRadioDefault1">
                                Pembayaran Online
                            </label>
                        </div>
                        <div class="form-check">
                            <input class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault2">
                            <label class="form-check-label" for="flexRadioDefault2">
                                Pembayaran di tempat
                            </label>
                        </div>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Jumlah produk yang diinginkan</label>
                        <input type="number" class="form-control" id="exampleFormControlInput1" placeholder="Masukkan jumlah produk" required min="1" value="1">
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Alamat Pengguna</label>
                        <textarea class="form-control" id="exampleFormControlTextarea1" placeholder="Masukkan alamat pengguna" rows="3" required></textarea>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Darimana kamu mengetahui acara ini</label>

                        <div class="form-check">
                            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault">
                            <label class="form-check-label" for="flexCheckDefault">
                                Sosial Media
                            </label>
                        </div>
                        <div class="form-check">
                            <input class="form-check-input" type="checkbox" value="" id="flexCheckChecked">
                            <label class="form-check-label" for="flexCheckChecked">
                                Teman
                            </label>
                        </div>
                    </div>
                    <div class="mb-3 mt-5 text-center">
                        <button type="submit" class="btn btn-primary">Submit</button>
                        <button type="reset" class="btn btn-danger">Reset</button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj" crossorigin="anonymous"></script>
</body>
</html>
```

Lengkap sekali bukan? Kode di atas meliputi segala bentuk komponen yang ada di sebuah form seperti:

- Input text
- Input number
- Input email
- Selection
- Radio Box
- Check box
- Text area

Pada kode di atas, kita juga menambahkan atribut `required`, yaitu atribut yang menandakan bahwa elemen tersebut tidak boleh kosong.

# Halaman Sign In

Sekarang kita akan coba membuat halaman sign in, silahkan copy paste kode berikut:

```html
<!doctype html>
<html lang="en">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">

    <title>Hello, world!</title>

    <style>
        .line-outside {
            border: 1px solid #000;
        }
    </style>
</head>

<body>
    <div class="container mt-5">
        <div class="row">
            <div class="col-12 col-md-8 offset-md-2 mb-5">
                <h1>Selamat Datang di Aplikasi-ku</h1>
            </div>

            <div class="col-12 col-md-8 offset-md-2 mb-2">
                <form method="GET">
                    <div class="mb-3">
                        <label class="form-label">Email</label>
                        <input type="email" class="form-control" id="exampleFormControlInput1" placeholder="Masukkan email" required>
                    </div>
                    <div class="mb-3">
                        <label class="form-label">Password</label>
                        <input type="password" class="form-control" id="exampleFormControlInput1" placeholder="Masukkan password" required>
                    </div>
                    <div class="mb-3 mt-4">
                        <button class="form-control btn btn-primary btn-block">Sign in</button>
                    </div>
                </form>
            </div>

            <div class="col-12 col-md-8 offset-md-2 text-center">
                <p>Tidak memiliki akun? Klik
                    <a href="#">disini</a> atau
                    <a href="#">lupa kata sandi</a>
                </p>
            </div>

        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj" crossorigin="anonymous"></script>
</body>

</html>
```

Pada halaman sign in, kita menggunakan input bertipe password agar password yang dimasukkan tidak ketahuan oleh pengguna pada layar webnya.

# Latihan

Kita akan coba latihan membuat sebuah card yang kurang lebih secara konsep sama seperti mockup berikut:

[Add new card](https://dribbble.com/shots/15954863-Add-new-card)

> [!NOTE]
> 💡 Cobalah semaksimal mungkin, kalau kamu menyerah, silahkan intip kode dibawah

> [!NOTE]
> 💡 HASIL TIDAK 100% MIRIP, KITA TIDAK BANYAK MENG-CUSTOM CSS-NYA.


CODE RESULT

```html
<!doctype html>
<html lang="en">

<head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
    <link href='https://unpkg.com/boxicons@2.0.9/css/boxicons.min.css' rel='stylesheet'>

    <title>Hello, world!</title>

    <style>
        .line-outside {
            border: 1px solid #000;
        }
        
        .form-label-small {
            font-size: .8rem;
            float: left;
            position: absolute;
            margin-bottom: 100px;
        }
    </style>
</head>

<body style="background-color: #B7B9C7">
    <div class="container mt-5">
        <div class="row">
            <div class="col-12 col-md-5 offset-md-3 mb-5 mt-5">
                <div class="card rounded-xl mt-5">
                    <div class="card-body">
                        <div class="row">
                            <div class="col-12 mb-4">
                                <div class="border-bottom pb-1">
                                    <h5 class="bold"><strong>Add new card</strong></h5>
                                </div>
                            </div>
                            <div class="col-12">
                                <div class="form-floating mb-3">
                                    <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                                    <label for="floatingInput" class="pb-3"><small> Card number </small><i class='bx bxs-credit-card'></i></label>
                                </div>
                            </div>
                            <div class="col-12">
                                <div class="row">
                                    <div class="col-6">
                                        <div class="form-floating mb-3">
                                            <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                                            <label for="floatingInput" class="pb-3"><small> Expiry Date (mm/yy) </small><i class='bx bxs-calendar-alt'></i></label>
                                        </div>
                                    </div>
                                    <div class="col-6">
                                        <div class="form-floating mb-3">
                                            <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                                            <label for="floatingInput" class="pb-3"><small> CVC/CVV </small><i class='bx bxs-info-circle'></i></label>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="col-12">
                                <div class="form-floating mb-3">
                                    <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                                    <label for="floatingInput" class="pb-3"><small> Cardholder name </small><i class='bx bxs-user'></i></label>
                                </div>
                            </div>
                            <div class="col-12">
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault">
                                    <label class="form-check-label" for="flexCheckDefault">
                                        Save card
                                    </label>
                                </div>
                            </div>
                            <div class="col-12 mt-4">
                                <button class="form-control btn btn-primary pt-3 pb-3">Add card</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js" integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj" crossorigin="anonymous"></script>
</body>

</html>
```
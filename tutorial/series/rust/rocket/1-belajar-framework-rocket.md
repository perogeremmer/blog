## 1. Belajar Framework Rocket - Introduction

Gue lagi pengen ngulik framework rust, yaitu rocket. Dimana framework ini merupakan salah satu framework yang ajib buat rust.

Framework ini memungkinkan kita untuk bikin API yang jauh lebih cepat daripada ngoding native, ya karena kita pengen ngulik mah, ya gas-gas aja gak sih? 😆

## Install Projek

Pertama kita install projeknya terlebih dahulu, kita akan pake cargo. Btw, gue asumsiin ya kalo kalian udah paham cara menggunakan Rust atau bahkan belajar dasarnya, kalo kalian belom paham bisa coba baca ini:

<https://www.freecodecamp.org/news/rust-in-replit/>

Pertama, kita harus make sure bahwa kita pake rust yang versi stable, ketik ini di terminal:

```bash
rustup default stable
```

Kedua, pergi ke salah satu direktori kalian terus jalanin perintah berikut:

```bash
cargo new hello-rocket --bin
cd hello-rocket
```

Nantinya kamu akan otomatis masuk ke dalam folder projekmu, rust ini agak beda, kita gak se-ez ngeinstall laravel / code igniter pake composer. Kurang lebih mirip-mirip sama python yang kita harus bikin foldernya dulu terus bikin projeknya pake nginstall library/dependenciesnya.

Ohiya, kalo kamu nanya `--bin` itu artinya kita bikin projek yang jadi project binary, alias program yang executetable, soalnya kalo gak pake `--bin` atau malah pake `--lib`, jadinya kita tuh mau bikin library di rust, gitu aja sih simplenya.

## Install Library

Setelah masuk ke dalam projek, buka foldernya pake VSCode kalian terus cari file cargo.toml, edit bagian dependenciesnya jadi kaya gini:

```toml
[dependencies]
rocket = "=0.5.0-rc.3"
```

Kita akan pake versi terbaru dari projeknya si rocket.

## Ubah file `main.rs`

Sekarang kita ubah file main.rs di dalam folder src jadi kaya gini:

```rs
#[macro_use] extern crate rocket;

#[get("/")]
fn index() -> &'static str {
    "Hello, world!"
}

#[launch]
fn rocket() -> _ {
    rocket::build().mount("/", routes![index])
}
```

Bisa jalan gak sekarang? Bisa banget cuy!

Langsung eksekusi aja pake

```bash
cargo run
```

Nanti hasilnya kaya gini:

```bash
> cargo run
🔧 Configured for debug.
   >> address: 127.0.0.1
   >> port: 8000
   >> workers: [..]
   >> keep-alive: 5s
   >> limits: [..]
   >> tls: disabled
   >> temp dir: /tmp
   >> log level: normal
   >> cli colors: true
🛰  Routes:
   >> (index) GET /
🚀 Rocket has launched from http://127.0.0.1:8000
```

Kita bisa akses localhost:8000, dan voila, sudah berhasil deh~

## Tambahin Routes Baru

Kita mau coba nih tambahin routes baru, sekarang tambahin deh fungsi ini:

```rs
#[get("/hi")]
fn say_hi() -> &'static str {
    "Hi!"
}


#[launch]
fn rocket() -> _ {
    rocket::build()
    .mount("/", routes![index])
    .mount("/", routes![say_hi])
}
```

Keseluruhan filenya jadi kaya gini:

```rust
#[macro_use] extern crate rocket;

#[get("/")]
fn index() -> &'static str {
    "Hello, world!"
}

#[get("/hi")]
fn say_hi() -> &'static str {
    "Hi!"
}

#[launch]
fn rocket() -> _ {
    rocket::build()
    .mount("/", routes![index])
    .mount("/", routes![say_hi])
}
```

Sekarang stop pake CTRL + C terus jalanin ulang `cargo run`, akses ke localhost:8000/hi dan kamu akan ngeliat halaman baru 😃.

## Cara penamaan routing

Kalo kamu perhatiin pada bagian mount, keduanya sama-sama pake `/` untuk mounting, kenapa? Karena kita udah nge-define URL-nya di bagian atas, pada bagian get("/hi") dan get("/"), kalo kita gak define disana, kita perlu define di mount, coba ubah semuanya jadi kaya gini:


```rust
#[macro_use] extern crate rocket;

#[get("/")]
fn index() -> &'static str {
    "Hello, world!"
}

#[get("/")]
fn say_hi() -> &'static str {
    "Hi!"
}

#[launch]
fn rocket() -> _ {
    rocket::build()
    .mount("/", routes![index])
    .mount("/hi", routes![say_hi])
}
```

Cobain stop pake CTRL + C terus jalanin lagi, voila, kamu berhasil akses juga. Jadi intinya adalah kamu bisa kasih nama di bagian mount atau bahkan di fungsinya.

## Routes dengan parameter

Kita bisa dapetin parameter pake path di framework rocket, sekarang rombak lagi main.rs kamu jadi kaya begini:

```rust
#[macro_use] extern crate rocket;

#[get("/")]
fn index() -> &'static str {
    "Hello, world!"
}

#[get("/hi")]
fn say_hi() -> &'static str {
    "Hi!"
}

#[get("/say-name/<name>")]
fn say_name(name: &str) -> String {
    format!("Hello, {}!", name)
}

#[launch]
fn rocket() -> _ {
    rocket::build()
    .mount("/", routes![index])
    .mount("/", routes![say_hi])
    .mount("/", routes![say_name])
}
```

Stop, jalanin lagi, dan coba akses ke `localhost:8000/say-name/hudya`, kamu bakalan ngeliat pesan "Hello, Hudya!"

Gampang lah ya? Ini baru permulaan ges, nanti kita terusin sampai ke struktur foldernya~
<img src="../assets/" style="border-radius:10px;" />

<br/>

by [@perogeremmer](https://twitter.com/perogeremmer)

**Table of contents**

- [Kenalan sama OOP, penting gak penting sih](#kenalan-sama-oop-penting-gak-penting-sih)

## Introduction

Sebenernya keliatan basi sih belajar fundamental begini pake bahasa Rust, tapi menurut saya Rust ini agak beda. Soalnya dari segi bahasa dia bisa dibilang lebih rumit daripada bahasa lainnya seperti Python.

Bagi yang udah pernah belajar C atau C++ mungkin gak kesulitan sama Rust, tapi bagi yang belom pernah sama sekali? Maka dari itu saya pengen berbagi catatan sederhana biar kalian bisa lebih mudah mempelajari fundamental pake Rust.

Ohiya kalo misalnya ditanya gue belajarnya darimana, gue belajarnya [disini](https://doc.rust-lang.org/book/) guys tentunya dengan bantuan latihan soal dari [ChatGPT](https://chat.openapi.com).

## Compiler

Kalo lo mau jalanin rust di laptop lo bisa download langsung [disini](https://www.rust-lang.org/tools/install).

Tapi saran gue, lo mendingan pake online aja kaya [rust playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021) atau lo bisa juga pake [replit](https://replit.com).

Rust ini kaya C, C++, atau Java. Sebelum dijalanin harus di-compile terlebih dahulu, beda sama Python yang interpreter.

## Belajar Variabel

Gue gak perlu basa-basi lah ya jelasin apa itu variabel, gue anggap lo udah paham apa itu variabel, soalnya disini gue nulis untuk orang yang udah pernah terjun ke programming, bukan yang bener-bener buta.

Pada sarnya rust itu untuk ngebuat variabel cukup sesimple ini:

```rust
let x = 42;
```

Inget ya di rust itu pake titik koma, soalnya emang begitu grammarnya.

Nah sekarang lo perlu tau bahwa rust itu gak bisa sembarangan ditiban nilainya, lo harus pake syntax `mut`.

```rust
let mut x = 42;
x = 32;
```

## Static Variable

Di Rust juga ada static variable, ya udah pasti syntaxnya pake static. Bedanya kalo pake static kita harus masukin tipe datanya. Sebenernya sih kalo non-static kita juga bisa pake tipe data, tapi kalo static tuh wajib.

```rust
static PI : f64 = 3.14;
static MY_NAME : &str = "Hudya";
```

Nah rumus tipe data sebenernya sederhana yaitu `static nama-variabel : tipe data = nilai`.

> Bang itu kenapa &str bukan str?

Iyak nanti dijelasin pas bagian string ya.

## Nyetak Data

Setelah kita kenalan sama variabel, ya kita belajar nyetak data ges.

Nyetak data di rust pada umumnya sederhana, tinggal gini aja:

```rust
print!("Hello, World!")
```

<br/>

Nah, tapi beda guys sama kalo nyetak variabel, kita gak segampang Python yang tinggal print aja, kita perlu masukin placeholder agar bisa dicompile sebagai string.

```rust
let mut x = 42;
print!("Nilai x adalah {}", x);
```

<br/>

> Kenapa harus pake {} bang?

Ya emang begitu aturannya, kalo mau nyetak object variabel di print, ya pake `placeholder`.

> Bang emang kalo di rust ngeprint harus ada tanda seru (!)-nya ya?

Iya, emang begitu grammarnya, gak usah didebatin.

Ada cara lain juga ngeprint, yaitu `println!()`, udah kebayang hasilnya gimana? Ya, nyetak garis baru.

```rust
let mut x = 42;
println!("Nilai x adalah {}", x);
```

Bedanya `print` dan `println` adalah kalo `println` itu nyetak baris baru biar langsung kebawah, kalo kamu pake `print` dan nyetak dua kali, dia malah nyetak kesamping.

Ada satu lagi, namanya `format`.

Syntax ini dipake kalo kita mau nyimpen di sebuah nilai terlebih dahulu tanpa refer ke memory aslinya, gunanya biar data aslinya gak keganggu (kata ChatGPT sih begitu).

```rust
let mut x = 42;
let message = format!("Nilai x adalah {} ", x);
print!("{}", message);
```

> Dih ribet yak udah di format pake placeholder, di print pake lagi...

Ya emang, tapi secara memory ini aman, karena kita ngeprint objek si message, bukan object x.

Jadi kalo kita ngeprint x, kita refer ke nilai dari memory x, kalo kita pake format, kita bikin copy-annya yang jelas memorynya beda. Kalo ditanya lebih aman gak? Jelas lebih aman kalo kita bikin baru, karena gak akan berdampak pada memory aslinya, walau gue sendiri prefer gak pake format sih.

Menurut ChatGPT sih `format` dipake kalo kita ngebangun aplikasi GUI gitu kaya desktop.

<hr />

Udah segini dulu ya materinya nanti dilanjut lagi kalo gak mager hehehe.
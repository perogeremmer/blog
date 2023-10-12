**Table of contents**

- [Overview](#overview)
- [CSS: Short Introduction](#css-short-introduction)
- [Selector](#selector)
- [Property pada CSS](#property-pada-css)
  - [Borders](#borders)
  - [Padding](#padding)
  - [Margin](#margin)
  - [Height \& Width](#height--width)
  - [Text](#text)
  - [Fonts](#fonts)
  - [Icons](#icons)
- [Penggunaan !Important](#penggunaan-important)
- [Bermain dengan Table](#bermain-dengan-table)
- [Menghilangkan Elemen](#menghilangkan-elemen)
- [Posisi Objek](#posisi-objek)
- [Objek Melayang dengan Floating](#objek-melayang-dengan-floating)
- [Latihan](#latihan)

# Overview

Pada materi sebelumnya yaitu [2. HTML — Memulai Tag Dasar](https://www.notion.so/2-HTML-Memulai-Tag-Dasar-c817d0897fdf47378add6bacacdf170e?pvs=21) sempet saya singgung mengenai HTML bisa bergaya dan CSS merupakan atributnya.

Materi ini akan menjelaskan kode CSS yang dapat membuat HTML kamu menjadi SWAG~

# CSS: Short Introduction

✅ CSS is the language we use to style an HTML document.

CSS describes how HTML elements should be displayed.

CSS adalah bahasa yang digunakan untuk memberikan gaya (style) pada dokumen HTML. CSS dapat memberikan tampilan sehingga HTML kamu akan memiliki bentuk ataupun warna yang berbeda. Pada materi sebelumnya saya juga sudah menyampaikan syntax sederhana dari CSS yaitu:

```html
<tagname style="property:value;">
```

CSS akan dimasukkan sebagai property pada atribut style, dan tiap property akan memiliki sebuah nilai.

Contoh syntax CSS:

```css
h1 {
  color: blue;
  text-align: right;
}
```

- p → Selector dari tag paragraph pada HTML
- color → Properti warna teks
- text-align → Properti tata letak teks

Mari kita coba. Buatlah sebuah file bernama `index_with_css.html` dan masukkan kode berikut:

```html
<!DOCTYPE html>
<html>
<head>
<style>
h1 {
  color: blue;
  text-align: right;
}
</style>
</head>
<body>

<h1>Hello World!</h1>
<p>Headingnya dibuat dengan CSS.</p>

</body>
</html>
```

Sekarang buka dengan browser dan lihat hasilnya.

![](./assets/2023-08-24-17-57-03.png)

Sangat membagongkan bukan?

# Selector

Pada CSS, ada yang disebut dengan selector, yang artinya **pengenal**. CSS membutuhkan pengenal untuk memberikan style agar HTML kamu menjadi SWAG. Seperti apa saja bentuk selector? Tuliskan kode berikut:

```html
<!DOCTYPE html>
<html>

<head>
    <style>
        h1 {
            color: blue;
            text-align: right;
        }
        
        #my-id {
            color: red;
            text-align: center
        }
        
        .my-class {
            color: green;
            text-align: left;
        }
        
        .my-second-class {
            font-size: 2rem;
        }
    </style>
</head>

<body>

    <h1>Hello World!</h1>
    <p>Headingnya dibuat dengan CSS.</p>

    <p class="my-class my-second-class">Paragraf ini menggunakan selector class untuk CSS</p>
    <p id="my-id">Paragraf ini menggunakan selector ID untuk CSS</p>

</body>

</html>
```

Sekarang buka kembali halaman HTML dengan browser kamu.

![](./assets/2023-08-24-17-56-40.png)

- Pada atribut class, CSS dibuat dengan menggunakan simbol titik (.)
- Pada atribut id, CSS dibuat dengan menggunakan simbol hashtag (#)

Mana yang harus digunakan ID atau Class? Your call, tapi umumnya para web designer menggunakan class, karena class dapat menggunakan beberapa class secara bersamaan, sedangkan ID hanya bersifat single block saja.

# Property pada CSS

Ada banyak sekali property pada CSS, kamu tidak harus menghafalkan semuanya, namun yang lazim digunakan adalah sebagai berikut:

## Borders

Memberikan border pada komponen.

```css
.my-second-class {
    font-size: 2rem;
  border-style: dotted;
}
```

Border memiliki banyak nilai:

- dotted → Garis titik titik
- dashed → Garis panjang
- none → Menghilangkan border
- hidden → Menyembunyikan border

    Ada banyak yang lainnya lagi, namun ini umumnya yang sering dipakai.

## Padding

Memberikan jarak antara komponen dengan blocknya.

```css
.my-second-class {
    font-size: 2rem;
    padding: 25px;
}
```

Padding juga dapat diberikan tempat spesifik:

- padding-top
- padding-bottom
- padding-left
- padding-right

## Margin

Memberikan jarak antara block dengan block lainnya.

```css
.my-second-class {
    font-size: 2rem;
    margin: 25px;
}
```

Padding juga dapat diberikan tempat spesifik:

- margin-top
- margin-bottom
- margin-left
- margin-right

## Height & Width

Kamu dapat mengatur tinggi dan panjangnya sebuah block

```css
body {
 height: 200px;
}
```

Hal ini akan membuat kamu memiliki body dengan tinggi 200px saja.

<aside>
✅ Kamu dapat mengganti satuan px dengan rem, pt, dan satuan lainnya yang mendukung pixel.

</aside>

## Text

Untuk memberikan style pada text, kita dapat memberikan beberapa property:

**Color**

Memberikan warna pada teks

```css
p {
 color: red;
}
```

<aside>
✅ Kamu juga dapat mengganti kata red dengan kode warna misalnya #e74c3c

</aside>

**Background Color**

Memberikan warna pada teks

```css
p {
 background-color: red;
}
```

<aside>
✅ Kamu juga dapat mengganti kata red dengan kode warna misalnya #e74c3c

</aside>

**Text Alignment**

Memberikan posisi pada teks

```css
p {
 text-align: center;
}
```

<aside>
✅ Kamu dapat mengganti center dengan right, left, atau justify.

</aside>

## Fonts

Pada CSS, kita dapat mengganti font sesuai dengan keinginan kita. Terdapat lima font dasar pada CSS:

- Serif
- Sans-serif
- Monospace
- Cursive
- Fantasy

Contoh code:

```css
.paragraf {
  font-family: "Times New Roman", Times, serif;
}
```

<aside>
✅ Untuk Font yang lebih dari satu kata, maka harus menggunakan tanda kutip.

</aside>

**Font-size**

Kita juga dapat mengganti besar teks menggunakan property berikut:

```css
.teks {
 font-size: 40px;
}
```

**Cara Import Font dari Google Font**

```html
<!DOCTYPE html>
<html>

<head>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto">

    <style>
        body {
            font-family: "Roboto", serif;
        }
    </style>
</head>

<body>
    <h1>Hello World!</h1>
    <p>Pada halaman ini, kita menggunakan font Roboto loh!</p>
</body>

</html>
```

## Icons

Kamu dapat menambahkan icon agar HTML kamu menjadi lebih menarik, tulis kode berikut:

```html
<!DOCTYPE html>
<html>

<head>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css" integrity="sha512-1ycn6IcaQQ40/MKBW2W4Rhis/DbILU74C1vSrLJxCq57o941Ym01SwNsOMqvEBFlcgUa6xLiPY/NS5R+E6ztJQ==" crossorigin="anonymous" referrerpolicy="no-referrer" />
</head>

<body>

    <h1>Daftar Social Media</h1>
    <ul>
        <li><i class="fab fa-facebook"></i> Facebook</li>
        <li><i class="fab fa-instagram"></i> Instagram</li>
        <li><i class="fab fa-twitter"></i> Twitter</li>
    </ul>
</body>
</html>
```

Daftar icon dapat dilihat pada URL berikut:

[Font Awesome](https://fontawesome.com/v5.15/icons)

# Penggunaan !Important

Pada CSS kita dapat menggabungkan dua class yang berbeda. Apabila kita menggabungkan dua class yang berbeda, nilai property pada class pertama akan ditiban. Jika kamu ingin membuat nilai property class pertama lebih penting, kamu dapat menggunakan fungsi important. Cobalah kode berikut:

```html
<!DOCTYPE html>
<html>

<head>
    <style>
        h1 {
            color: blue;
            text-align: right;
        }
        
        #my-id {
            color: red;
            text-align: center
        }
        
        .my-class {
            color: green;
            text-align: left;
        }
        
        .my-second-class {
            font-size: 2rem;
            color: blue;
        }
    </style>
</head>

<body>

    <h1>Hello World!</h1>
    <p>Headingnya dibuat dengan CSS.</p>

    <p class="my-class my-second-class">Paragraf ini menggunakan selector class untuk CSS</p>
    <p id="my-id">Paragraf ini menggunakan selector ID untuk CSS</p>

</body>

</html>
```

<aside>
⚠️ Perhatikan my-second-class, class tersebut menimpa my-class yang memiliki warna hijau. Otomatis warna teks akan menjadi biru.

</aside>

Sekarang coba tambahkan `!important` di sebelah kanan kata green.

```css
.my-class {
    color: green !important;
    text-align: left;
}
```

Lihat kembali, sekarang kamu akan menemukan teks berwarna hijau kembali. Hal ini dikarenakan kita sudah memaksa dan memberitahu CSS bahwa value green dari property color pada class CSS my-class harus diutamakan.

# Bermain dengan Table

Pada materi [2. HTML — Memulai Tag Dasar](https://www.notion.so/2-HTML-Memulai-Tag-Dasar-c817d0897fdf47378add6bacacdf170e?pvs=21), disitu terdapat tag table yang apabila kita lihat, tidak terdapat border. Tentu saja border perlu ditambahkan dengan CSS, tuliskan kode berikut:

```html
<!DOCTYPE html>
<html>

<head>
    <title>Belajar border table - CSS</title>
    <style>
        table,
        th,
        td {
            border: 1px solid black;
        }
    </style>
</head>

<body>

    <h1>Daftar Pemenang Lomba 17 Agustusan</h1>
    <table>
        <tr>
            <th>Nama</th>
            <th>Kota</th>
        </tr>
        <tr>
            <td>Hudya</td>
            <td>Jakarta</td>
        </tr>
        <tr>
            <td>Susi Susanti</td>
            <td>Bandung</td>
        </tr>
    </table>
</body>

</html>
```

Hasilnya adalah sebagai berikut:

![](./assets/2023-08-24-17-55-55.png)

# Menghilangkan Elemen

Kita dapat menghilangkan elemen menggunakan atribut `display` pada css.

```html
<!DOCTYPE html>
<html>

<head>
    <title>Belajar border table - CSS</title>
    <style>
        .hilang {
            display: none;
        }
    </style>
</head>

<body>
    <h1>Ini Terlihat</h1>
    <h1 class="hilang">Ini Tidak Terlihat</h1>
</body>
</html>
```

<aside>
✅ Fungsi display none digunakan untuk menghilangkan sebuah bagian, terutama saat pergantian resolusi layar misalnya dari desktop ke mobile.

</aside>

# Posisi Objek

CSS dapat menentukan posisi sebuah tag (Objek) HTML. Posisi ini merupakan kunci tata letak konten di HTML saat kamu membangun sebuah website.

Terdapat beberapa fungsi posisi pada CSS:

<aside>
⚠️ Silahkan langsung copy paste seluruh kode dan jalankan pada browser kalian untuk melihat hasilnya

</aside>

- static → Posisi default sebuah objek pada CSS, yaitu statis mengikuti baris.

    ```html
    <!DOCTYPE html>
    <html>
    
    <head>
        <title>Belajar border table - CSS</title>
        <style>
            .fixed-position {
                position: static;
                width: auto;
                border: 3px solid #eb4d4b;
                background-color: white;
                top: 0;
                right: 0;
            }
        </style>
    </head>
    
    <body>
    
        <h1>Ini Terlihat</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <h1 class="fixed-position">Posisinya tetap</h1>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
    </body>
    </html>
    ```

- relative → Posisi objek menjadi relatif terhadap barisnya.

    ```html
    <!DOCTYPE html>
    <html>
    
    <head>
        <title>Belajar border table - CSS</title>
        <style>
            .fixed-position {
                position: relative;
                width: auto;
                border: 3px solid #eb4d4b;
                background-color: white;
                top: 0;
                right: 0;
                left: 40px;
            }
        </style>
    </head>
    
    <body>
    
        <h1>Ini Terlihat</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <h1 class="fixed-position">Posisinya tetap</h1>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
    </body>
    
    </html>
    ```

- fixed → Posisi objek akan tetap berada pada posisi yang ditentukan.

    ```html
    <!DOCTYPE html>
    <html>
    
    <head>
        <title>Belajar border table - CSS</title>
        <style>
            .fixed-position {
                position: fixed;
                width: auto;
                border: 3px solid #eb4d4b;
                background-color: white;
                top: 0;
                right: 0;
                margin: 40px;
            }
        </style>
    </head>
    
    <body>
    
        <h1>Ini Terlihat</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <h1 class="fixed-position">Posisinya tetap</h1>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
    </body>
    
    </html>
    ```

- absolute → Posisi objek menjadi absolut, menimpa objek lainnya yang bukan absolute.

    ```html
    <!DOCTYPE html>
    <html>
    
    <head>
        <title>Belajar border table - CSS</title>
        <style>
            .fixed-position {
                position: absolute;
                width: auto;
                border: 3px solid #eb4d4b;
                background-color: white;
                top: 0;
                right: 0;
                margin: 40px;
            }
        </style>
    </head>
    
    <body>
    
        <h1>Ini Terlihat</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <h1 class="fixed-position">Posisinya Absolut sekali</h1>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
    </body>
    
    </html>
    ```

- sticky → Posisi objek berdasarkan scroll.

    <aside>
    ⚠️ Harap scroll dan perhatikan objeknya menempel pada bagian atas!

    </aside>

    ```html
    <!DOCTYPE html>
    <html>
    
    <head>
        <title>Belajar border table - CSS</title>
        <style>
            .fixed-position {
                position: sticky;
                width: auto;
                border: 3px solid #eb4d4b;
                background-color: white;
                top: 0;
                right: 0;
                margin: 40px;
            }
        </style>
    </head>
    
    <body>
    
        <h1>Ini Terlihat</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <h1 class="fixed-position">Posisinya sticky</h1>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec gravida accumsan dapibus. Quisque et augue sed arcu dignissim finibus. Vestibulum velit ante, efficitur eu vestibulum quis, pulvinar ac nisl. Suspendisse potenti. Fusce pharetra accumsan
            viverra. Integer lobortis pulvinar velit, eget fermentum metus rhoncus sit amet. Duis semper augue at mi accumsan, vestibulum hendrerit ipsum egestas. Vestibulum malesuada, ipsum eu auctor egestas, quam mauris auctor metus, sit amet ultrices quam
            leo sed ligula. Suspendisse tortor nulla, scelerisque non sagittis sed, dignissim et justo. Integer auctor ipsum vel risus euismod iaculis. Praesent luctus est ut massa cursus sodales. Nam mauris velit, aliquet et leo ut, blandit eleifend nisl.
            Nunc vulputate justo et velit dapibus, et mattis felis hendrerit. Phasellus at efficitur libero, in fermentum libero. Phasellus dapibus mi est. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec sit amet
            lectus ligula. Vestibulum gravida lacinia dolor, vitae commodo augue varius eget. Sed rutrum fringilla dolor. Cras auctor mauris non purus congue, vel accumsan dui volutpat. Sed ligula eros, lobortis commodo odio sit amet, aliquet dignissim est.
            Fusce non enim velit. In hac habitasse platea dictumst. Nulla fringilla rhoncus ligula a feugiat. In ut tellus vitae sem bibendum vestibulum. Donec interdum, libero in mollis pulvinar, mauris turpis ullamcorper lorem, nec dictum velit leo et diam.
            Duis quis tempor justo. Aenean nec velit ut purus blandit vulputate sed eu lectus. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Maecenas nunc enim, auctor vel ornare non, pharetra eleifend elit.
            Mauris fermentum blandit ullamcorper. Vivamus vestibulum, arcu id tempus interdum, dolor diam hendrerit mauris, vitae placerat lectus dolor sit amet urna. Vestibulum dignissim neque leo, at luctus magna facilisis malesuada. Vivamus nec scelerisque
            metus. Proin vestibulum dictum ligula eget tempor. Praesent sed lorem vel lectus malesuada ullamcorper efficitur eget orci. Etiam pharetra accumsan mauris. Aliquam erat volutpat. Aliquam quis tortor in nisi vehicula vehicula. Pellentesque lobortis,
            est vel mollis aliquet, diam sem ultrices libero, at sollicitudin tortor sapien non ex. Aenean erat justo, imperdiet sed quam sit amet, laoreet porta neque. Quisque mollis facilisis nisi ut vulputate. Integer at enim est. Nulla facilisi. Integer
            ac dui eget sapien fringilla vestibulum in ac nunc. Cras eu diam euismod, posuere augue vel, commodo nibh. Praesent sollicitudin velit non ante aliquet condimentum. Sed accumsan metus quis dolor finibus venenatis. Nunc tincidunt mi a est ultrices
            faucibus. In in lacinia leo. Vestibulum nec metus neque. Vestibulum faucibus fringilla elit. Suspendisse odio quam, eleifend vel ipsum at, aliquet pretium odio. In rhoncus ipsum et nulla bibendum, eget consequat nisi posuere. Cras sodales accumsan
            dui, nec maximus nulla hendrerit non. Suspendisse eros augue, tristique a vestibulum vel, imperdiet id enim. Suspendisse vehicula vehicula odio, eu convallis orci elementum id.</p>
    
    </body>
    
    </html>
    ```

# Objek Melayang dengan Floating

Mendengar kata Float, tentu saja ini hal yang paling basic pada CSS. Terkadang kita mendapatkan momen disaat kita menggabungkan tag gambar dengan paragraf, pada bagian ini kita memerlukan sebuah style dimana objek lainnya harus dapat melayang mengikuti keadaan block (dinamis), jadi seolah seperti paragraf dengan gambar. Dengan menggunakan property float, kamu dapat menyelesaikan masalah tersebut.

Tuliskan kode berikut:

```html
<!DOCTYPE html>
<html>

<head>
    <style>
        img {
            float: left;
        }
    </style>
</head>

<body>

    <h2>Float Left</h2>

    <p>In this example, the image will float to the right in the paragraph, and the text in the paragraph will wrap around the image.</p>

    <p><img src="https://www.w3schools.com/css/pineapple.jpg" alt="Pineapple" style="margin-right:15px;"> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim
        ligula venenatis dolor. Maecenas nisl est, ultrices nec congue eget, auctor vitae massa. Fusce luctus vestibulum augue ut aliquet. Mauris ante ligula, facilisis sed ornare eu, lobortis in odio. Praesent convallis urna a lacus interdum ut hendrerit
        risus congue. Nunc sagittis dictum nisi, sed ullamcorper ipsum dignissim ac. In at libero sed nunc venenatis imperdiet sed ornare turpis. Donec vitae dui eget tellus gravida venenatis. Integer fringilla congue eros non fermentum. Sed dapibus pulvinar
        nibh tempor porta. Cras ac leo purus. Mauris quis diam velit.</p>
</body>
</html>
```

Nilai property float:

- left → Objek melayang di sebelah kiri.
- right → Objek melayang di sebelah kanan.
- inherit → Objek mengikuti sifat float dari parent tag-nya.
- none → Objek tidak bersifat float.

Hasilnya sebagai berikut

![](./assets/2023-08-24-17-57-37.png)

Menggunakan float

# Latihan

Saatnya latihan yuk, dapatkah kamu membuat website sederhana seperti ini?

![](./assets/2023-08-24-17-58-03.png)

<aside>
⚠️ Untuk menggunakan gambar secara local, copy gambar yang kamu inginkan pada lokasi yang sama dengan HTML kamu.
</aside>

Menyerah atau ingin mengintip codenya? Lihat [disini](./answer/challenge-task-3.html).
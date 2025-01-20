# 1 - Introduction

## MongoDB

MongoDB adalah database dokumen NoSQL yang open-source. Dirancang untuk menyimpan data dalam format fleksibel, mirip dengan JSON, yang disebut BSON (Binary JSON). Keunikan MongoDB terletak pada kemampuannya untuk menangani data dengan struktur yang beragam dan kompleks.

MongoDB dikembangkan oleh MongoDB Inc. (sebelumnya dikenal sebagai 10gen) pada tahun 2007. Versi pertama dari database ini dirilis ke publik pada tahun 2009. Nama "Mongo" berasal dari kata "humongous", menunjukkan kemampuannya untuk menangani data dalam jumlah yang sangat besar.

## Features

MongoDB memiliki beberapa fitur utama yang membuatnya menonjol di antara database lainnya:

1. **Skalabilitas horizontal**: MongoDB dapat dengan mudah didistribusikan di beberapa server, memungkinkan pertumbuhan database seiring dengan peningkatan kebutuhan.

2. **Fleksibilitas**: Skema yang dinamis memungkinkan struktur dokumen yang bervariasi dalam satu koleksi, memberikan fleksibilitas yang tinggi dalam pengelolaan data.

3. **Performa tinggi**: MongoDB mendukung indexing, sharding, dan replikasi, yang berkontribusi pada kinerja dan ketersediaan data yang tinggi.

4. **Dukungan untuk berbagai bahasa pemrograman**: Tersedia driver untuk banyak bahasa pemrograman populer, memudahkan integrasi dengan berbagai platform pengembangan.

## Konsep Dasar MongoDB

Untuk memahami MongoDB, penting untuk mengenal beberapa konsep dasarnya:

1. **Database**: Kontainer fisik untuk koleksi. Satu instance MongoDB dapat memiliki beberapa database.

2. **Collection**: Grup dokumen MongoDB, setara dengan tabel dalam RDBMS. Koleksi tidak memaksakan struktur yang seragam pada dokumen-dokumennya.

3. **Dokumen**: Satu record dalam MongoDB, disimpan dalam format BSON. Dokumen adalah unit dasar data dalam MongoDB dan dapat memiliki struktur yang berbeda-beda dalam satu koleksi.

4. **Field**: Pasangan key-value dalam dokumen, setara dengan kolom dalam RDBMS. Field dapat berisi berbagai tipe data, termasuk array dan dokumen bersarang.

Pemahaman tentang konsep-konsep ini penting untuk mengoptimalkan penggunaan MongoDB dalam pengembangan aplikasi dan pengelolaan data.

# MongoDB vs RDBMS

## Model Data dan Skema

RDBMS menggunakan model data tabular dengan skema yang tetap, sedangkan MongoDB mengadopsi model data dokumen dengan skema yang fleksibel. Dalam RDBMS, struktur tabel bersifat kaku, dan perubahan memerlukan migrasi. Sebaliknya, MongoDB memungkinkan dokumen dalam koleksi yang sama memiliki struktur yang berbeda, memberikan fleksibilitas yang lebih besar.

## Relasi dan Transaksi

RDBMS mengandalkan foreign key untuk menghubungkan tabel, sementara MongoDB menggunakan referensi atau embedding dokumen untuk menyimpan data terkait. Dalam hal transaksi, RDBMS mendukung transaksi ACID sepenuhnya, sedangkan MongoDB baru mendukung transaksi ACID multi-dokumen sejak versi 4.0.

## Skalabilitas dan Performa

RDBMS umumnya di-scale secara vertikal dengan meningkatkan kapasitas server, sementara MongoDB dirancang untuk scale secara horizontal dengan menambah lebih banyak server. Dalam hal performa, RDBMS optimal untuk operasi kompleks yang melibatkan banyak tabel, sedangkan MongoDB sangat cepat untuk operasi read/write pada data dokumen.

## Query Language dan Use Cases

RDBMS menggunakan SQL (Structured Query Language), sementara MongoDB menggunakan query language berbasis JSON. RDBMS ideal untuk aplikasi yang memerlukan transaksi kompleks dan integritas data yang ketat, sedangkan MongoDB cocok untuk aplikasi yang membutuhkan skalabilitas tinggi dan fleksibilitas data.

Pemilihan antara RDBMS dan MongoDB tergantung pada kebutuhan spesifik aplikasi. RDBMS tetap menjadi pilihan utama untuk sistem yang memerlukan konsistensi data yang kuat dan transaksi kompleks, seperti sistem perbankan atau e-commerce. Di sisi lain, MongoDB unggul dalam skenario yang membutuhkan penanganan data besar dengan struktur yang berubah-ubah, seperti aplikasi sosial media atau analitik real-time.
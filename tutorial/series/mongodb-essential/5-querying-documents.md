# 5 - Query di MongoDB

- [5 - Query di MongoDB](#5---query-di-mongodb)
  - [Overview](#overview)
  - [Read](#read)
    - [Tabel Operator Logical](#tabel-operator-logical)
    - [Pencarian dengan Logical Operator](#pencarian-dengan-logical-operator)
    - [Pencarian dengan kolom tertentu](#pencarian-dengan-kolom-tertentu)
    - [Tabel Operator Aritmatika](#tabel-operator-aritmatika)
  - [Menampilkan dengan Batasan dan Urutan](#menampilkan-dengan-batasan-dan-urutan)
  - [Insert](#insert)
    - [Bulk Write](#bulk-write)
  - [Update](#update)
  - [Delete](#delete)

## Overview

Pada materi ini, kamu akan belajar bagaimana melakukan query atau menulis query dasar di MongoDB.

Untuk memulainya, akan dibuatkan satu collection dengan memasukkan data sebanyak 20 data. Gunakan database yang ingin kalian gunakan lalu copy kode di bawah ini:

```bash
db.inventories.insertMany([
  // Kategori: Elektronik
  {
    "name": "Laptop Asus ROG",
    "category": "Elektronik",
    "stock": 15,
    "price": 15000000,
    "company": "PT Asus Indonesia",
    "created_at": "2023-01-15T08:00:00Z",
    "updated_at": "2023-06-20T10:30:00Z",
    "deleted_at": null
  },
  {
    "name": "Samsung QLED TV 55 inch",
    "category": "Elektronik",
    "stock": 10,
    "price": 12500000,
    "company": "PT Samsung Electronics Indonesia",
    "created_at": "2023-03-10T11:30:00Z",
    "updated_at": "2023-06-15T16:20:00Z",
    "deleted_at": null
  },
  {
    "name": "Sony WH-1000XM4",
    "category": "Elektronik",
    "stock": 30,
    "price": 3799000,
    "company": "PT Sony Indonesia",
    "created_at": "2023-02-14T10:00:00Z",
    "updated_at": "2023-06-19T11:30:00Z",
    "deleted_at": null
  },
  {
    "name": "LG UltraFine 5K Display",
    "category": "Elektronik",
    "stock": 12,
    "price": 9999000,
    "company": "PT LG Electronics Indonesia",
    "created_at": "2023-03-15T11:45:00Z",
    "updated_at": "2023-06-20T14:30:00Z",
    "deleted_at": null
  },
  {
    "name": "Bose QuietComfort Earbuds",
    "category": "Elektronik",
    "stock": 22,
    "price": 3999000,
    "company": "PT Bose Indonesia",
    "created_at": "2023-01-05T09:45:00Z",
    "updated_at": "2023-06-21T13:50:00Z",
    "deleted_at": null
  },

  // Kategori: Smartphone
  {
    "name": "iPhone 13 Pro",
    "category": "Smartphone",
    "stock": 25,
    "price": 17999000,
    "company": "Apple Inc.",
    "created_at": "2023-02-01T09:15:00Z",
    "updated_at": "2023-06-18T14:45:00Z",
    "deleted_at": null
  },
  {
    "name": "Samsung Galaxy S21",
    "category": "Smartphone",
    "stock": 20,
    "price": 12999000,
    "company": "PT Samsung Electronics Indonesia",
    "created_at": "2023-02-05T10:00:00Z",
    "updated_at": "2023-06-19T11:30:00Z",
    "deleted_at": null
  },
  {
    "name": "Xiaomi Mi 11",
    "category": "Smartphone",
    "stock": 30,
    "price": 9999000,
    "company": "PT Xiaomi Communications Indonesia",
    "created_at": "2023-02-10T14:30:00Z",
    "updated_at": "2023-06-20T16:45:00Z",
    "deleted_at": null
  },
  {
    "name": "Google Pixel 6",
    "category": "Smartphone",
    "stock": 15,
    "price": 10999000,
    "company": "Google LLC",
    "created_at": "2023-02-15T09:45:00Z",
    "updated_at": "2023-06-21T13:20:00Z",
    "deleted_at": null
  },
  {
    "name": "OnePlus 9 Pro",
    "category": "Smartphone",
    "stock": 18,
    "price": 11999000,
    "company": "OnePlus Technology",
    "created_at": "2023-02-20T11:15:00Z",
    "updated_at": "2023-06-22T15:10:00Z",
    "deleted_at": null
  },

  // Kategori: Kamera
  {
    "name": "Canon EOS R6",
    "category": "Kamera",
    "stock": 8,
    "price": 39999000,
    "company": "PT Datascrip",
    "created_at": "2023-03-05T14:20:00Z",
    "updated_at": "2023-06-21T15:40:00Z",
    "deleted_at": null
  },
  {
    "name": "Sony Alpha A7 III",
    "category": "Kamera",
    "stock": 10,
    "price": 29999000,
    "company": "PT Sony Indonesia",
    "created_at": "2023-03-10T10:30:00Z",
    "updated_at": "2023-06-22T14:15:00Z",
    "deleted_at": null
  },
  {
    "name": "Fujifilm X-T4",
    "category": "Kamera",
    "stock": 12,
    "price": 27999000,
    "company": "PT Fujifilm Indonesia",
    "created_at": "2023-03-15T09:45:00Z",
    "updated_at": "2023-06-23T11:30:00Z",
    "deleted_at": null
  },
  {
    "name": "Nikon Z6 II",
    "category": "Kamera",
    "stock": 7,
    "price": 31999000,
    "company": "PT Nikon Indonesia",
    "created_at": "2023-03-20T13:00:00Z",
    "updated_at": "2023-06-24T16:20:00Z",
    "deleted_at": null
  },
  {
    "name": "Panasonic Lumix GH5",
    "category": "Kamera",
    "stock": 4,
    "price": 24999000,
    "company": "PT Panasonic Gobel Indonesia",
    "created_at": "2023-03-12T13:30:00Z",
    "updated_at": "2023-06-22T14:10:00Z",
    "deleted_at": null
  },

  // Kategori: Aksesoris Komputer
  {
    "name": "Logitech MX Master 3",
    "category": "Aksesoris Komputer",
    "stock": 50,
    "price": 1499000,
    "company": "PT Logitech Indonesia",
    "created_at": "2023-01-20T13:45:00Z",
    "updated_at": "2023-06-22T09:10:00Z",
    "deleted_at": null
  },
  {
    "name": "Razer BlackWidow V3",
    "category": "Aksesoris Komputer",
    "stock": 35,
    "price": 1899000,
    "company": "PT Razer Indonesia",
    "created_at": "2023-02-20T10:30:00Z",
    "updated_at": "2023-06-22T11:20:00Z",
    "deleted_at": null
  },
  {
    "name": "SteelSeries Arctis Pro",
    "category": "Aksesoris Komputer",
    "stock": 20,
    "price": 2799000,
    "company": "PT Steel Series Indonesia",
    "created_at": "2023-02-25T15:40:00Z",
    "updated_at": "2023-06-21T10:05:00Z",
    "deleted_at": null
  },
  {
    "name": "Corsair K95 RGB Platinum",
    "category": "Aksesoris Komputer",
    "stock": 25,
    "price": 2599000,
    "company": "PT Corsair Indonesia",
    "created_at": "2023-03-01T11:20:00Z",
    "updated_at": "2023-06-23T14:30:00Z",
    "deleted_at": null
  },
  {
    "name": "ASUS ROG Swift PG279Q",
    "category": "Aksesoris Komputer",
    "stock": 15,
    "price": 11999000,
    "company": "PT ASUS Indonesia",
    "created_at": "2023-03-05T09:15:00Z",
    "updated_at": "2023-06-24T12:40:00Z",
    "deleted_at": null
  }
]);
```

> [!NOTE] > `created_at` dan `updated_at` adalah kolom yang menunjukkan kapan data tersebut dibuat dan diupdate, biasanya ini menjadi standar di beberapa framework seperti Laravel.

Kamu akan melihat hasilnya seperti ini:

```bash
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("678cb3c89a05e75c5db1b0cc"),
    '1': ObjectId("678cb3c89a05e75c5db1b0cd"),
    '2': ObjectId("678cb3c89a05e75c5db1b0ce"),
    '3': ObjectId("678cb3c89a05e75c5db1b0cf"),
    '4': ObjectId("678cb3c89a05e75c5db1b0d0"),
    '5': ObjectId("678cb3c89a05e75c5db1b0d1"),
    '6': ObjectId("678cb3c89a05e75c5db1b0d2"),
    '7': ObjectId("678cb3c89a05e75c5db1b0d3"),
    '8': ObjectId("678cb3c89a05e75c5db1b0d4"),
    '9': ObjectId("678cb3c89a05e75c5db1b0d5"),
    '10': ObjectId("678cb3c89a05e75c5db1b0d6"),
    '11': ObjectId("678cb3c89a05e75c5db1b0d7"),
    '12': ObjectId("678cb3c89a05e75c5db1b0d8"),
    '13': ObjectId("678cb3c89a05e75c5db1b0d9"),
    '14': ObjectId("678cb3c89a05e75c5db1b0da"),
    '15': ObjectId("678cb3c89a05e75c5db1b0db"),
    '16': ObjectId("678cb3c89a05e75c5db1b0dc"),
    '17': ObjectId("678cb3c89a05e75c5db1b0dd"),
    '18': ObjectId("678cb3c89a05e75c5db1b0de"),
    '19': ObjectId("678cb3c89a05e75c5db1b0df")
  }
}
```

## Read

Perintah dasar untuk menampilkan data adalah fungsi (method) `.find()`, seperti query yang sudah kita lakukan sebelumnya.

```bash
db.inventories.find(query)
```

Dengan menjalankan query di atas kamu akan melihat semua datanya tampil, bagaimana apabila kita ingin mencari data dengan beberapa syarat? Misalnya yang stoknya lebih besar dari 3, maka kita akan menggunakan query object di dalam method find.

Coba query berikut:

```bash
db.inventories.find({stock: {$gt: 10}})
```

Hasilnya adalah semua barang dengan stok lebih dari 10 akan ditampilkan.

Sehingga rumus dasar penggunaan query pada pencarian adalah:

```text
db.nama_collection.find({query})
```

Apabila kita ingin menampilkan datanya satu saja, maka kita akan gunakan fungsi `.findOne()`.

Jalankan kembali query di bawah ini:

```bash
db.inventories.findOne({stock: {$gt: 10}})
```

Hasil

```bash
Atlas atlas-969x7s-shard-0 [primary] coba> db.inventories.findOne({stock: {$gt: 10}})
{
  _id: ObjectId("678cb3c89a05e75c5db1b0cc"),
  name: 'Laptop Asus ROG',
  category: 'Elektronik',
  stock: 15,
  price: 15000000,
  company: 'PT Asus Indonesia',
  created_at: '2023-01-15T08:00:00Z',
  updated_at: '2023-06-20T10:30:00Z',
  deleted_at: null
}
```

Perbedaannya sangat spesifik dimana menggunakan `find` akan mengembalikan array, sedangkan dengan `findOne` akan mengembalikan object.

### Tabel Operator Logical

| Operator  | Deskripsi                                                 | Contoh Penggunaan                                 |
| --------- | --------------------------------------------------------- | ------------------------------------------------- |
| `$eq`     | Sama dengan (equal)                                       | `{ field: { $eq: value } }`                       |
| `$ne`     | Tidak sama dengan (not equal)                             | `{ field: { $ne: value } }`                       |
| `$gt`     | Lebih besar dari (greater than)                           | `{ field: { $gt: value } }`                       |
| `$gte`    | Lebih besar dari atau sama dengan (greater than or equal) | `{ field: { $gte: value } }`                      |
| `$lt`     | Kurang dari (less than)                                   | `{ field: { $lt: value } }`                       |
| `$lte`    | Kurang dari atau sama dengan (less than or equal)         | `{ field: { $lte: value } }`                      |
| `$in`     | Cocok dengan salah satu nilai dalam array                 | `{ field: { $in: [value1, value2, ...] } }`       |
| `$nin`    | Tidak cocok dengan nilai apapun dalam array               | `{ field: { $nin: [value1, value2, ...] } }`      |
| `$exists` | Memeriksa keberadaan field                                | `{ field: { $exists: true/false } }`              |
| `$type`   | Memeriksa tipe data field                                 | `{ field: { $type: "string" } }`                  |
| `$regex`  | Mencocokkan dengan pola regex                             | `{ field: { $regex: /pattern/, $options: 'i' } }` |
| `$and`    | Menggabungkan kondisi dengan AND logika                   | `{ $and: [ {condition1}, {condition2} ] }`        |
| `$or`     | Menggabungkan kondisi dengan OR logika                    | `{ $or: [ {condition1}, {condition2} ] }`         |
| `$not`    | Membalikkan hasil dari ekspresi query                     | `{ field: { $not: { $gt: value } } }`             |
| `$size`   | Mencocokkan array dengan panjang tertentu                 | `{ field: { $size: number } }`                    |

### Pencarian dengan Logical Operator

Secara eksplisit apabila kamu ingin mencari menggunakan logical operator kamu tidak perlu menggunakan `$and`, karena ketika kamu menggabungkan dua buah kondisi seperti di bawah ini, MongoDB otomatis menggunakan `AND` operator.

```javascript
db.inventories.find({
  stock: { $gt: 10 },
  company: { $regex: /xiaomi/i },
});
```

Namun apabila menggunakan operator `OR` kamu wajib untuk menggunakan operatornya.

```javascript
db.inventories.find({
  $or: [
    { stock: { $gt: 10 } },
    { company: { $regex: /xiaomi/i } },
    { price: { $lt: 5000000 } },
  ],
});
```

Penggabungan keduanya juga memungkinkan:

```javascript
db.inventories.find({
  $and: [
    { category: "Elektronik" },
    { $or: [{ stock: { $gt: 10 } }, { company: { $regex: /xiaomi/i } }] },
  ],
});
```

### Pencarian dengan kolom tertentu

Mencari dengan kolom tertentu memungkinkan di MongoDB, misalnya kita akan menampilkan nama barang, harga, harga yang di-diskon dengan mengalikannya dengan 0.9 (diskon 10%) kemudian kita tutup id-nya.

```javascript
db.inventories.find(
  {},
  {
    name: 1,
    price: 1,
    discounted_price: { $multiply: ["$price", 0.9] },
    _id: 0,
  }
);
```

> [!NOTE]
> Kolom pertama merupakan query, jadi cukup masukkan objek kosong saja kemudian diikuti dengan kolom yang ingin ditampilkan. Angka 1 untuk `true` dan 0 untuk `false`.

Hasil

```javascript
[
  {
    name: "Laptop Asus ROG",
    price: 15000000,
    discounted_price: 13500000,
  },
  {
    name: "iPhone 13 Pro",
    price: 17999000,
    discounted_price: 16199100,
  },
  {
    name: "Samsung QLED TV 55 inch",
    price: 12500000,
    discounted_price: 11250000,
  },
  {
    name: "Logitech MX Master 3",
    price: 1499000,
    discounted_price: 1349100,
  },
  {
    name: "Sony WH-1000XM4",
    price: 3799000,
    discounted_price: 3419100,
  },
  { name: "Canon EOS R6", price: 39999000, discounted_price: 35999100 },
  {
    name: "Philips Air Fryer",
    price: 1999000,
    discounted_price: 1799100,
  },
  {
    name: "Nvidia GeForce RTX 3080",
    price: 12000000,
    discounted_price: 10800000,
  },
  {
    name: "LG UltraFine 5K Display",
    price: 9999000,
    discounted_price: 8999100,
  },
  {
    name: "DJI Mavic Air 2",
    price: 14999000,
    discounted_price: 13499100,
  },
  {
    name: "Razer BlackWidow V3",
    price: 1899000,
    discounted_price: 1709100,
  },
  {
    name: "GoPro HERO10 Black",
    price: 7499000,
    discounted_price: 6749100,
  },
  {
    name: "Bose QuietComfort Earbuds",
    price: 3999000,
    discounted_price: 3599100,
  },
  {
    name: "Dyson V11 Absolute",
    price: 10999000,
    discounted_price: 9899100,
  },
  {
    name: "Wacom Cintiq 16",
    price: 11999000,
    discounted_price: 10799100,
  },
  {
    name: "Epson EcoTank L3210",
    price: 2499000,
    discounted_price: 2249100,
  },
  { name: "Fitbit Versa 3", price: 2999000, discounted_price: 2699100 },
  {
    name: "Panasonic Lumix GH5",
    price: 24999000,
    discounted_price: 22499100,
  },
  {
    name: "Xiaomi Mi Robot Vacuum",
    price: 3499000,
    discounted_price: 3149100,
  },
  {
    name: "SteelSeries Arctis Pro",
    price: 2799000,
    discounted_price: 2519100,
  },
];
```

> [!WARNING]
> Pencarian dengan menggabungkan operasi lanjutan di dalamnya dengan operator matmethamical seperti contoh di atas akan berpengaruh buruk pada query pencarian khususnya dengan data yang banyak. Jadi tidak disarankan untuk menggunakannya.

### Tabel Operator Aritmatika

| Operator    | Deskripsi                                  | Contoh Penggunaan                        |
| ----------- | ------------------------------------------ | ---------------------------------------- |
| `$add`      | Menjumlahkan angka atau tanggal            | `{ $add: [<expr1>, <expr2>, ...] }`      |
| `$subtract` | Mengurangkan dua angka atau tanggal        | `{ $subtract: [<expr1>, <expr2>] }`      |
| `$multiply` | Mengalikan angka                           | `{ $multiply: [<expr1>, <expr2>, ...] }` |
| `$divide`   | Membagi dua angka                          | `{ $divide: [<expr1>, <expr2>] }`        |
| `$mod`      | Menghitung sisa pembagian                  | `{ $mod: [<expr1>, <expr2>] }`           |
| `$abs`      | Menghitung nilai absolut                   | `{ $abs: <number> }`                     |
| `$ceil`     | Membulatkan ke atas                        | `{ $ceil: <number> }`                    |
| `$floor`    | Membulatkan ke bawah                       | `{ $floor: <number> }`                   |
| `$round`    | Membulatkan ke bilangan bulat terdekat     | `{ $round: [<number>, <place>] }`        |
| `$exp`      | Menghitung e pangkat x                     | `{ $exp: <exponent> }`                   |
| `$ln`       | Menghitung logaritma natural               | `{ $ln: <number> }`                      |
| `$log`      | Menghitung logaritma dengan basis tertentu | `{ $log: [<number>, <base>] }`           |
| `$pow`      | Menghitung pangkat                         | `{ $pow: [<base>, <exponent>] }`         |
| `$sqrt`     | Menghitung akar kuadrat                    | `{ $sqrt: <number> }`                    |
| `$trunc`    | Memotong angka ke bilangan bulat           | `{ $trunc: [<number>, <place>] }`        |
| `$avg`      | Menghitung rata-rata (dalam `$group`)      | `{ $avg: <expression> }`                 |
| `$max`      | Menemukan nilai maksimum (dalam `$group`)  | `{ $max: <expression> }`                 |
| `$min`      | Menemukan nilai minimum (dalam `$group`)   | `{ $min: <expression> }`                 |
| `$sum`      | Menjumlahkan nilai (dalam `$group`)        | `{ $sum: <expression> }`                 |

## Menampilkan dengan Batasan dan Urutan

Untuk menampilkan dengan batasan dan urutan, kita akan menggunakan dua fungsi yaitu `sort()` dan `limit()`.

Contoh:

```javascript
db.inventories.find({ category: "Smartphone" }).sort({ price: 1 }).limit(3);
```

Kita akan menampilkan produk dengan category smartphone diurutkan dengan price ascending (terkecil) dan kita batasi limit 3 saja.

Bisa juga kita misalnya ingin menampilkan dari yang descending (terbesar)

```javascript
db.inventories.find({ category: "Smartphone" }).sort({ price: -1 }).limit(3);
```

Kamu juga bisa menggunakan sort tanpa limit dan sebaliknya, jadi gunakan sesuai kebutuhan.

> Kalau kebalik limit duluan baru sort?

Bisa kok, coba saja query di bawah ini.

```bash
db.inventories.find({ category: "Smartphone" }).limit(3).sort({ price: -1 })
```

Tidak akan mempengaruhi hasil atau sintaks error.

Kamu juga dapat menggunakan offset dengan fungsi `skip`. Misalnya kita ingin menampilkan data sebanyak 10 setiap halamannya, maka rumusnya akan seperti ini:

```javascript
db.inventories.find().sort({ name: 1 }).skip(offset).limit(batasData);
```

Contoh:

```bash
db.inventories.find().sort({ name: 1 }).skip(0).limit(10)
```

Hasil:

```bash
[
  {
    _id: ObjectId("678ce0499a05e75c5db1b108"),
    name: 'ASUS ROG Swift PG279Q',
    category: 'Aksesoris Komputer',
    stock: 15,
    price: 11999000,
    company: 'PT ASUS Indonesia',
    created_at: '2023-03-05T09:15:00Z',
    updated_at: '2023-06-24T12:40:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b0f9"),
    name: 'Bose QuietComfort Earbuds',
    category: 'Elektronik',
    stock: 22,
    price: 3999000,
    company: 'PT Bose Indonesia',
    created_at: '2023-01-05T09:45:00Z',
    updated_at: '2023-06-21T13:50:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b0ff"),
    name: 'Canon EOS R6',
    category: 'Kamera',
    stock: 8,
    price: 39999000,
    company: 'PT Datascrip',
    created_at: '2023-03-05T14:20:00Z',
    updated_at: '2023-06-21T15:40:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b107"),
    name: 'Corsair K95 RGB Platinum',
    category: 'Aksesoris Komputer',
    stock: 25,
    price: 2599000,
    company: 'PT Corsair Indonesia',
    created_at: '2023-03-01T11:20:00Z',
    updated_at: '2023-06-23T14:30:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b101"),
    name: 'Fujifilm X-T4',
    category: 'Kamera',
    stock: 12,
    price: 27999000,
    company: 'PT Fujifilm Indonesia',
    created_at: '2023-03-15T09:45:00Z',
    updated_at: '2023-06-23T11:30:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b0fd"),
    name: 'Google Pixel 6',
    category: 'Smartphone',
    stock: 15,
    price: 10999000,
    company: 'Google LLC',
    created_at: '2023-02-15T09:45:00Z',
    updated_at: '2023-06-21T13:20:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b0f8"),
    name: 'LG UltraFine 5K Display',
    category: 'Elektronik',
    stock: 12,
    price: 9999000,
    company: 'PT LG Electronics Indonesia',
    created_at: '2023-03-15T11:45:00Z',
    updated_at: '2023-06-20T14:30:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b0f5"),
    name: 'Laptop Asus ROG',
    category: 'Elektronik',
    stock: 15,
    price: 15000000,
    company: 'PT Asus Indonesia',
    created_at: '2023-01-15T08:00:00Z',
    updated_at: '2023-06-20T10:30:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b104"),
    name: 'Logitech MX Master 3',
    category: 'Aksesoris Komputer',
    stock: 50,
    price: 1499000,
    company: 'PT Logitech Indonesia',
    created_at: '2023-01-20T13:45:00Z',
    updated_at: '2023-06-22T09:10:00Z',
    deleted_at: null
  },
  {
    _id: ObjectId("678ce0499a05e75c5db1b102"),
    name: 'Nikon Z6 II',
    category: 'Kamera',
    stock: 7,
    price: 31999000,
    company: 'PT Nikon Indonesia',
    created_at: '2023-03-20T13:00:00Z',
    updated_at: '2023-06-24T16:20:00Z',
    deleted_at: null
  }
]
```

## Insert

Untuk menambahkan data ke MongoDB, terdapat dua query dasar.

```javascript
db.collection.insertOne(object); // Menambahkan satu data saja
db.collection.insertMany(object); // Menambahkan banyak objek
```

> Apa yang terjadi kalau saya insertOne dengan data array?

Well, seperti ini nantinya:

```javascript
db.users.insertOne([
  { name: "Alice", email: "alice@example.com" },
  { name: "Bob", email: "bob@example.com" },
  { name: "Charlie", email: "charlie@example.com" },
  { name: "David", email: "david@example.com" },
  { name: "Eve", email: "eve@example.com" },
]);
```

```bash
Atlas atlas-969x7s-shard-0 [primary] coba> db.users.find();
[
  {
    _id: ObjectId("67892b2cc0387848d86fb654"),
    name: 'Alice',
    email: 'alice@example.com'
  },
  {
    _id: ObjectId("67892b2cc0387848d86fb655"),
    name: 'Bob',
    email: 'bob@example.com'
  },
  {
    _id: ObjectId("67892b2cc0387848d86fb656"),
    name: 'Charlie',
    email: 'charlie@example.com'
  },
  {
    _id: ObjectId("67892b2cc0387848d86fb657"),
    name: 'David',
    email: 'david@example.com'
  },
  {
    _id: ObjectId("67892b2cc0387848d86fb658"),
    name: 'Eve',
    email: 'eve@example.com',
    phone: '123-456-7890'
  },
  {
    _id: ObjectId("678cae3d9a05e75c5db1b0cb"),
    name: 'Hudya',
    email: 'hudya@example.com'
  },
  {
    '0': { name: 'Alice', email: 'alice@example.com' },
    '1': { name: 'Bob', email: 'bob@example.com' },
    '2': { name: 'Charlie', email: 'charlie@example.com' },
    '3': { name: 'David', email: 'david@example.com' },
    '4': { name: 'Eve', email: 'eve@example.com' },
    _id: ObjectId("678cbf529a05e75c5db1b0e0")
  }
]
```

Gunakan `insertOne` hanya untuk satu data saja dengan tipe `object`.

### Bulk Write

Pada proses insert sebenarnya kita dapat menggunakan query bernama Bulk Write. Dimana query ini ditujukan untuk membuat beberapa operasi secara bersamaan pada satu collection. Contoh:

```javascript
db.inventories.bulkWrite([
  {
    updateOne: {
      filter: { _id: ObjectId("678cb3c89a05e75c5db1b0d3") },
      update: {
        $inc: { stock: 5 },
        $set: { updated_at: new Date() },
      },
    },
  },
  {
    updateOne: {
      filter: { _id: ObjectId("678cb3c89a05e75c5db1b0df") },
      update: {
        $inc: { stock: -2 },
        $set: { updated_at: new Date() },
      },
    },
  },
]);
```

> [!WARNING]
> Ganti ObjectID di atas dengan Object Id yang ada di data kamu.

Hasil apabila ID-nya sesuai dengan data yang ada pada database kamu.

```bash
{
  acknowledged: true,
  insertedCount: 0,
  insertedIds: {},
  matchedCount: 2,
  modifiedCount: 2,
  deletedCount: 0,
  upsertedCount: 0,
  upsertedIds: {}
}
```

## Update

Nah update ada beberapa fungsi, lihat tabel di bawah ini:

| Operasi | Metode             | Deskripsi                                                                        |
| ------- | ------------------ | -------------------------------------------------------------------------------- |
| Update  | updateOne()        | Memperbarui satu dokumen yang cocok dengan filter                                |
| Update  | updateMany()       | Memperbarui banyak dokumen yang cocok dengan filter                              |
| Update  | replaceOne()       | Mengganti satu dokumen yang cocok dengan filter                                  |
| Update  | findOneAndUpdate() | Memperbarui satu dokumen dan mengembalikan dokumen (sebelum atau sesudah update) |

Kita coba praktek langsung!

Pertama kita coba `updateOne()`.

```javascript
db.inventories.updateOne(
  { _id: Masukkan ObjectId },
  { $set: { stock: 20, updated_at: new Date() } }
)
```

Perintah di atas akan memperbarui satu data saja, misalnya ada dua kolom dengan nilai yang sama, data yang diperbarui hanya akan satu saja.

Kedua kita coba `updateMany()`.

```javascript
db.inventories.updateMany(
  { category: "Smartphone" },
  { $inc: { stock: 5 }, $set: { updated_at: new Date() } }
);
```

Kita menaikkan semua stock smartphone sebanyak 5 buah.

Ketiga kita coba `replaceOne`.

```javascript
db.inventories.replaceOne(
  { _id: Masukkan ObjectId },
  {
    name: "iPhone 14 Pro",
    category: "Smartphone",
    stock: 30,
    price: 19999000,
    company: "Apple Inc.",
    created_at: new Date(),
    updated_at: new Date(),
    deleted_at: null,
  }
);
```

Fungsi `replaceOne` akan menimpa keseluruhan dokumen berdasarkan kolom yang diinginkan dengan dokumen baru.

Terakhir, gunakan `findOneAndUpdate()`

```javascript
db.inventories.findOneAndUpdate(
  { _id: Masukkan ObjectId },
  { $set: { price: 3999000 }, $inc: { stock: -1 } },
  { returnDocument: "after" }
);
```

Menggunakan atribut `returnDocument: "after"` akan mengembalikan dokumen yang diperbarui.

```bash
Atlas atlas-969x7s-shard-0 [primary] coba> db.inventories.findOneAndUpdate(
...   { _id: ObjectId("678cb3c89a05e75c5db1b0df") },
...   { $set: { price: 3999000 }, $inc: { stock: -1 } },
...   { returnDocument: "after" }
... );
{
  _id: ObjectId("678cb3c89a05e75c5db1b0df"),
  name: 'SteelSeries Arctis Pro',
  category: 'Aksesoris Gaming',
  stock: 17,
  price: 3999000,
  company: 'PT Steel Series Indonesia',
  created_at: '2023-02-25T15:40:00Z',
  updated_at: ISODate("2025-01-19T09:12:41.823Z"),
  deleted_at: null
}
```

## Delete

Kemudian untuk delete kita memiliki beberapa fungsi berikut.

| Operasi | Metode             | Deskripsi                                                     |
| ------- | ------------------ | ------------------------------------------------------------- |
| Delete  | deleteOne()        | Menghapus satu dokumen yang cocok dengan filter               |
| Delete  | deleteMany()       | Menghapus banyak dokumen yang cocok dengan filter             |
| Delete  | findOneAndDelete() | Menghapus satu dokumen dan mengembalikan dokumen yang dihapus |

Berikut contoh operasinya, pertama kita coba `deleteOne()`.

```javascript
db.inventories.deleteOne({ _id: Masukkan ObjectId })
```

Kemudian kita coba `deleteMany()`, untuk fungsi ini kita bisa menggunakan kolom yang sekiranya memiliki kondisi stok adalah 0.

```javascript
db.inventories.deleteMany({ stock: 0 });
```

Terakhir fungsi `findOneAndDelete()` ini sama seperti update, bedanya hanya aksinya saja.

```javascript
db.inventories.findOneAndDelete(
  { category: "Peralatan Dapur", stock: { $lt: 5 } },
  { sort: { price: 1 } } // Menghapus item termurah jika ada beberapa yang cocok
);
```

Pada query di atas ada kemungkinan dimana kita ingin menghapus data di kategori Peralatan daper yang stoknya di bawah 5 tapi kita hanya ingin menghapus barang dengan harga termurah saja, sehingga kita sort. Contoh lainnya dengan ID adalah sebagai berikut:

```javascript
db.inventories.findOneAndDelete({ _id: Masukkan ObjectId })
```

Contoh:

```bash
Atlas atlas-969x7s-shard-0 [primary] coba> db.inventories.findOneAndDelete({ _id: ObjectId("678cb3c89a05e75c5db1b0df") });
{
  _id: ObjectId("678cb3c89a05e75c5db1b0df"),
  name: 'SteelSeries Arctis Pro',
  category: 'Aksesoris Gaming',
  stock: 17,
  price: 3999000,
  company: 'PT Steel Series Indonesia',
  created_at: '2023-02-25T15:40:00Z',
  updated_at: ISODate("2025-01-19T09:12:41.823Z"),
  deleted_at: null
}
Atlas atlas-969x7s-shard-0 [primary] coba> db.inventories.find({ _id: ObjectId("678cb3c89a05e75c5db1b0df") });
```

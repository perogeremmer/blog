# 4 - Struktur Dokumen dan Tipe Data

MongoDB, sebagai database dokumen, menyimpan data dalam format BSON (Binary JSON). Hal ini memungkinkan fleksibilitas dalam struktur data dan mendukung berbagai tipe data.

## Tipe Data di MongoDB

MongoDB mendukung beberapa tipe data utama:

1. **String**: Untuk menyimpan teks. Contoh: `"name": "John Doe"`

2. **Integer**: Bilangan bulat 32-bit atau 64-bit. Contoh: `"age": 30`

3. **Double**: Untuk angka floating-point. Contoh: `"price": 99.99`

4. **Boolean**: Nilai true atau false. Contoh: `"isActive": true`

5. **Date**: Menyimpan tanggal dan waktu. Contoh: `"createdAt": ISODate("2023-11-15T12:00:00Z")`

6. **Null**: Merepresentasikan nilai null atau tidak ada. Contoh: `"middleName": null`

7. **Array**: Kumpulan nilai. Contoh: `"hobbies": ["reading", "cycling"]`

8. **Object/Embedded Document**: Dokumen bersarang. Contoh: `"address": { "street": "123 Main St", "city": "Anytown" }`

9. **ObjectId**: Identifier unik yang dihasilkan secara otomatis. Contoh: `"_id": ObjectId("507f1f77bcf86cd799439011")`

10. **Binary Data**: Untuk menyimpan data biner seperti gambar.

11. **Code**: Untuk menyimpan JavaScript code.

12. **Regular Expression**: Untuk pattern matching.

## Struktur Dokumen

Dokumen di MongoDB adalah struktur data yang mirip dengan JSON. Berikut adalah contoh dokumen MongoDB:

```json
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "John Doe",
  "age": 30,
  "email": "john@example.com",
  "isSubscribed": true,
  "interests": ["technology", "sports", "music"],
  "address": {
    "street": "123 Main St",
    "city": "Anytown",
    "country": "USA"
  },
  "orderHistory": [
    {
      "orderId": "ORD001",
      "date": ISODate("2023-10-15T10:30:00Z"),
      "total": 150.75
    },
    {
      "orderId": "ORD002",
      "date": ISODate("2023-11-01T14:45:00Z"),
      "total": 89.99
    }
  ],
  "lastLogin": ISODate("2023-11-15T08:00:00Z")
}
```

Karakteristik utama dokumen MongoDB:

- Fleksibel: Tidak memerlukan skema yang kaku.
- Nested: Dapat berisi sub-dokumen dan array.
- Dinamis: Mudah diubah dan diperluas.

## Fleksibilitas Skema dan Potensi Inkonsistensi di MongoDB

MongoDB dikenal dengan skema fleksibelnya, yang memungkinkan dokumen dalam satu koleksi memiliki struktur yang berbeda. Meskipun ini memberikan fleksibilitas yang tinggi, hal ini juga dapat menyebabkan inkonsistensi struktur antar dokumen. Berikut penjelasannya:

### Konsep Skema Fleksibel

- MongoDB tidak memaksakan skema yang kaku pada koleksi.
- Setiap dokumen dalam satu koleksi dapat memiliki struktur (fields) yang berbeda.

### Contoh Inkonsistensi Struktur

Misalkan kita memiliki koleksi `users` dengan 5 dokumen.

Jalankan perintah berikut

```bash
db.users.insertMany([
  { "name": "Alice", "email": "alice@example.com" },
  { "name": "Bob", "email": "bob@example.com" },
  { "name": "Charlie", "email": "charlie@example.com" },
  { "name": "David", "email": "david@example.com" },
  { "name": "Eve", "email": "eve@example.com" }
])
```

Lalu jalankan perintah berikut:

```bash
db.users.find()
```

Hasilnya seperti ini:

```json
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
    email: 'eve@example.com'
  }
]

```

Jika kita menambahkan atribut baru ke salah satu dokumen:

```bash
db.users.updateOne(
  { _id: ObjectId("67892b2cc0387848d86fb658") },
  { $set: { phone: "123-456-7890" } }
)
```

Setelah operasi ini, jalankan kembali perintah berikut:

```bash
db.users.find()
```

Hasilnya

```json
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
  }
]
```

Semua data kecuali milik eve tidak memiliki atribut `phone`. Mengapa?

- Inkonsistensi Struktur: Hanya dokumen Eve yang memiliki field phone. Dokumen lainnya tidak terpengaruh dan tidak memiliki field ini.
- Quering: Query yang melibatkan field phone hanya akan relevan untuk dokumen yang memiliki field tersebut.
- Aplikasi: Aplikasi harus didesain untuk menangani kemungkinan ketidakhadiran field tertentu di beberapa dokumen.

Tapi sejujurnya jangan panik, ini tidak akan mengubah bagaimana query bekerja, hanya saja datanya menjadi bolong dan tidak konsisten. Kamu bisa mencoba dua query di bawah ini:

```bash
# Tampilkan user yang phonenya null

db.users.find({phone: {$e: null}});
```

```bash
# Tampilkan user yang phonenya tidak null

db.users.find({phone: {$ne: null}});
```

Dalam mencari dokumen, kamu juga bisa mengetiknya dengan enter seperti GIF di bawah ini:

![alt text](<./assets/3-installation/Peek 2025-01-16 22-58.gif>)

### Mengelola Inkonsistensi

Inkonsistensi memang terkesan bermasalah bagi mereka yang memang membutuhkan konsistensi data, **walau pada MongoDB sebenarnya hal tersebut tidak terlalu dibutuhkan** karena pada dasarnya memang MongoDB diciptakan untuk membuat data menjadi dinamis.

Namun ada beberapa hal yang dapat dilakukan untuk membuat data tetap konsisten.

- Update Masal: Jika diperlukan, lakukan update ke semua dokumen untuk menambahkan field baru.

  ```javascript
  db.users.updateMany({ phone: { $exists: false } }, { $set: { phone: null } });
  ```

- Validasi Skema: Gunakan JSON Schema validation untuk memaksakan struktur tertentu jika diperlukan.

- Desain Aplikasi: Selalu cek keberadaan field sebelum mengaksesnya dalam aplikasi.

- Dokumentasi: Pastikan struktur data didokumentasikan dengan baik, termasuk field opsional.

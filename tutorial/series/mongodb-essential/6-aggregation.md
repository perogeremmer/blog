# 6 - Aggregation

- [6 - Aggregation](#6---aggregation)
  - [Overview](#overview)
  - [Aggregation Update](#aggregation-update)
  - [Aggregation](#aggregation)
  - [Sintaks Aggregation](#sintaks-aggregation)
  - [Praktek](#praktek)
  - [Join Table](#join-table)
  - [Praktek Part 2](#praktek-part-2)

## Overview

MongoDB menyediakan fitur untuk memperbarui data yang kompleks menggunakan aggregation pipeline. Ini berguna kalo kamu perlu melakukan transformasi atau kalkulasi sebelum melakukan update terhadap sebuah data.

## Aggregation Update

Aggregation update pada MongoDB adalah fitur yang menggabungkan kekuatan pipeline agregasi dengan kemampuan untuk memodifikasi dokumen secara langsung. Fitur ini memungkinkan developer untuk melakukan perubahan data yang kompleks dan menerapkan logika langsung di dalam operasi update database. Dalam praktiknya, developer dapat menggunakan berbagai tahap agregasi seperti `$set`, `$unset`, `$addFields`, dan lainnya dalam konteks operasi update.

Konsep dasar dari aggregation update adalah bahwa developer dapat menjalankan serangkaian tahap agregasi untuk setiap dokumen yang cocok dengan kriteria update. Ini membuka peluang untuk melakukan kalkulasi yang rumit, perubahan data yang mendalam, dan bahkan menggunakan data dari dokumen itu sendiri sebagai bagian dari proses update. Bagian terpenting untuk diingat adalah bahwa seluruh pipeline dijalankan dalam sebuah operasi untuk setiap dokumen.

Agar dapat memahaminya, cobalah query berikut:

```javascript
db.inventories.updateMany({ category: "Smartphone" }, [
  {
    $set: {
      discountedPrice: { $multiply: ["$price", 0.9] },
      lastUpdated: "$$NOW",
    },
  },
  {
    $set: {
      priceRange: {
        $switch: {
          branches: [
            { case: { $lt: ["$discountedPrice", 5000000] }, then: "Budget" },
            {
              case: { $lt: ["$discountedPrice", 10000000] },
              then: "Mid-range",
            },
            { case: { $gte: ["$discountedPrice", 10000000] }, then: "Premium" },
          ],
          default: "Unknown",
        },
      },
    },
  },
]);
```

Apa yang dijalankan dari kode di atas?

- Memperbarui semua dokumen dalam kategori `"Smartphone"`.
- Pertama, menambahkan kolom `discountedPrice` dimana menghitung dari harga diskon (90% dari harga asli) dan menambahkan timestamp update.
- Kedua, menambahkan kolom baru yaitu teks `priceRange` berdasarkan harga diskon.

Pertanyaannya, mengapa kita harus memisahkan dua buah `$set`? Sintaks pertama adalah kita membuat field `discountedPrice`, sedangkan `$set` yang kedua adalah mengatur `priceRange`. Jawabannya adalah sebagai berikut.

1. Urutan Eksekusi
   Dalam pipeline agregasi MongoDB, setiap tahap dieksekusi secara berurutan. Hasil dari satu tahap menjadi input untuk tahap berikutnya.

2. Dependensi Data
   Dalam contoh di atas, perhitungan field `priceRange` bergantung pada nilai dari field `discountedPrice` yang dihitung pada tahap pertama.

3. Visibilitas Field Baru
   Field baru yang dibuat dalam satu tahap `$set` tidak tersedia untuk digunakan pada tahap yang sama, tetapi bisa digunakan di tahap-tahap berikutnya.

Jadi, alasan utama mengapa priceRange tidak dimasukkan ke set yang pertama adalah karena operasi tersebut bergantung pada nilai `discountedPrice` yang dihitung pada tahap pertama. MongoDB tidak akan mengenali `discountedPrice` sebagai field yang valid untuk digunakan dalam perhitungan ketika mengatur `priceRange`, karena field tersebut belum ada saat tahap dimulai.

## Aggregation

Aggregation pipeline di MongoDB adalah sebuah fungsi yang powerful untuk melakukan transformasi dan analisis data.

Apabila dibandingkan dengan SQL seperti filtering, grouping, dan sorting, aggregation pipeline menawarkan pendekatan yang jauh lebih fleksibel dan adaptif.

Dalam pipeline ini, data dapat mengalir melalui serangkaian tahapan, di mana output dari satu tahap menjadi input untuk tahap berikutnya, memungkinkan kontrol yang sangat granular atas proses transformasi data.

Agar dapat memahaminya lebih lanjut, coba jalankan query berikut.

```javascript
db.inventories.aggregate([
  // Stage 1: Filter dokumen
  { $match: { stock: { $gt: 0 } } },

  // Stage 2: Meanmpilkan data berdasarkan kategori
  {
    $group: {
      _id: "$category",
      totalItems: { $sum: 1 },
      averagePrice: { $avg: "$price" },
      totalStock: { $sum: "$stock" },
    },
  },

  // Stage 3: Tambahkan field baru
  {
    $addFields: {
      averagePrice: { $round: ["$averagePrice", 2] },
    },
  },

  // Stage 4: Urutkan hasil
  { $sort: { totalItems: -1 } },
]);
```

Penjelasan dari query di atas adalah sebagai berikut.

- `$match`: Pada bagian ini, query disiapkan untuk mencari dokumen dengan kriteria stok > 0.
- `$group`: Mengelompokkan berdasarkan kategori dan menghitung statistik.
- `$addFields`: Membulatkan harga rata-rata.
- `$sort`: Mengurutkan hasil berdasarkan jumlah item.

Kalau disamakan dengan SQL maka querynya akan seperti ini.

```sql
SELECT
    category AS _id,
    COUNT(*) AS totalItems,
    ROUND(AVG(price), 2) AS averagePrice,
    SUM(stock) AS totalStock
FROM
    inventories
WHERE
    stock > 0
GROUP BY
    category
ORDER BY
    totalItems DESC;
```

Secara teori, memang untuk membuat query se-sederhana di MongoDB tidak semudah membuatnya di SQL.

## Sintaks Aggregation

MongoDB Menawarkan banyak sintaks aggregation yang dapat digunakan pada saat membuat pipeline aggregation, berikut adalah fungsi yang disediakan.

| Fungsi     | Deskripsi                                                                                                  |
| ---------- | ---------------------------------------------------------------------------------------------------------- |
| $match     | Memfilter dokumen berdasarkan kriteria tertentu, mirip dengan WHERE clause di SQL.                         |
| $group     | Mengelompokkan dokumen berdasarkan kriteria tertentu dan melakukan agregasi pada kelompok tersebut.        |
| $sort      | Mengurutkan dokumen berdasarkan satu atau lebih field.                                                     |
| $project   | Memilih field tertentu, mengubah atau menambahkan field baru ke dokumen output.                            |
| $lookup    | Melakukan operasi "left outer join" dengan koleksi lain, mirip dengan JOIN di SQL tapi lebih fleksibel.    |
| $unwind    | Mendeconstruct array field dari input dokumen untuk menghasilkan dokumen output untuk setiap elemen array. |
| $addFields | Menambahkan field baru ke dokumen tanpa menghapus field yang sudah ada.                                    |
| $limit     | Membatasi jumlah dokumen yang diproses dalam pipeline.                                                     |
| $skip      | Melewati sejumlah dokumen dalam pipeline.                                                                  |
| $count     | Menghitung jumlah dokumen dalam pipeline pada tahap tertentu.                                              |
| $facet     | Memungkinkan penggunaan multiple aggregation pipeline dalam satu stage.                                    |
| $bucket    | Mengelompokkan dokumen ke dalam "buckets" berdasarkan ekspresi tertentu.                                   |
| $geoNear   | Mengembalikan dokumen berdasarkan kedekatan geografis.                                                     |
| $out       | Menulis hasil aggregation pipeline ke koleksi baru atau yang sudah ada.                                    |
| $merge     | Menggabungkan hasil aggregation pipeline dengan koleksi yang ada.                                          |

## Praktek

Untuk berlatih terkait aggregation, kita akan gunakan database `sample_mflix` yang sudah disediakan MongoDB Atlas ketika kamu membuat database.

```bash
Atlas atlas-969x7s-shard-0 [primary] test> show dbs;
coba          144.00 KiB
sample_mflix  114.23 MiB
admin         348.00 KiB
local           8.93 GiB
```

Jangan lupa untuk pindah database dengan cara menuliskan perintah `use sample_mflix` pada terminal.

Pertama kita akan coba untuk menampilkan data dimana

```javascript
db.movies.aggregate([
  { $unwind: "$genres" },
  { $group: { _id: "$genres", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 10 },
  { $set: { genre: "$_id", _id: "$$REMOVE" } },
]);
```

Kamu akan melihat hasil seperti ini.

```bash
[
  { count: 12385, genre: 'Drama' },
  { count: 6532, genre: 'Comedy' },
  { count: 3318, genre: 'Romance' },
  { count: 2457, genre: 'Crime' },
  { count: 2454, genre: 'Thriller' },
  { count: 2381, genre: 'Action' },
  { count: 1900, genre: 'Adventure' },
  { count: 1834, genre: 'Documentary' },
  { count: 1470, genre: 'Horror' },
  { count: 1269, genre: 'Biography' }
]
```

Kita mencoba untuk menghitung berapa banyak semua dokumen berdasarkan `genres`. Perlu diketahui bahwa struktur sample dari salah satu data adalah sebagai berikut:

```javascript
{
  _id: ObjectId("573a1390f29313caabcd42e8"),
  plot: 'A group of bandits stage a brazen train hold-up, only to find a determined posse hot on their heels.',
  genres: [ 'Short', 'Western' ],
  runtime: 11,
  cast: [
    'A.C. Abadie',
    "Gilbert M. 'Broncho Billy' Anderson",
    'George Barnes',
    'Justus D. Barnes'
  ],
  poster: 'https://m.media-amazon.com/images/M/MV5BMTU3NjE5NzYtYTYyNS00MDVmLWIwYjgtMmYwYWIxZDYyNzU2XkEyXkFqcGdeQXVyNzQzNzQxNzI@._V1_SY1000_SX677_AL_.jpg',
  title: 'The Great Train Robbery',
  fullplot: "Among the earliest existing films in American cinema - notable as the first film that presented a narrative story to tell - it depicts a group of cowboy outlaws who hold up a train and rob the passengers. They are then pursued by a Sheriff's posse. Several scenes have color included - all hand tinted.",
  languages: [ 'English' ],
  released: ISODate("1903-12-01T00:00:00.000Z"),
  directors: [ 'Edwin S. Porter' ],
  rated: 'TV-G',
  awards: { wins: 1, nominations: 0, text: '1 win.' },
  lastupdated: '2015-08-13 00:27:59.177000000',
  year: 1903,
  imdb: { rating: 7.4, votes: 9847, id: 439 },
  countries: [ 'USA' ],
  type: 'movie',
  tomatoes: {
    viewer: { rating: 3.7, numReviews: 2559, meter: 75 },
    fresh: 6,
    critic: { rating: 7.6, numReviews: 6, meter: 100 },
    rotten: 0,
    lastUpdated: ISODate("2015-08-08T19:16:10.000Z")
  },
  num_mflix_comments: 0
}
```

Dapat dilihat bahwa `genres` merupakan array, sehingga menggunakan `$unwind` akan membongkar array tersebut menjadi sebuah dokumen tersendiri.

Penggunaan grouping dengan `_id` meskipun diisi dengan nilai `genres` film adalah rumus MongoDB yang mengharuskan kita grouping ke dalam field `_id`.

Kemudian pada baris `$sort` kita ingin mengurutkan nilai dari paling terbesar lalu ditampilkan 10 data saja dengan `$limit`.

Terakhir, fungsi `$set` akan menampilkan kolom sesuai yang kita inginkan, disini kita akan menampilkannya dengan nama `genre` dan `count`.

Data `{ count: 12385, genre: 'Drama' }` dimana genre baru saja diinput pada bagian akhir yaitu di dalam `$set`.

Apabila kamu ingin merubah agar genre berada di depan kemudian count dihilangkan dan diganti dengan nama lain, kamu dapat mencoba query berikut:

```bash
db.movies.aggregate([
  { $unwind: "$genres" },
  { $group: { _id: "$genres", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 10 },
  { $set: {
      genre: "$_id",
      jumlah: "$count",
      _id: "$$REMOVE",
      count: "$$REMOVE"
    }
  }
])
```

Kita hilangkan field count dan diganti field baru.

---

Ketika `genres` merupakan nilai array sehingga harus menggunakan sintaks `$unwind`, maka untuk kolom lain seperti `rated` tidak perlu. Coba input query berikut:

```bash
db.movies.aggregate([
  { $group: { _id: "$rated", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 10 },
  { $set: { rating: "$_id", _id: "$$REMOVE" } }
])
```

## Join Table

Menggunakan pipeline aggregation, kita dapat menggunakan fungsi `$lookup` yang sama maknanya dengan join.

Coba input query di bawah ini:

```javascript
db.comments.aggregate([
  // Sort comments by date descending
  { $sort: { date: -1 } },

  // Limit to last 10 comments
  { $limit: 10 },

  // Lookup to get movie information
  {
    $lookup: {
      from: "movies",
      localField: "movie_id",
      foreignField: "_id",
      as: "movie_info",
    },
  },

  // Unwind the movie_info array
  { $unwind: "$movie_info" },

  // Project only the fields we need
  {
    $project: {
      _id: 1,
      text: 1,
      name: 1,
      movie_title: "$movie_info.title",
      date: 1,
    },
  },

  // Sort again by date to ensure order after lookup
  { $sort: { date: -1 } },
]);
```

Hasil yang kamu dapatkan akan menjadi seperti ini:

```javascript
[
  {
    _id: ObjectId("5a9427648b0beebeb6959449"),
    name: "Victor Patel",
    text: "Fugit asperiores libero ullam culpa soluta. Sint maxime expedita rem voluptas ullam labore aliquid.",
    date: ISODate("2017-09-13T00:37:11.000Z"),
    movie_title: "Will Success Spoil Rock Hunter?",
  },
  {
    _id: ObjectId("5a9427648b0beebeb695f8f7"),
    name: "Selyse Baratheon",
    text: "Provident iure quas ducimus soluta voluptates hic perferendis. Perferendis tenetur deleniti explicabo eos. Natus labore soluta expedita animi.",
    date: ISODate("2017-09-12T08:32:53.000Z"),
    movie_title: "The Jungle Creature: Hugo",
  },
  {
    _id: ObjectId("5a9427648b0beebeb695abe6"),
    name: "Megan Richards",
    text: "Ratione vel aspernatur unde dolore at eius. Aliquam quibusdam vitae quos ea consequatur fugiat reprehenderit. Quibusdam maxime perspiciatis accusantium dolores molestias debitis.",
    date: ISODate("2017-09-11T23:10:35.000Z"),
    movie_title: "Sounder",
  },
  {
    _id: ObjectId("5a9427658b0beebeb696f61c"),
    name: "Missandei",
    text: "Explicabo fuga rem necessitatibus saepe. Fugiat explicabo culpa adipisci repellendus voluptatem qui nesciunt.",
    date: ISODate("2017-09-11T16:52:51.000Z"),
    movie_title: "National Treasure",
  },
  {
    _id: ObjectId("5a9427648b0beebeb6959ec6"),
    name: "Jason Hernandez",
    text: "Quod soluta qui tempora totam. Dolore dicta rem eius sapiente rerum dolorem. Mollitia et dolores eius ad voluptas.",
    date: ISODate("2017-09-11T13:24:21.000Z"),
    movie_title: "The War Is Over",
  },
  {
    _id: ObjectId("5a9427658b0beebeb697485a"),
    name: "Khal Drogo",
    text: "Cum id alias ut ea provident corrupti harum at. Dolores eaque harum doloremque ipsa. Eum omnis culpa reiciendis pariatur ea blanditiis voluptatum. Tempore quod consequatur neque quidem.",
    date: ISODate("2017-09-10T07:56:58.000Z"),
    movie_title: "Les amants du Flore",
  },
  {
    _id: ObjectId("5a9427658b0beebeb6971c22"),
    name: "Meera Reed",
    text: "Doloremque ab officiis corrupti. Occaecati laborum blanditiis repellendus. Nemo alias nihil magni quo iure at omnis eius.",
    date: ISODate("2017-09-10T06:24:48.000Z"),
    movie_title: "Terminator Salvation",
  },
  {
    _id: ObjectId("5a9427658b0beebeb696ec0d"),
    name: "Michael Moore",
    text: "Consequuntur mollitia accusantium assumenda voluptate. Perferendis velit repudiandae iusto expedita. Consequuntur ut temporibus vero natus illum harum.",
    date: ISODate("2017-09-09T16:58:34.000Z"),
    movie_title: "A Cinderella Story",
  },
  {
    _id: ObjectId("5a9427658b0beebeb6970956"),
    name: "Garrett Obrien",
    text: "Repudiandae consectetur facilis ratione ab quia. Accusamus quo amet maiores quae in.",
    date: ISODate("2017-09-09T13:16:33.000Z"),
    movie_title: "Shrek the Third",
  },
  {
    _id: ObjectId("5a9427658b0beebeb696e6b3"),
    name: "Justin Williams",
    text: "Aliquam blanditiis nemo ea repudiandae. Error earum minus dolore animi. Ratione eaque labore tenetur ipsum quibusdam ratione.",
    date: ISODate("2017-09-09T10:17:02.000Z"),
    movie_title: "Ocean's Twelve",
  },
];
```

## Praktek Part 2

Lalu kamu juga bisa menggunakan aggregation untuk menyelesaikan kasus di bawah ini:

1. Tampilkan sepuluh aktor yang memiliki film paling tinggi.
2. Tampilkan sepuluh film apakah yang memiliki rata-rata nilai paling tinggi.

Jawaban nomor satu:

```javascript
db.movies.aggregate([
  // Unwind the cast array
  { $unwind: "$cast" },

  // Group by actor and count their movies
  {
    $group: {
      _id: "$cast",
      movieCount: { $sum: 1 },
    },
  },

  // Sort by movie count descending
  { $sort: { movieCount: -1 } },

  // Limit to top 10
  { $limit: 10 },

  // Project for nicer output
  {
    $project: {
      _id: 0,
      actor: "$_id",
      movieCount: 1,
    },
  },
]);
```

Jawaban nomor dua:

```javascript
db.movies.aggregate([
  // Filter movies with at least 1000 IMDB votes
  {
    $match: {
      "imdb.votes": { $gte: 1000 },
      "imdb.rating": { $exists: true },
    },
  },

  // Sort by IMDB rating descending
  { $sort: { "imdb.rating": -1 } },

  // Limit to top 10
  { $limit: 10 },

  // Project desired fields
  {
    $project: {
      _id: 1,
      title: 1,
      rating: "$imdb.rating",
      votes: "$imdb.votes",
    },
  },
]);
```

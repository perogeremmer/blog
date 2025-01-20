# 6 - Aggregation

## Overview

MongoDB menyediakan fitur untuk memperbarui data yang kompleks menggunakan aggregation pipeline. Ini berguna kalo kamu perlu melakukan transformasi atau kalkulasi sebelum melakukan update terhadap sebuah data.

## Aggregation Update

Cobalah query berikut

```javascript
db.inventories.updateMany(
  { category: "Smartphone" },
  [
    { $set: { 
        discountedPrice: { $multiply: ["$price", 0.9] },
        lastUpdated: "$$NOW"
    }},
    { $set: {
        priceRange: {
          $switch: {
            branches: [
              { case: { $lt: ["$discountedPrice", 5000000] }, then: "Budget" },
              { case: { $lt: ["$discountedPrice", 10000000] }, then: "Mid-range" },
              { case: { $gte: ["$discountedPrice", 10000000] }, then: "Premium" }
            ],
            default: "Unknown"
          }
        }
    }}
  ]
)
```

Apa yang dijalankan dari kode di atas?

- Memperbarui semua dokumen dalam kategori `"Smartphone"`.
- Pertama, menambahkan kolom `discountedPrice` dimana menghitung dari harga diskon (90% dari harga asli) dan menambahkan timestamp update.
- Kedua, menambahkan kolom baru yaitu teks `priceRange` berdasarkan harga diskon.

## Aggregation

Aggregation pipeline di MongoDB memiliki beberapa kesamaan dengan SQL, termasuk konsep alias dan grouping, tetapi sebenarnya lebih luas dan fleksibel.

Cobalah query berikut.

```javascript
db.inventories.aggregate([
  // Stage 1: Filter dokumen
  { $match: { stock: { $gt: 0 } } },
  
  // Stage 2: Meanmpilkan data berdasarkan kategori
  { $group: {
      _id: "$category",
      totalItems: { $sum: 1 },
      averagePrice: { $avg: "$price" },
      totalStock: { $sum: "$stock" }
  }},
  
  // Stage 3: Tambahkan field baru
  { $addFields: {
      averagePrice: { $round: ["$averagePrice", 2] }
  }},
  
  // Stage 4: Urutkan hasil
  { $sort: { totalItems: -1 } }
])
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
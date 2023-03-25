<img src="assets/memahami-normalisasi-database-relasi/6d51d6f8-e5e9-4c53-8ff9-8fe607199c79.png" style="border-radius:10px;" />

<br/>

by [@perogeremmer](https://twitter.com/perogeremmer)

**Table of contents**

- [Apa aja jenis relasi di database relasional?](#apa-aja-jenis-relasi-di-database-relasional)
- [Relasi itu apa sebenernya?](#relasi-itu-apa-sebenernya)
- [One to One](#one-to-one)
- [One to Many](#one-to-many)
- [Many to Many](#many-to-many)

## Apa aja jenis relasi di database relasional?

Post ini berkaitan dengan post [memahami normalisasi di database relasion](./memahami-normalisasi-database-relasi.md), kalo kamu belom paham normalisasi, mending baca itu dulu.

## Relasi itu apa sebenernya?

Ketika kita memiliki hubungan antar tabel seperti yang dibuat di normalisasi, umumnya kita akan ngelihat tiga jenis relasi yang memungkinkan, yaitu:

- One to One
- One to Many
- Many to Many

Masing-masing dari jenis relasi ini memiliki keterkaitan data antara tabel a dengan tabel lain yang menggambarkan hubungan (relasi) dari kedua data tersebut.

## One to One

Relasi one to one adalah relasi dimana satu data hanya berkaitan dengan satu saja, artinya dia gak punya lebih dari satu data. Kalo kamu udah baca post [memahami normalisasi di database relasion](./memahami-normalisasi-database-relasi.md) pada bagian 2NF, tentunya kamu ngeliat ada tabel `employee_phones`, kan?

tabel `employees`
|id|name|email|
|-|-|-|
|1|Hudya|hudya@mail.com|
|2|Ani|ani@mail.com|
|3|Budi|budi@mail.com|

table `employee_phones`
|id|user_id|phone|
|-|-|-|
|1|1|082213071234|
|2|2|085827492857|
|3|3|081285920483|
|4|1|082145319483|

Nah, kalau misalnya kita buat data pada tabel employee_phones menjadi seperti ini, maka ini disebut relasi one to one.

table `employee_phones`
|id|user_id|phone|
|-|-|-|
|1|1|082213071234|
|2|2|085827492857|
|3|3|081285920483|

Karena **employee hanya boleh** memiliki satu nomor telfon saja.

> Tapi bang, kalo gitu jadi gak normalisasi dong datanya?

Ya enggak dong, kan itu udah dibuat bentuk 2NF, bedanya ya datanya cuma boleh satu aja, artinya secara peraturan program employee tidak boleh memiliki lebih dari satu nomor telfon.

> Seberapa sering one to one terjadi bang?

Ya tergantung kebutuhan aplikasi bray hahaha, kalo misalnya aturan dari aplikasinya setiap orang hanya boleh punya nomor satu telfon, maka hasil datanya adalah ya satu tabel hanya menyimpan satu data aja.

> Lah kalo gitu ngapain dibuat normalisasi bang?

Soalnya kalo kita butuh untuk mencari data dimana kita udah tau ID-nya tanpa harus mencari lagi di tabel employees, ini akan jadi kelebihan sendiri.

As example, anggap setiap users atau employees, gak wajib dicatet nomor telfonnya, let's say ada jumlah 10.000 pegawai, dan cuma 3.000 yang ngisi nomor telfon, misalnya lho ya.

Daripada ngescan 10.000 data untuk cari nomor telfon si Hudya, better ngescan 3.000 data untuk cari nomor telfon Hudya, dengan asumsi, kita udah tau ID-nya Hudya.

> Jadi kesimpulannya gimana bang?

Kembali ke kepercayaan dan idealisme masing-masing, karena gak ada cara yang salah, masing-masing ada kelebihan dan kekurangan. Kalo menurut elo lebih pede pake satu kolom, boleh, kalo mau dibuat normalisasi, juga boleh.

## One to Many

Masih di kasus yang sama, tanpa mengubah tabel.

tabel `employees`
|id|name|email|
|-|-|-|
|1|Hudya|hudya@mail.com|
|2|Ani|ani@mail.com|
|3|Budi|budi@mail.com|

table `employee_phones`
|id|user_id|phone|
|-|-|-|
|1|1|082213071234|
|2|2|085827492857|
|3|3|081285920483|
|4|1|082145319483|

Jelas relasi di atas adalah one to many, artinya satu data memiliki lebih dari satu data. Udah keliatan kan data yang mana?

|id|user_id|phone|
|-|-|-|
|1|1|082213071234|
|4|1|082145319483|

Yep, dua data ini dimiliki sama satu user. Hudya punya dua nomor telfon, tapi kedua nomor telfon itu dimiliki sama satu user, yaitu Hudya.

## Many to Many

Nah many to many ini umumnya terjadi pada tabel transaksi, yang mana biasanya sih, paling sering terjadi di tabel detail transaksi. Contohnya gimana? Sikat:

tabel `products`
|id|name|category_id|price|
|-|-|-|-|
|1|Odol|1|10000|
|2|Sabun 500ml|1|20000|
|3|Buku|2|25000|

tabel `transactions`
|id|order_id|user_id|
|-|-|-|
|1|BAH781|1|
|2|BAH782|3|

tabel `transaction_details`
|id|order_id|product_id|count_of_products|
|-|-|-|-|
|1|BAH781|1|4|
|2|BAH782|2|2|
|3|BAH782|3|3|

Dari sample 3NF, kita bisa ngeliat relasi many to many. Mungkin kalo kaya gini kurang keliatan ya? Kita coba tambahin data di `transaction_details` dan `transactions`.

tabel `transactions`
|id|order_id|user_id|
|-|-|-|
|1|BAH781|1|
|2|BAH782|3|
|3|BAH783|2|
|4|BAH784|1|
|4|BAH785|2|

tabel `transaction_details`
|id|order_id|product_id|count_of_products|
|-|-|-|-|
|1|BAH781|1|4|
|2|BAH782|2|2|
|3|BAH782|3|3|
|4|BAH783|2|1|
|5|BAH784|2|1|
|6|BAH785|1|10|

Dari sini bisa keliatan kan bahwa ada relasi many to many dari tabel penghubung `transaction_details`, dimana data sebuah `produk` dapat dimiliki oleh banyak `transaksi` di tabel `transaction_details` dan juga sebaliknya.

Misal ditanya nih, produk dengan ID 2 dimiliki di transaksi mana aja?

Jawabannya:

- BAH782
- BAH783
- BAH784

Terus misal ditanya, transaksi dengan ID `BAH782` memiliki produk apa aja?

Jawabannya:

- Produk ID 2
- Produk ID 3

Jadi `many to many` ini adalah relasi dimana datanya bisa lebih dari satu, dan gak cuma di satu sisi aja. Data produk bisa dimiliki di transaksi mana aja (atau lebih dari satu transaksi), dan sebuah transaksi bisa punya data produk lebih dari satu, maka relasi ini disebut `many to many`.

Jadi gimana ges? Gampang kan? :)

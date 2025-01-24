# 10 - Backup and Restore

## Overview

Untuk melakukan backup dan restore pada MongoDB, pertama kamu harus menginstall toolsnya terlebih dahulu.

Ini berbeda dengan `mongoosh` yang kita install karena `mongoosh` hanya untuk terhubung dengan cloud DB.

## Download Tools

Pertama, pergi menuju [URL berikut](https://www.mongodb.com/try/download/database-tools).

![alt text](./assets/10-backup-and-restore/1.png)

Pilih package menjadi `msi` lalu download.

Kemudian install seperti biasa:

![alt text](./assets/10-backup-and-restore/2.png)

Kemudian masukkan path tempat instalasi ke dalam environment variables.

![alt text](./assets/10-backup-and-restore/3.png)

```plain
C:\Program Files\MongoDB\Tools\100\bin
```

Sekarang buka kembali command prompt atau powershell

![alt text](./assets/10-backup-and-restore/4.png)

Harusnya tidak akan muncul teks ini:

![alt text](./assets/10-backup-and-restore/5.png)

> [!INFO]
> Cara di atas hanya berlaku untuk Windows

<br />

Untuk Mac OS silahkan [klik disini](https://www.mongodb.com/docs/database-tools/installation/installation-macos/) dan untuk Linux silahkan [klik disini](https://www.mongodb.com/docs/database-tools/installation/installation-linux/).

## Export DB ke CSV / JSON

MongoDB bisa meng-export data langsung ke CSV atau JSON, hal ini berguna biasanya untuk analisis data. Rumus dari perintahnya adalah:

```bash
mongoexport --uri mongodb+srv://username:password@host/database --collection nama_collection --type csv/json --out namafile.csv --fields kolom
```

Contoh:

```bash
mongoexport --uri mongodb+srv://admin:*****@cluster0.0kfik.mongodb.net/latihanbaru --collection inventories --type csv --out latihan.csv --fields _id,name,category,stock
```

Gunakan asterix untuk menampilkan semua kolom:

```bash
mongoexport --uri mongodb+srv://admin:*****@cluster0.0kfik.mongodb.net/latihanbaru --collection inventories --type csv --out latihan.csv --fields "*"
```

Ketika dijalankan:

```bash
hudya@perogeremmer-pc:~/Downloads$ mongoexport --uri mongodb+srv://admin:****@cluster0.0kfik.mongodb.net/latihanbaru --collection inventories --type csv --out latihan.csv --fields _id,name,category,stock
2025-01-22T23:02:07.131+0700	connected to: mongodb+srv://[**REDACTED**]@cluster0.0kfik.mongodb.net/latihanbaru
2025-01-22T23:02:07.304+0700	exported 20 records
```

Hasilnya ketika dijalankan:

![alt text](./assets/10-backup-and-restore/6.png)

## Export DB ke Binary Files

Sama seperti Export ke CSV, bedanya kita menggunakan perintah `mongodump`.

Rumusnya adalah sebagai berikut.

```bash
mongodump --uri="mongodb+srv://username:****@host/namadatabase" --out=path
```

Contoh:

```bash
mongodump --uri="mongodb+srv://admin:***@cluster0.0kfik.mongodb.net/latihanbaru" --out=./backup
```

Hasilnya seperti ini:

```bash
hudya@perogeremmer-pc:~/Documents/ccit/mongodb$ mongodump --uri="mongodb+srv://admin:*****@cluster0.0kfik.mongodb.net/latihanbaru" --out=./backup
2025-01-22T23:06:32.797+0700	writing latihanbaru.users to backup/latihanbaru/users.bson
2025-01-22T23:06:32.860+0700	writing latihanbaru.inventories to backup/latihanbaru/inventories.bson
2025-01-22T23:06:32.956+0700	done dumping latihanbaru.users (5 documents)
2025-01-22T23:06:32.987+0700	done dumping latihanbaru.inventories (20 documents)
```

![alt text](./assets/10-backup-and-restore/7.png)

![alt text](./assets/10-backup-and-restore/8.png)

## Import DB from CSV

Untuk import DB dari CSV maka rumusnya adlaah:

```bash
mongoimport --uri="mongodb+srv://<username>:<password>@<cluster-url>/<database>" --collection=<collection_name> --type=<file_type> --file=<path_to_file>
```

Contohnya dengan data CSV tadi:

```bash
mongoimport --uri="mongodb+srv://admin:***@cluster0.0kfik.mongodb.net/hasilimport" --collection=inventories --type=csv --headerline --file=/home/hudya/Documents/ccit/mongodb/latihan.csv
```

Berikut beberapa opsi flag yang bisa dilakukan:

- `--headerline`: Untuk CSV, gunakan baris pertama sebagai nama field.
- `--mode=upsert`: Update dokumen yang sudah ada atau insert jika belum ada.
- `--upsertFields`: Spesifikasi field untuk upsert.
- `--drop`: Hapus collection sebelum mengimpor.

Hasilnya sebagai berikut:

```bash
Atlas atlas-969x7s-shard-0 [primary] latihanbaru> show dbs
belajar         8.00 KiB
coba          144.00 KiB
hasilimport    40.00 KiB <-- Hasil Import
inventories    80.00 KiB
latihan        72.00 KiB
latihanbaru   128.00 KiB
latihanmongo   40.00 KiB
sample_db      72.00 KiB
sample_mflix  114.99 MiB
admin         348.00 KiB
local           8.93 GiB
```

## Import DB from Binary

Untuk Restore data dari MongoDB Binary JSON maka perintahnya adalah sebagai berikut:

```bash
mongorestore --uri="mongodb+srv://<username>:<password>@<cluster-url>/<database>" <path_to_backup>
```

Flag yang mungkin digunakan adalah:

- `--drop`: Hapus collection yang ada sebelum restore.
- `--gzip`: Untuk file backup yang dikompresi.
- `--nsInclude=<database>.<collection>`: Restore database atau collection tertentu.

Contoh:

```bash
mongorestore --uri="mongodb+srv://admin:*****@cluster0.0kfik.mongodb.net/hasil_import_binary" /home/hudya/Documents/ccit/mongodb/backup/latihanbaru
```

Hasilnya:

```bash
hudya@perogeremmer-pc:~/Documents/ccit/mongodb/backup/latihanbaru$ mongorestore --uri="mongodb+srv://admin:****@cluster0.0kfik.mongodb.net/hasil_import_binary" /home/hudya/Documents/ccit/mongodb/backup/latihanbaru
2025-01-22T23:18:53.722+0700	WARNING: On some systems, a password provided directly in a connection string or using --uri may be visible to system status programs such as `ps` that may be invoked by other users. Consider omitting the password to provide it via stdin, or using the --config option to specify a configuration file with the password.
2025-01-22T23:18:54.417+0700	The --db and --collection flags are deprecated for this use-case; please use --nsInclude instead, i.e. with --nsInclude=${DATABASE}.${COLLECTION}
2025-01-22T23:18:54.417+0700	building a list of collections to restore from /home/hudya/Documents/ccit/mongodb/backup/latihanbaru dir
2025-01-22T23:18:54.417+0700	reading metadata for hasil_import_binary.inventories from /home/hudya/Documents/ccit/mongodb/backup/latihanbaru/inventories.metadata.json
2025-01-22T23:18:54.418+0700	reading metadata for hasil_import_binary.users from /home/hudya/Documents/ccit/mongodb/backup/latihanbaru/users.metadata.json
2025-01-22T23:18:54.546+0700	restoring hasil_import_binary.inventories from /home/hudya/Documents/ccit/mongodb/backup/latihanbaru/inventories.bson
2025-01-22T23:18:54.602+0700	restoring hasil_import_binary.users from /home/hudya/Documents/ccit/mongodb/backup/latihanbaru/users.bson
2025-01-22T23:18:54.636+0700	finished restoring hasil_import_binary.inventories (20 documents, 0 failures)
2025-01-22T23:18:54.670+0700	finished restoring hasil_import_binary.users (5 documents, 0 failures)
2025-01-22T23:18:54.670+0700	no indexes to restore for collection hasil_import_binary.inventories
2025-01-22T23:18:54.670+0700	no indexes to restore for collection hasil_import_binary.users
2025-01-22T23:18:54.670+0700	25 document(s) restored successfully. 0 document(s) failed to restore.
```

```bash
Atlas atlas-969x7s-shard-0 [primary] latihanbaru> show dbs
belajar                8.00 KiB
coba                 144.00 KiB
hasil_import_binary   80.00 KiB <--- Hasil import file binary
hasilimport           40.00 KiB
inventories           80.00 KiB
latihan               72.00 KiB
latihanbaru          128.00 KiB
latihanmongo          40.00 KiB
sample_db             72.00 KiB
sample_mflix         114.99 MiB
admin                348.00 KiB
local                  8.93 GiB
```

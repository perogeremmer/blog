<img src="assets/soft-delete-teknik-ngilang-tanpa-ngapus/8d53e324-8b29-41ed-8917-5b74e088a6c8.png" style="border-radius:10px;" />

<br/>

by [@perogeremmer](https://twitter.com/perogeremmer)

**Table of contents**

- [Soft Delete, Teknik Ngilang Tanpa Ngapus](#soft-delete-teknik-ngilang-tanpa-ngapus)
- [Lah kenapa data gak boleh diapus bang?](#lah-kenapa-data-gak-boleh-diapus-bang)
- [Kasus soft delete biasa dipake dimana bang?](#kasus-soft-delete-biasa-dipake-dimana-bang)
- [Bentuk soft delete itu gimana aja bang?](#bentuk-soft-delete-itu-gimana-aja-bang)
  - [Text based](#text-based)
  - [Datetime based](#datetime-based)
- [Paling bagus pake tipe apa bang?](#paling-bagus-pake-tipe-apa-bang)
- [Berarti sebenernya data kita selama ini gak ilang ya?](#berarti-sebenernya-data-kita-selama-ini-gak-ilang-ya)

## Soft Delete, Teknik Ngilang Tanpa Ngapus

SDTNTN, adalah singkatan dari judul di atas. Nah kali ini gue mau jelasin salah satu teknik ngilangin data dari database, yaitu pake soft delete.

Seperti yang kalian tau, tentunya kalian gak asing sama syntax ini kan?

```sql
DELETE FROM table WHERE value = "?"
```

Yap, query di atas adalah query untuk ngapus (menghapus) data dari database. Permasalahannya, kadang kita gak boleh ngapus data.

## Lah kenapa data gak boleh diapus bang?

Karena datanya sensitif atau datanya berelasi. Liat dua kasus berikut:

Pertama, misal dari kasus pembuatan [database notes](../../tutorial/single/database/1-database-notes.md) kemarin, kalo lo cek di table notes, ada kolom deleted_at. Yup kolom ini tuh kolom buat soft delete dimana user boleh ngapus data, tapi bisa aja 14 hari kemudian user tersebut pengen nge-restore data itu. Sama aja lah kaya konsep di recycle bin. Sebelum data kalian bener-bener diapus, ya ditampung dulu di recycle bin.

Atau misalnya email, kalo kalian perhatiin di gmail, kita bisa ngapus email terus nge-restore email tersebut dalam waktu 30 hari. Jadi kalo misalnya salah nih ngehapus email, cek aja di tab trash, pasti ketemu.

Hal ini nandain apa? Yap, fungsi untuk restore apabila kita gak sengaja menghapus data tersebut.

Kedua, misal yang mau dihapus adalah data notes, masih pake studi kasus [database notes](../../tutorial/single/database/1-database-notes.md) kemarin, kalo misalnya data notes tersebut dihapus secara real, nanti data di table `note_logs` gimana? Kan table_note_logs bergantung sama ID dari `notes`. Karena kita pake aturan foreign key, tentu hal ini bakalan bikin error dan dilarang database kalo dihapus notesnya, tapi... nih tapi, kalo misalnya sengaja dimatiin pengecekan foreign key-nya gimana? Tentu data di table notes bisa dihapus.

Hal ini bakalan bikin inkonsistensi data, makanya kalo ada data yang bergantung sama data tersebut, data utamanya gak boleh dihapus.

Kalo mau hapus data di table `notes`, cuma boleh soft delete, karena `note_logs` bergantung sama notes.

> Tapi kalo emang beneran mau dilenyapin gimana bang?

Hapus dulu data di `note_logs` yang bergantung sama ID notes yang mau dihapus, baru di table `notes` dihapus.

## Kasus soft delete biasa dipake dimana bang?

Dimana aja yang membutuhkan data untuk tetep bisa diperiksa, umumnya sih pada kasus-kasus yang membutuhkan fungsi restore, atau kasus yang kebijakan bisnisnya dimana data tersebut harus dipertahankan karena ada kebutuhan sama *data analytics*.

> Berarti data transaksi gak boleh dihapus ya, bang?

Binggo 😉! Karena data transaksi ini akan jadi patokan data kemana-mana, kalo kalian dapet pengajar yang bagus pas kuliah, pasti ngajarin betapa pentingnya soft delete.

## Bentuk soft delete itu gimana aja bang?

Sebenernya bisa banyak cara, tapi umumnya, dibagi dua:

- text based
- datetime based

### Text based

Jenis soft delete ini umumnya ngedepanin pake kolom bernama `status` atau `is_active`. Nah kolom ini biasanya akan ngisi nilai tergantung yang dibuat sama developernya.

- Kalo pake kolom status bisa `Y` atau `N`, `1` atau `0` dan tipenya biasanya char atau varchar.
- Kalo pake kolom is_active bisa `true` atau `false` yang pake tipe boolean.

### Datetime based

Jenis soft delete ini umumnya ngedepanin pake kolom datetime dengan nama `deleted_at` atau misal `archived_at`. Jadi ada teks `_at` nya dibelakang yang mana nandain kalo diartiin "dihapus pada" atau "disimpan pada".

Nah kalo pake kolom ini kita langsung ngisi aja tanggal dari kolom tersebut, bisa pake current millis atau pake date time format `Y-m-d H:i:s`.

## Paling bagus pake tipe apa bang?

Gak ada yang paling bagus, sesuain aja sama kebutuhannya. Kalo misalnya perlu untuk deteksi kapan dihapus secara exact tanggalnya, pake datetime based, kalo butuh multiple condition silahkan pake text based.

Tapi in my honest opinion, better pake datetime, karena bisa spesifik nandain kapan action itu dilakukan. Cuma kekurangannya ya actionnya cuma satu, yaitu sesuai nama kolom. Maka makesure kalau ada multiple conditions pake text based, **tapi khusus menghapus, pake datetime based**. Itu sih saran saya aja.

## Berarti sebenernya data kita selama ini gak ilang ya?

Kurang lebih sih gitu, sebenernya data kalian disimpan rapat-rapat oleh para tech company, dan ini fakta. Data kalian dipake buat bahan analytics mereka supaya mereka bisa ambil keputusan terkait produk mereka.

> Bentar bang, berarti data tweets saya kalo saya hapus gimana? Data pesan yang saya kirim di Whatsapp walaupun saya hapus, gak bener-bener ilang dong di pihak whatsappnya?

Cuma satu emoji yang bisa saya gambarin, yaitu 😆.

You know what I mean.

So, pikir-pikir lagi ya kalo mau mengirimkan sesuatu, apalagi gambar senonoh/vulgar.

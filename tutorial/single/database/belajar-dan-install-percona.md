<img src="assets/belajar-dan-install-percona/header.png" style="border-radius:10px;" />

<br/>

by [@perogeremmer](https://twitter.com/perogeremmer)

## Belajar dan Install Percona

Sebelum kamu lanjut untuk membaca ini, saya mau bilang bahwa tutorial ini bukan untuk **pemula**.

Sekali lagi, tutorial ini bukan untuk **pemula**.

Tutorial ini ditujukan untuk mereka yang sudah belajar backend paling enggak satu tahun, kenapa? Harapannya adalah yang sudah belajar backend satu tahun sudah paham dengan istilah-istilah yang akan saya sebutkan.

Untuk memahami ini, paling nggak kamu udah harus terbiasa dengan hal-hal berikut:

- Docker
- Command Line (Linux khususnya)
- Sedikit pemahaman server
- Pemahaman HTTP / HTTPS
- Instalasi DB (MySQL)
- MySQL syntax admin (grant, create user)

Maka kalau kamu belum paham tapi tetep pengen maksa supaya baca, resiko anda tanggung sendiri hehehe.

## Percona itu apaan sih?

Percona sebenernya adalah software atau tools **open source** yang memungkinkan kita untuk melakukan **monitoring** terhadap performa database kita. Gak cuma performa database sebenernya, tapi juga performa OS tempat si Percona berjalan (please correct me if i'm wrong), tapi mostly tujuan utamanya adalah monitoring database.

> Kenapa database harus di-monitoring bang?

Supaya memahami apa yang menjadi masalah, misalnya:

- Performa terhadap query
- Query mana yang menyebabkan lemot
- Query apa yang kerja mulu
- Query apa yang jalannya lambat
- I/O (input/output) database itu sendiri

dan hal lainnya yang berkaitan dengan database yang kita punya.

Namanya aja monitoring, so pasti yang kita lakukan adalah memantau, tapi mantau disini konteksnya bukan seperti petugas yang kerjanya ngeliatin layar ya, tapi memahami bagaimana database kita berjalan. Kenapa? karena kita gak tau keadaan di dalamnya seperti apa, maka dari itu, penting untuk melakukan monitoring.

Misalnya gambar berikut

![Sample](assets/belajar-dan-install-percona/sample.png)

Bisa dilihat dari gambar berikut adalah contoh monitoring terhadap server yang saya install, saya bisa lihat versi database saya, kemudian berapa koneksi yang berjalan, dan hal lainnya yang memudahkan devops untuk paham keadaan servernya dan supaya tim backend itu sendiri bisa paham apa yang terjadi di database akibat dosa-dosa mereka membuat query atau bahkan struktur table yang kurang bijaksana 👿.

---

Mungkin kalo cuma ngomongin teori bakalan bingung ya, jadi pada intinya, di tutorial kali ini kita bakalan nyobain install percona DB-nya terlebih dahulu pada server. Untuk kali ini gue gak akan pake server local, tapi pake server beneran.

> Bang kalo mau install di local boleh?

Boleh banget lah, cuma gue sih biar gampang aja makanya gue pengen install di server gue langsung. Lagian gue males bersih-bersihin filenya kalo di local gue hehehe, tapi kalo kalian emang gak ada doku alias duit, yaudah gapapa install aja di local kalian.

> Ohiya bang yang terpenting, gratis gak sih? hehehe

Bayar lah, hari gini gratis?

Gak deng, karena ini `open source` maka biaya toolsnya gratis. Tapi tetep ya, kalian harus **bayar server** kalian, masa udah toolsnya gratis, servernya juga mau gratis???? Kurang ajar banget klean ini.

## Arsitektur

Sebelum kita lanjut untuk install, kita pahami dulu arsitektur yang akan kita bangun.

```mermaid
graph LR;
  A[Percona Server] --> B[Percona Client];
  B --> C[Your Database];
```

Jadi akan ada tiga aplikasi yang kita install:

1. Percona Server → Software Server Percona untuk monitoring
2. Percona Client → Software Client Percona untuk melihat hasil monitoring
3. Database MySQL 8.0 → Tempat nyimpen data, apalagi coba?

Sebenernya untuk nomor ketiga, kita ada dua opsi yaitu:

- Install MySQL 8.0 (Native)
- Install Percona MySQL 8.0 (Bawaan Percona)

Bedanya apa? Sebenernya Percona MySQL 8.0 ini bawaan dari core MySQL 8.0 juga, namun karena ya Percona yang bikin, udah pasti secara scalability bakalan di-tweak sama percona untuk menyesuaikan software mereka, karena MySQL itu sendiri adalah open source sehingga ya wajar aja kalo misalnya Percona bisa nge-tweak dan ngotak-ngatik kode dasar MySQL 8.0 supaya bisa match sama Percona itu sendiri.

Anyway jadi kesimpulannya bagusan MySQL 8.0 Native atau Percona MySQL 8.0?

Jawabannya, depends, kalo kita banyak mau bergantung sama percona itu sendiri dari segi scalability, terus misalnya at the end kita bakalan pake banyak service percona, ada baiknya install Percona MySQL 8.0, tapi kalo kita cuma butuh monitoringnya aja, ya gapapa kita pake MySQL 8.0 Native aja.

Nah untuk kasus kali ini kita bakalan pake MySQL 8.0 Native aja biar kesannya natural gitu loh.

> Bang Percona support MySQL 5.7 gak?

Jawabannya, support, cek aja [disini](https://docs.percona.com/percona-server/5.7/index.html).

## It's Time to Start

Yep udah saatnya kita mulai install.

Ohiya sebelum mulai pahami dulu requirement si percona, karena ini untuk monitoring, tentu aja resource yang dimakan pasti lebih banyak.

Paling enggak, server kita harus memiliki:

- RAM 2GB
- Disk free 1GB per-minggunya, karena percona akan ngelakuin retensi data per-30 hari.
- CPU-nya support SSE 4.2 (Jujur gue juga kurang paham sih hahaha).

Disini gue akan pake requirement server kaya gini:

- Ubuntu 20.04 LTS
- CPU 1
- RAM 2GB
- 60GB Disk

Nah untuk provider cloudnya gue pake .....

Ah berhubung kaga ada yang kerjasama sama gue, ya gue gak spill cloudnya pake apa xixixi. Ditunggu ya buat para provider cloud kalo mau kerjasama 🤣.

Pertama, install dulu MySQL 8.0.

```bash
sudo apt install mysql-server

sudo systemctl start mysql.service
```

Kedua, pastikan kalian sudah bisa masuk ke database kalian.

```plain
ubuntu@ip-172-26-13-205:~$ mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 18
Server version: 8.0.33-0ubuntu0.20.04.2 (Ubuntu)

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

Ketiga, install docker kalo belom ada.

```bash
sudo apt install docker.io
```

Keempat, install nginx jangan lupa.

```bash
sudo apt install nginx
```

## Install Percona Server

Biar docker gak ribet pake sudo-sudo, kita tambahin dulu nih ke sudo group

```bash
sudo usermod -aG docker $USER
```

Kemudian kita pull terlebih dahulu dockernya.

```bash
docker pull percona/pmm-server:2
```

Kemudian kita buat volume datanya

```bash
docker volume create pmm-data
```

Then, kita jalankan server percona di docker.

```bash
docker run --detach --restart always \
--publish 443:443 \
-v pmm-data:/srv \
--name pmm-server \
percona/pmm-server:2
```

Terakhir, kita ganti password default adminnya dengan password yang baru

```bash
docker exec -t pmm-server change-admin-password <new_password>
```

hapus `<new_password>` ganti dengan password baru, misalnya `admin123`

Jadinya seperti ini:

```bash
docker exec -t pmm-server change-admin-password admin123
```

Selesai, sekarang kita siap untuk nginstall client app-nya.

## Install Percona Client

Ada dua teknik untuk menginstall ini:

1. [Docker](https://docs.percona.com/percona-monitoring-and-management/setting-up/client/index.html#docker)
2. Package Manager

Untuk kali ini, saya bakalan ajarin pake package managernya.

Download terlebih dahulu debian packagenya.

```bash
wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb
```

Install percona client-nya.

```bash
sudo apt install -y pmm2-client
```

Kemudian cek sudah terinstall atau belum

```bash
pmm-admin --version
```

Terakhir, kita config sesuai dengan IP kita

```bash
sudo pmm-admin config --server-insecure-tls --server-url=https://admin:<password kalian>@ip-address-server-kalian:443
```

Misalnya:

```bash
sudo pmm-admin config --server-insecure-tls --server-url=https://admin:123456@127.0.0.1:443
```

Kalo berhasil ntar tulisannya begini harusnya:

```plain
Checking local pmm-agent status...
pmm-agent is running.
Registering pmm-agent on PMM Server...
Registered.
Configuration file /usr/local/percona/pmm2/config/pmm-agent.yaml updated.
Reloading pmm-agent configuration...
Configuration reloaded.
Checking local pmm-agent status...
pmm-agent is running.
```

Kalo sudah kita bisa cek dengan pergi ke IP server kita, kalo berhasil muncul halaman kaya gini, berarti sudah jalan:

Misalnya IP server local saya `192.168.1.103` berarti saya pergi ke <https://192.168.1.103>, nanti akan ada popup peringatan https, di-skip aja, karena kita tau bahwa ini server yang kita kenal kok.

![Login page](assets/belajar-dan-install-percona/login-page.png)

Coba login dengan username admin dan password yang telah kita set, kemudian login, jika berhasil nanti muncul seperti ini:

![Home Tour](assets/belajar-dan-install-percona/home-tour.png)

![Home](assets/belajar-dan-install-percona/home.png)

Oke kalo sudah bisa, selamat, sekarang masuk ke tahap akhir, yaitu menghubungkan Percona Server dengan Database kalian.

## Connecting Percona with Database

Nah kita perlu akun database untuk Percona, pertama login ke MySQL kalian dengan role access root kemudian buat user baru. Dokumentasi lengkap ada [disini](https://docs.percona.com/percona-monitoring-and-management/setting-up/client/mysql.html#before-you-start).

MySQL 8.0

```sql
CREATE USER 'pmm'@'127.0.0.1' IDENTIFIED BY 'password-baru' WITH MAX_USER_CONNECTIONS 10;
GRANT SELECT, PROCESS, REPLICATION CLIENT, RELOAD, BACKUP_ADMIN ON *.* TO 'pmm'@'127.0.0.1';
```

MySQL 5.7

```sql
CREATE USER 'pmm'@'127.0.0.1' IDENTIFIED BY 'password-baru' WITH MAX_USER_CONNECTIONS 10;
GRANT SELECT, PROCESS, REPLICATION CLIENT, RELOAD ON *.* TO 'pmm'@'127.0.0.1';
```

Hasilnya:

```plain
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 21
Server version: 8.0.33-0ubuntu0.20.04.2 (Ubuntu)

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CREATE USER 'pmm'@'127.0.0.1' IDENTIFIED BY 'password-baru' WITH MAX_USER_CONNECTIONS 10;
Query OK, 0 rows affected (0.11 sec)

mysql> GRANT SELECT, PROCESS, REPLICATION CLIENT, RELOAD, BACKUP_ADMIN ON *.* TO 'pmm'@'127.0.0.1';
Query OK, 0 rows affected (0.00 sec)

mysql> 
```

Keluar dari MySQL dan masukkan perintah berikut untuk menghubungkan Percona Server dengan DB

```bash
sudo pmm-admin add mysql --username=pmm --password=password-baru --query-source=perfschema
```

Hasilnya akan seperti ini:

```bash
MySQL Service added.
Service ID  : /service_id/0b537b6a-35e4-442d-b296-960582242413
Service name: ip-172-26-13-205-mysql

Table statistics collection enabled (the limit is 1000, the actual table count is 328).
```

Tunggu beberapa saat hingga Percona Server berhasil mengumpulkan berbagai data kita.

Kalau misalnya ngerasa ada yang aneh atau gak berubah, bisa coba re-loggin dan pergi ke tab MySQL / Overview, hasilnya akan seperti ini:

![](assets/belajar-dan-install-percona/result.png)

Wew, keren ya?

## Monitoring Query

Kita bisa monitoring query pada menu QAN (Query Analytics) di bagian kiri dan hasilnya akan seperti ini:

![Query Analytics Page](assets/belajar-dan-install-percona/query-analytics.png)

Maka dosa-dosa kita sebagai backend akan kelihatan disini ngeliat querynya hahaha.

Gimana cara kita melihat query sample yang lebih asli?

Oke, pergi ke MySQL kalian lagi, terus bikin database namanya belajar.

```sql
CREATE DATABASE belajar;
USE belajar;
```

Buat table baru:

```sql
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  name VARCHAR(230) NOT NULL,
  email VARCHAR(230) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Masukkan 100 data baru:

```sql
INSERT INTO users (name, email)
SELECT CONCAT('User', t.id), CONCAT('user', t.id, '@example.com')
FROM (
  SELECT (t1.num * 10 + t2.num) + 1 AS id
  FROM (SELECT 0 AS num UNION SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5 UNION SELECT 6 UNION SELECT 7 UNION SELECT 8 UNION SELECT 9) AS t1
  CROSS JOIN (SELECT 0 AS num UNION SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 UNION SELECT 5 UNION SELECT 6 UNION SELECT 7 UNION SELECT 8 UNION SELECT 9) AS t2
) AS t
LIMIT 100;
```

Sekarang lihat, query kita sudah terdeteksi Percona:

![Query List](assets/belajar-dan-install-percona/query-list.png)

Tunggu beberapa saat lagi, sambil tekan refresh pada pojok kanan atas, lakukan search INSERT, kita akan melihat query yang kita lakukan untuk meng-insert 100 data.

![Query List Insert](assets/belajar-dan-install-percona/query-list-insert.png)

Gimana? Gampang kan ngelakuinnya? 😎

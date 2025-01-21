# 2 - Servers and Clients

- [2 - Servers and Clients](#2---servers-and-clients)
  - [Koneksi](#koneksi)
  - [MongoDB Server](#mongodb-server)
  - [MongoDB Clients](#mongodb-clients)
  - [Interaksi Client-Server](#interaksi-client-server)
  - [Keamanan](#keamanan)
  - [Skalabilitas](#skalabilitas)

## Koneksi

Dalam mengakses antara server dan klien, MongoDB secara garis besar sama seperti RDBMS. Perhatikan graph berikut:

```mermaid
graph TD
    A[Clients] -->|Queries/Operations| D
    D[mongod Process] -->|Read/Write| E[Database Storage]
    D -.->|Can be configured as| F[Replica Set / Sharding]
```

## MongoDB Server

Ini adalah inti dari sistem MongoDB, yang menjalankan database engine. Server bertanggung jawab untuk menyimpan, mengambil, dan mengelola data. Biasanya berjalan sebagai proses daemon (mongod) di sistem operasi. Dapat dikonfigurasi untuk berjalan sebagai standalone, replica set, atau sharded cluster.

## MongoDB Clients

Ini adalah aplikasi atau tools yang berinteraksi dengan MongoDB server.

- MongoDB Shell (mongo): Command-line interface untuk berinteraksi dengan database. Biasanya diinstall pada client untuk konfigurasi dan interaksi dasar.
- Driver MongoDB: Library untuk berbagai bahasa pemrograman (seperti Python, Java, Node.js) yang memungkinkan aplikasi berinteraksi dengan MongoDB.
- GUI Tools: Seperti MongoDB Compass untuk manajemen visual database.
- Aplikasi yang Anda kembangkan: Menggunakan driver MongoDB untuk berkomunikasi dengan server.

## Interaksi Client-Server

Clients mengirim permintaan (queries, updates, etc.) ke server. Server memproses permintaan tersebut dan mengembalikan hasilnya ke client. Komunikasi biasanya menggunakan protokol wire yang khusus didesain untuk MongoDB.

## Keamanan

Autentikasi dan otorisasi diterapkan di sisi server.
Clients perlu menyediakan kredensial yang sesuai untuk mengakses database.

## Skalabilitas

MongoDB dapat di-scale secara horizontal dengan menambahkan lebih banyak server (sharding). Clients dapat terhubung ke multiple servers dalam konfigurasi cluster.

Berikut gambaran cluster skalabilitas dalam mongoDB.

```mermaid
graph TD
    C[Client] --> MR[MongoDB Router]
    MR -->|Read Write| P[Primary]
    MR -->|Read| S1[Secondary 1]
    MR -->|Read| S2[Secondary 2]
    P -->|Replication| S1
    P -->|Replication| S2
    S1 -.->|Sync| P
    S2 -.->|Sync| P
```

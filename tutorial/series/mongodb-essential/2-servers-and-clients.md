# 2 - Servers and Clients

## Koneksi

Dalam mengakses antara server dan klien, MongoDB secara garis besar sama seperti RDBMS. Perhatikan graph berikut:

```mermaid
graph TD
    subgraph Clients
        A[MongoDB Shell]
        B[Application with MongoDB Driver]
        C[MongoDB Compass GUI]
    end

    subgraph "MongoDB Server"
        D[mongod Process]
        E[Database Storage]
    end

    A -->|Queries/Commands| D
    B -->|CRUD Operations| D
    C -->|Management/Queries| D
    D -->|Read/Write| E

    subgraph "Distributed Setup"
        F[Replica Set]
        G[Sharded Cluster]
    end

    D -.->|Can be configured as| F
    D -.->|Can be configured as| G
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
    subgraph "Clients"
        C1[Client 1]
        C2[Client 2]
        C3[Client 3]
    end

    subgraph "MongoDB Cluster"
        subgraph "Shard 1"
            S1[Primary]
            S1R1[Secondary]
            S1R2[Secondary]
            S1 --- S1R1
            S1 --- S1R2
        end

        subgraph "Shard 2"
            S2[Primary]
            S2R1[Secondary]
            S2R2[Secondary]
            S2 --- S2R1
            S2 --- S2R2
        end

        subgraph "Config Servers"
            CS1[Config Server 1]
            CS2[Config Server 2]
            CS3[Config Server 3]
            CS1 --- CS2
            CS2 --- CS3
            CS3 --- CS1
        end

        MR1[Mongos Router 1]
        MR2[Mongos Router 2]

        MR1 --> S1
        MR1 --> S2
        MR2 --> S1
        MR2 --> S2

        MR1 -.-> CS1
        MR2 -.-> CS1
    end

    C1 --> MR1
    C2 --> MR1
    C3 --> MR2
```

# 9 - Replication

- [9 - Replication](#9---replication)
  - [Overview](#overview)
  - [Alur Replikasi di MongoDB](#alur-replikasi-di-mongodb)
    - [Kriteria Pemilihan Primary Baru](#kriteria-pemilihan-primary-baru)
    - [Proses Pemilihan](#proses-pemilihan)
    - [Operasi Baca dan Tulis pada Primary Baru](#operasi-baca-dan-tulis-pada-primary-baru)
  - [Perbandingan Replikasi MongoDB dan MySQL](#perbandingan-replikasi-mongodb-dan-mysql)

## Overview

Replication (Replika) dalam konteks database adalah salinan data yang identik dengan data asli, yang disimpan di server terpisah. Tujuan utama replikasi adalah:

1. Meningkatkan ketersediaan data (high availability)
2. Meningkatkan toleransi terhadap kegagalan (fault tolerance)
3. Meningkatkan kinerja dengan mendistribusikan beban baca (read scaling)
4. Mendukung disaster recovery

Tidak memungkinkan untuk terhubung ke salah satu shard cluster menggunakan **MongoDB Atlas Free Tier**, karena fitur sharding tidak tersedia pada tingkat layanan ini. Agar dapat digunakan maka perlu meningkatkan ke tier berbayar yang mendukung fitur ini.

## Alur Replikasi di MongoDB

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg">
  <style>
    .small { font: italic 13px sans-serif; }
    .heavy { font: bold 30px sans-serif; }
    .label { font: normal 16px sans-serif; fill: #333; }
    .small-label { font: normal 14px sans-serif; fill: #666; }
  </style>

  <!-- Primary Node -->
  <rect x="100" y="50" width="200" height="300" rx="10" ry="10" fill="#4DB33D" />
  <text x="200" y="90" text-anchor="middle" class="heavy" fill="white">Primary</text>
  
  <!-- Oplog in Primary -->
  <rect x="120" y="120" width="160" height="100" rx="5" ry="5" fill="white" stroke="#333" />
  <text x="200" y="145" text-anchor="middle" class="label">Oplog</text>
  <line x1="130" y1="160" x2="270" y2="160" stroke="#333" stroke-width="1" />
  <line x1="130" y1="180" x2="270" y2="180" stroke="#333" stroke-width="1" />
  <line x1="130" y1="200" x2="270" y2="200" stroke="#333" stroke-width="1" />

  <!-- Secondary Node -->
  <rect x="500" y="50" width="200" height="300" rx="10" ry="10" fill="#589636" />
  <text x="600" y="90" text-anchor="middle" class="heavy" fill="white">Secondary</text>

  <!-- Oplog in Secondary -->
  <rect x="520" y="120" width="160" height="100" rx="5" ry="5" fill="white" stroke="#333" />
  <text x="600" y="145" text-anchor="middle" class="label">Oplog Copy</text>
  <line x1="530" y1="160" x2="670" y2="160" stroke="#333" stroke-width="1" />
  <line x1="530" y1="180" x2="670" y2="180" stroke="#333" stroke-width="1" />
  <line x1="530" y1="200" x2="670" y2="200" stroke="#333" stroke-width="1" />

  <!-- Replication Arrow -->
  <line x1="300" y1="170" x2="480" y2="170" stroke="#333" stroke-width="2" marker-end="url(#arrowhead)" />
  <text x="390" y="155" text-anchor="middle" class="small-label">Oplog Sync</text>

  <!-- Heartbeat Arrows -->
  <line x1="300" y1="280" x2="480" y2="280" stroke="#666" stroke-width="2" stroke-dasharray="5,5" marker-end="url(#arrowhead)" />
  <line x1="480" y1="300" x2="300" y2="300" stroke="#666" stroke-width="2" stroke-dasharray="5,5" marker-end="url(#arrowhead)" />
  <text x="390" y="270" text-anchor="middle" class="small-label">Heartbeats</text>

  <!-- Arrow Marker -->
  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="0" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#333" />
    </marker>
  </defs>
</svg>

MongoDB menggunakan model replikasi yang disebut Replica Set. Berikut adalah alur replikasi di MongoDB:

1. **Inisialisasi Replica Set**:

   - Satu node diinisialisasi sebagai Primary, sisanya sebagai Secondary.

2. **Operasi Tulis**:

   - Klien mengirim operasi tulis ke node Primary.
   - Primary mencatat operasi dalam oplog (operations log).
   - Primary menerapkan perubahan ke datanya sendiri.

3. **Replikasi ke Secondary**:

   - Node Secondary secara asinkron menyalin oplog dari Primary.
   - Secondary menerapkan operasi dari oplog ke data mereka.

4. **Sinkronisasi Berkelanjutan**:

   - Secondary terus memantau oplog Primary untuk perubahan baru.
   - Jika tertinggal, Secondary akan melakukan sinkronisasi penuh jika diperlukan.

5. **Heartbeats dan Pemilihan**:

   - Semua node bertukar heartbeat secara teratur.
   - Jika Primary tidak tersedia, Secondary akan memilih Primary baru.

6. **Pembacaan dari Secondary** (opsional):
   - Klien dapat dikonfigurasi untuk membaca dari Secondary untuk load balancing.

### Kriteria Pemilihan Primary Baru

Ketika primary node dalam MongoDB replica set tidak tersedia, proses pemilihan primary baru (election) terjadi dengan kriteria sebagai berikut:

1. **Eligibility**:

   - Hanya secondary node yang eligible dapat menjadi primary.
   - Node harus memiliki `{priority: 1}` atau lebih tinggi.

2. **Oplog Currency**:

   - Node dengan oplog paling up-to-date memiliki peluang lebih besar terpilih.

3. **Connectivity**:

   - Node harus dapat berkomunikasi dengan mayoritas anggota replica set.

4. **Priority Setting**:

   - Node dengan priority setting lebih tinggi akan diutamakan.

5. **Votes**:

   - Node harus menerima mayoritas suara dari anggota replica set yang memiliki hak suara.

6. **Tiebreaker**:
   - Jika terjadi seri, node dengan optime (timestamp operasi terakhir) tertinggi akan menang.

### Proses Pemilihan

1. Inisiasi pemilihan ketika primary tidak merespon heartbeat.
2. Eligible secondary mempromosikan diri sebagai kandidat.
3. Kandidat meminta suara dari anggota lain.
4. Anggota memberikan suara berdasarkan kriteria di atas.
5. Kandidat dengan mayoritas suara menjadi primary baru.

### Operasi Baca dan Tulis pada Primary Baru

Ketika sebuah secondary node terpilih menjadi primary baru:

1. **Transisi Peran**:

   - Node mengubah statusnya dari secondary menjadi primary.
   - Proses ini biasanya berlangsung sangat cepat (dalam hitungan detik).

2. **Kemampuan Operasional**:

   - Segera setelah menjadi primary, node dapat melakukan operasi baca DAN tulis.
   - Tidak ada "warm-up period" – operasi baca/tulis dapat langsung dilakukan.

3. **Konsistensi**:

   - Primary baru menjamin bahwa ia memiliki data paling up-to-date sebelum menerima operasi tulis.

4. **Penyesuaian Klien**:

   - Driver MongoDB yang kompatibel akan otomatis mendeteksi primary baru dan mengarahkan operasi tulis ke sana.

5. **Read Preference**:
   - Operasi baca tetap dapat dikonfigurasi untuk membaca dari secondary jika diinginkan.

<br/>
<br/>
<br/>

## Perbandingan Replikasi MongoDB dan MySQL

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg">
  <style>
    .heavy { font: bold 22px sans-serif; }
    .label { font: normal 16px sans-serif; fill: #333; }
    .small-label { font: normal 14px sans-serif; fill: #666; }
  </style>

  <!-- MongoDB Side -->
  <rect x="450" y="50" width="300" height="300" rx="10" ry="10" fill="#4DB33D" />
  <text x="600" y="85" text-anchor="middle" class="heavy" fill="white">MongoDB</text>

  <!-- Primary in MongoDB -->
  <rect x="470" y="100" width="260" height="100" rx="5" ry="5" fill="white" stroke="#333" />
  <text x="600" y="130" text-anchor="middle" class="label">Primary</text>
  <rect x="480" y="150" width="240" height="30" rx="5" ry="5" fill="#FFD700" />
  <text x="600" y="170" text-anchor="middle" class="small-label">Oplog</text>

  <!-- Secondary in MongoDB -->
  <rect x="470" y="230" width="260" height="100" rx="5" ry="5" fill="white" stroke="#333" />
  <text x="600" y="260" text-anchor="middle" class="label">Secondary</text>
  <rect x="480" y="280" width="240" height="30" rx="5" ry="5" fill="#87CEFA" />
  <text x="600" y="300" text-anchor="middle" class="small-label">Oplog Sync</text>

  <!-- Replication Arrows -->
  <line x1="200" y1="200" x2="200" y2="230" stroke="#333" stroke-width="2" marker-end="url(#arrowhead)" />
  <line x1="600" y1="200" x2="600" y2="230" stroke="#333" stroke-width="2" marker-end="url(#arrowhead)" />

  <!-- MySQL Side -->
  <rect x="50" y="50" width="300" height="300" rx="10" ry="10" fill="#00758F" />
  <text x="200" y="85" text-anchor="middle" class="heavy" fill="white">MySQL / RDS</text>
  
  <!-- Master in MySQL -->
  <rect x="70" y="100" width="260" height="100" rx="5" ry="5" fill="white" stroke="#333" />
  <text x="200" y="130" text-anchor="middle" class="label">Master</text>
  <rect x="80" y="150" width="240" height="30" rx="5" ry="5" fill="#FFD700" />
  <text x="200" y="170" text-anchor="middle" class="small-label">Binary Log</text>

  <!-- Slave in MySQL -->
  <rect x="70" y="230" width="260" height="100" rx="5" ry="5" fill="white" stroke="#333" />
  <text x="200" y="260" text-anchor="middle" class="label">Slave</text>
  <rect x="80" y="280" width="240" height="30" rx="5" ry="5" fill="#87CEFA" />
  <text x="200" y="300" text-anchor="middle" class="small-label">Binlog Reader</text>

</svg>

| Aspek             | MongoDB                                         | MySQL                                                           |
| ----------------- | ----------------------------------------------- | --------------------------------------------------------------- |
| Model Replikasi   | Replica Set                                     | Master-Slave atau Group Replication                             |
| Log Replikasi     | Oplog (Operations Log)                          | Binary Log (Binlog)                                             |
| Pemilihan Leader  | Otomatis (dalam Replica Set)                    | Manual (dalam Master-Slave), Otomatis (dalam Group Replication) |
| Konsistensi       | Eventually Consistent (default)                 | Strongly Consistent (default)                                   |
| Skalabilitas Baca | Built-in dengan Secondary Reads                 | Memerlukan konfigurasi tambahan                                 |
| Format Log        | BSON (Binary JSON)                              | Row-based, Statement-based, atau Mixed                          |
| Topologi          | Biasanya odd-numbered set (e.g., 3, 5, 7 nodes) | Flexible (Master-Slave atau Multi-Master)                       |
| Failover          | Otomatis dalam Replica Set                      | Manual dalam Master-Slave, Otomatis dalam Group Replication     |
| Sharding          | Native support                                  | Memerlukan konfigurasi tambahan (MySQL Cluster)                 |
| Replikasi Partial | Tidak didukung                                  | Didukung (dapat mereplikasi tabel tertentu)                     |

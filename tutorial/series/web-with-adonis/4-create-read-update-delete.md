<br/>

by [@perogeremmer](https://twitter.com/perogeremmer)

## CRUD (Create, Read, Update, Delete)

Fitur CRUD adalah salah satu fitur paling basic di dalam pembelajaran pemrograman. Fitur CRUD merupakan aksi dasar dalam membuat program, karena hampir semua program pasti memiliki fitur CRUD.

Perbedaan paling dasar pada CRUD di setiap program adalah kompleksitas dari proses akhir CRUD. Untuk pembelajaran, fitur CRUD paling awal biasanya hanya melibatkan sedikit proses yang mana langsung disimpan perubahannya menuju ke database.

Pada kasus kali ini, kita akan belajar CRUD todo-list dengan template yang kemarin kita gunakan.

## Migration

Pertama kita perlu membuat migration terlebih dahulu. Migration adalah file dimana kita dapat melakukan perubahan data pada database sehingga kita tidak perlu melakukan perubahan secara langsung pada database.

Hal ini penting dilakukan mengingat bahwa menyentuh database secara langsung dapat saja melakukan hal-hal yang malah nantinya merusak tabel atau data pada database itu sendiri.

Pertama, pastikan kalian sudah mengaktifkan atau menyalakan MySQL baik menggunakan PHPMyAdmin (sangat disarankan bagi pemula), atau kamu juga dapat menggunakan docker.

Kedua, pastikan kalian sudah menyiapkan databasenya, seharusnya sudah karena di tutorial pertama kita sudah harus menyiapkan databasenya.

Ketiga, silahkan masukkan perintah berikut untuk membuat migration.

```bash
node ace make:migration todo

# Hasil
# hudya@perogeremmer-pc:~/code/perogeremmer/hello-world$ node ace make:migration todo
# DONE:    create database/migrations/1723422869961_create_todos_table.ts
```

Menulis migration pada adonis juga memiliki grammar tersendiri, hal ini sama dengan Laravel yang memiliki Migration. Untuk melihat dokumentasi lengkapnya kamu bisa mengunjungi [adonis lucid disini](https://lucid.adonisjs.com/docs/migrations).

Kita akan membuat struktur yang sederhana yaitu:

- judul todo
- deskripsi
- status todo
- waktu dibuat
- waktu dihapus

Sehingga, file migration todo yang berada pada folder `database/migrations` akan menjadi seperti ini:

```typescript
import { BaseSchema } from '@adonisjs/lucid/schema'

export default class extends BaseSchema {
  protected tableName = 'todos'

  async up() {
    this.schema.createTable(this.tableName, (table) => {
      table.increments('id')
      table.string('title').notNullable()
      table.text('description').nullable()
      table.string('status', 30)
      table.timestamp('created_at')
      table.timestamp('updated_at')
      table.datetime('deleted_at').nullable()
    })
  }

  async down() {
    this.schema.dropTable(this.tableName)
  }
}
```

Secara default library migration zaman sekarang sudah menyiapkan `created_at` dan `updated_at` secara default untuk migrationnya. Hal ini dikarenakan kedua kolom ini sangat penting untuk mendeteksi kapan data dibuat dan kapan data diperbarui.

Sekarang kita bisa menguji coba terlebih dahulu apakah struktur ini berjalan atau tidak. Masukkan perintah berikut:

```bash
node ace migration:run

# Hasil

# [ info ] Upgrading migrations version from "1" to "2"
# ❯ migrated database/migrations/1723215580268_create_users_table
# ❯ migrated database/migrations/1723422869961_create_todos_table
# Migrated in 333 ms
```

Dapat kita lihat semua migrations berjalan dan kita bisa mengeceknya ke database, apabila kamu menggunakan PHPMyAdmin silahkan buka halamannya.

```plain
mysql> show tables;
+------------------------+
| Tables_in_adonis       |
+------------------------+
| adonis_schema          |
| adonis_schema_versions |
| todos                  |
| users                  |
+------------------------+
4 rows in set (0.00 sec)

mysql> show columns from todos;
+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| id          | int unsigned | NO   | PRI | NULL    | auto_increment |
| title       | varchar(255) | NO   |     | NULL    |                |
| description | text         | YES  |     | NULL    |                |
| status      | varchar(30)  | YES  |     | NULL    |                |
| created_at  | timestamp    | YES  |     | NULL    |                |
| updated_at  | timestamp    | YES  |     | NULL    |                |
| deleted_at  | datetime     | YES  |     | NULL    |                |
+-------------+--------------+------+-----+---------+----------------+
7 rows in set (0.00 sec)
```

> [!NOTE]
> Kelebihan dari migration itu sendiri adalah developer bisa melakukan rollback (mundur ke belakang), apabila terjadi sesuatu yang tidak diinginkan pada struktur database, hal ini dapat dilakukan di level development karena bisa saja perubahannya seperti menghapus kolom, maupun menghilangkan atribut.

## Seeder

Setelah membuat tabel, tentu tabel tersebut masih berisi data yang kosong. Kelebihan adonis JS adalah kita dapat membuat data seeder, artinya seperti memberikan biji ke dalam pot yang akan tumbuh.

Seeder ini merupakan fitur penting dalam pengembangan aplikasi, karena apabila sebuah proyek dilempar ke tim atau developer lain, developer tersebut dapat melihat seperti apa data awal (dasar) pada saat proyek dibangun.

Untuk membuatnya tidak sulit, cukup masukkan perintah:

```bash
node ace make:seeder todo

# Hasil
# DONE:    create database/seeders/todo_seeder.ts
```

Sekarang ubah `todo_seeder.ts` dengan kode berikut:

```ts
import db from '@adonisjs/lucid/services/db'
import { BaseSeeder } from '@adonisjs/lucid/seeders'

export default class extends BaseSeeder {
  async run() {

    let i = 0;
    while (i < 10) {
      await db
        .table('todos')
        .insert({
          "title": `Judul Todo ke-${i}`,
          "description": `Deskripsi Todo ke-${i}`,
          "status": "TODO",
          "created_at": new Date(),
          "updated_at": new Date()
        })
      i++;
    }
  }
}
```

Berdasarkan kode di atas, kita akan membuat sepuluh data baru pada table `todos` dengan judul, deskripsi dan status dasar.

Kode di atas menggunakan library DB dari lucid dimana kita tidak perlu membuat model untuk memasukannya ke DB, hal ini tentu memudahkan kita dalam memanipulasi data yang sifatnya seeding atau data awal.

Setelah merubah isi kode, jalankan dengan menuliskan perintah berikut:

```bash
node ace db:seed

# Hasil
# ❯ completed database/seeders/todo_seeder
```

<br />

Sekarang apabila kamu lihat ke database kamu akan melihat data tersebut:

```plain
mysql> select * from todos;
+----+-----------------+---------------------+--------+---------------------+---------------------+------------+
| id | title           | description         | status | created_at          | updated_at          | deleted_at |
+----+-----------------+---------------------+--------+---------------------+---------------------+------------+
|  1 | Judul Todo ke-0 | Deskripsi Todo ke-0 | TODO   | 2024-08-12 02:44:37 | 2024-08-12 02:44:37 | NULL       |
|  2 | Judul Todo ke-1 | Deskripsi Todo ke-1 | TODO   | 2024-08-12 02:44:37 | 2024-08-12 02:44:37 | NULL       |
|  3 | Judul Todo ke-2 | Deskripsi Todo ke-2 | TODO   | 2024-08-12 02:44:37 | 2024-08-12 02:44:37 | NULL       |
|  4 | Judul Todo ke-3 | Deskripsi Todo ke-3 | TODO   | 2024-08-12 02:44:37 | 2024-08-12 02:44:37 | NULL       |
|  5 | Judul Todo ke-4 | Deskripsi Todo ke-4 | TODO   | 2024-08-12 02:44:37 | 2024-08-12 02:44:37 | NULL       |
|  6 | Judul Todo ke-5 | Deskripsi Todo ke-5 | TODO   | 2024-08-12 02:44:38 | 2024-08-12 02:44:38 | NULL       |
|  7 | Judul Todo ke-6 | Deskripsi Todo ke-6 | TODO   | 2024-08-12 02:44:38 | 2024-08-12 02:44:38 | NULL       |
|  8 | Judul Todo ke-7 | Deskripsi Todo ke-7 | TODO   | 2024-08-12 02:44:38 | 2024-08-12 02:44:38 | NULL       |
|  9 | Judul Todo ke-8 | Deskripsi Todo ke-8 | TODO   | 2024-08-12 02:44:38 | 2024-08-12 02:44:38 | NULL       |
| 10 | Judul Todo ke-9 | Deskripsi Todo ke-9 | TODO   | 2024-08-12 02:44:38 | 2024-08-12 02:44:38 | NULL       |
+----+-----------------+---------------------+--------+---------------------+---------------------+------------+
10 rows in set (0.00 sec)
```

Viola, sepuluh data awal sudah berhasil kita tambahkan!

## Operasi Create, Read, Update, dan Delete

### Operasi Read

Setelah berhasil membuat data awal, kita akan coba untuk membuat CRUD yang menjadi tujuan utama. Sekarang hapus kedua file `seconds_controller.ts` dan `todos_controller.ts` karena kita sudah tidak membutuhkannya.

Alasan kita tidak membutuhkan `todos_controller.ts` adalah karena saya ingin memberitahu cara membuat controller dengan konsep restful dimana sudah tersedia banyak method bawaan, masukkan perintah berikut pada terminal:

```bash
node ace make:controller todo --resource

# Hasil
# DONE:    create app/controllers/todos_controller.ts
```

Sekarang kamu akan melihat isi file `todos_controller.ts` seperti ini:

```typescript
import type { HttpContext } from '@adonisjs/core/http'

export default class TodosController {
  /**
   * Display a list of resource
   */
  async index({}: HttpContext) {}

  /**
   * Display form to create a new record
   */
  async create({}: HttpContext) {}

  /**
   * Handle form submission for the create action
   */
  async store({ request }: HttpContext) {}

  /**
   * Show individual record
   */
  async show({ params }: HttpContext) {}

  /**
   * Edit individual record
   */
  async edit({ params }: HttpContext) {}

  /**
   * Handle form submission for the edit action
   */
  async update({ params, request }: HttpContext) {}

  /**
   * Delete record
   */
  async destroy({ params }: HttpContext) {}
}
```

Atribut `--resource` merupakan atribut yang dapat disisipkan pada saat membuat controller untuk menerapkan konsep RESTful yaitu `GET`, `POST`, `PUT`, dan `DELETE`.

Sebelum kita coba menampilkan data, kita perlu membuat model terlebih dahulu, masukkan perintah berikut:

```bash
node ace make:model todo

# Hasil
# DONE:    create app/models/todo.ts
```

Kemudian ubah isi file app/models/todo.ts dengan kode berikut:

```typescript
import { DateTime } from 'luxon'
import { BaseModel, column } from '@adonisjs/lucid/orm'

export default class Todo extends BaseModel {
  static table = 'todos'

  @column({ isPrimary: true })
  declare id: number

  @column()
  declare title: string

  @column()
  declare description: string

  @column()
  declare status: string

  @column.dateTime({ autoCreate: true })
  declare createdAt: DateTime

  @column.dateTime({ autoCreate: true, autoUpdate: true })
  declare updatedAt: DateTime

  @column.dateTime()
  declare deletedAt: DateTime
}
```

Kita memastikan semua kolom yang berada pada database ditulis di dalam model dimana Model Todo ini sendiri bertugas menjadi jembatan untuk mengelola data pada tabel todos.

Kita juga menambahkan `static table = 'todos'` karena `class Todo` mereprenstasikan table `todo`, sedangkan nama tabel kita adalah `todos` sehingga kita perlu menambahkan baris kode tersebut.

Sekarang kembali ke `todo controller` dan ubah kode pada fungsi index agar menjadi seperti ini:

```typescript
import type { HttpContext } from '@adonisjs/core/http'
import Todo from '#models/todo'

export default class TodosController {
  /**
   * Display a list of resource
   */
  async index({ view }: HttpContext) {
    const allTodos = await Todo.all()
    return view.render("pages/home", { todos: allTodos })
  }
```

Berdasarkan kode di atas, kita akan menampilkan seluruh data pada tabel `todos` dengan menggunakan model Todo. Memanggil model Todo tidaklah sulit, cukup import saja pada bagian paling atas lalu panggil dengan `await Todo.all()` untuk mengksekusi query dasar yaitu `SELECT * FROM todos`.

Data yang telah didapatkan disimpan dalam bentuk array di dalam variabel `allTodos` kemudian dioper ke views di dalam objek `todos`.

Sekarang pergi ke resources/views/pages/home.edge lalu ubah agar menjadi seperti ini:

```jinja
@base()
@slot("content")
<div class="container mt-5">
  <div class="row mb-4">
    <div class="col-12">
      <h5 class="mb-4">Judul Halaman</h5>

      <table class="table table-hover ">
        <thead>
          <tr>
            <th scope="col ">Title</th>
            <th scope="col ">Description</th>
            <th scope="col ">Created At</th>
            <th scope="col ">Status</th>
            <th scope="col ">Action</th>
          </tr>
        </thead>
        <tbody>
          @each(todo in todos)
          <tr>
            <td>{{ todo.title }}</td>
            <td>{{ todo.description }}</td>
            <td>{{ todo.createdAt }}</td>
            <td>
              <span class="badge badge-info text-white ">{{ todo.status }}</span>
            </td>
            <td>
              <div class="btn-group " role="group " aria-label="Basic example ">
                <a href="# " class="btn btn-primary text-white ">
                  <i class='bx bx-check'></i>
                </a>
                <a href="# " class="btn btn-info text-white ">
                  <i class='bx bx-pencil'></i>
                </a>
                <a href="# " class="btn btn-danger text-white ">
                  <i class='bx bx-trash'></i>
                </a>
              </div>
            </td>
          </tr>
          @end
        </tbody>
      </table>
    </div>
  </div>
</div>
@end
@end
```

Menggunakan sintaks `@each` sesuai dengan library [edge js](https://edgejs.dev/docs/loops), kita menampilkan semua data yang berada pada objek `todos` dari controller.

Terakhir, file `start/routes.ts` kita ubah terlebih dahulu agar bersih dari kode-kode sebelumnya:

```typescript
/*
|--------------------------------------------------------------------------
| Routes file
|--------------------------------------------------------------------------
|
| The routes file is used for defining the HTTP routes.
|
*/

import router from '@adonisjs/core/services/router'
import TodosController from '#controllers/todos_controller'

router.resource('/todo', TodosController)
```

Berbeda dengan kode sebelumnya, kita menggunakan fungsi `router.resource` karena fungsi ini otomatis mendeteksi fungsi-fungsi yang ada pada todo controller menuju url sebagai berikut:

- index: /todo `GET`
- create: /todo/create `GET`
- store: /todo `POST`
- show: /todo/{id} `GET`
- edit: /todo/{id}/edit `GET`
- update: /todo/{id} `PUT`
- delete: /todo/{id} `DELETE`

Sehingga secara teori kita tidak perlu repot-repot membuat URL tersebut.

Sekarang coba jalankan `npm run dev` lalu akses `localhost:3333/todo`.

![alt text](./assets/2.gif)

### Operasi Create

Pertama kita perlu membuat tampilan create terlebih dahulu, buat file baru bernama `create.edge` pada folder `resources/views/pages`, lalu masukkan kode berikut:

```jinja
@base()
@slot("content")
<div class="container mt-5">
  <div class="row mb-4">
    <div class="col-6">
      <h5 class="mb-4">Buat Todo Baru</h5>

      <form method="POST" action="{{ route('todo.store') }}">
        {{ csrfField() }}
        <div class="form-group">
          <label for="title">Title</label>
          <input type="text" class="form-control" id="title" name="title" placeholder="Place your title here...">
        </div>
        <div class="form-group">
          <label for="description">Description</label>
          <textarea class="form-control" id="description" rows="3"
            placeholder="Place your description here...." name="description"></textarea>
        </div>
        <div class="form-group">
          <button class="btn btn-md btn-info" type="submit">Submit</button>
        </div>
      </form>
    </div>
  </div>
</div>
@end
@end
```

URL Action pada kode di atas merujuk kepada class todo controller fungsi store, dimana URL akan diubah menjadi `/todo` dengan method `POST`.

Pada kode di atas juga ada fungsi `csrField()` dimana fungsi ini akan membuat kolom token csrf untuk mencegah serangan Cross Site Scripting (XSS Attack), inilah salah satu kelebihan adonis yang mana fitur ini juga ada pada laravel.

Sekarang ubah kode todo controller pada fungsi / method `create` dan `store` menjadi seperti ini:

```typescript
export default class TodosController {
  /**
   * Display a list of resource
   */
  async index({ view }: HttpContext) {
    const allTodos = await Todo.all()
    return view.render("pages/home", { todos: allTodos })
  }

  /**
   * Display form to create a new record
   */
  async create({ view }: HttpContext) {
    return view.render("pages/create")
  }

  /**
   * Handle form submission for the create action
   */
  async store({ request, response }: HttpContext) {
    const todo = new Todo()
    const body = await request.body()

    todo.title = body.title
    todo.description = body.description
    todo.status = "TODO"

    await todo.save()

    return response.redirect().toRoute('todo.index')
  }
```

Fungsi `create` akan menampilkan halaman `pages/create.edge` sedangkan fungsi `store` akan menjadi fungsi yang menuliskan data pada database melalui model Todo.

Pada fungsi `store` kita inisiasi model todo dan simpan semua nilai body pada variabel bernama body, kemudian kita assign masing-masing nilai pada objek todo dengan nilai dari body sesuai dengan name dari masing-masing atribut html tag yang kita kirimkan. Untuk status kita beri nilai default saja yaitu `TODO`.

Kemudian kita panggil fungsi `todo.save()` untuk mengeksekusi perintah `INSERT INTO` sesuai atribut yang kita set.

Terakhir kita arahkan responnya menuju rute fungsi `todo.index`, yang mana URLnya adalah `/todo`.

> [!NOTE]
> Apabila kamu bingung mengapa ada sintaks `await`, `await` adalah sintaks untuk membuat baris tersebut dieksekusi sebelum baris selanjutnya. Hal ini dilakukan karena Javascript pada umumnya bersifat asynchronous, sehingga baris selanjutnya bisa saja dieksekusi tanpa menunggu baris yang sedang berjalan. Dengan menggunakan sintaks `await` kita dapat memaksa program untuk menunggu proses pada baris tersebut hingga selesai sebelum melanjutkan proses ke baris selanjutnya.

Sekarang jalankan kembali dan lihat hasilnya, untuk mengakses halaman create kamu dapat mengunjungi `localhost:3333/create`.

![alt text](./assets/3.gif)

Data pun sudah pasti masuk ke database :smile:

```bash
mysql> select * from todos;
+----+-----------------+---------------------+--------+---------------------+---------------------+------------+
| id | title           | description         | status | created_at          | updated_at          | deleted_at |
+----+-----------------+---------------------+--------+---------------------+---------------------+------------+
|  1 | Judul Todo ke-0 | Deskripsi Todo ke-0 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
|  2 | Judul Todo ke-1 | Deskripsi Todo ke-1 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
|  3 | Judul Todo ke-2 | Deskripsi Todo ke-2 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
|  4 | Judul Todo ke-3 | Deskripsi Todo ke-3 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
|  5 | Judul Todo ke-4 | Deskripsi Todo ke-4 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
|  6 | Judul Todo ke-5 | Deskripsi Todo ke-5 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
|  7 | Judul Todo ke-6 | Deskripsi Todo ke-6 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
|  8 | Judul Todo ke-7 | Deskripsi Todo ke-7 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
|  9 | Judul Todo ke-8 | Deskripsi Todo ke-8 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
| 10 | Judul Todo ke-9 | Deskripsi Todo ke-9 | TODO   | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL       |
| 11 | Todo Test       | Test Todo           | TODO   | 2024-08-13 01:32:31 | 2024-08-13 01:32:31 | NULL       |
| 12 | Todo Baru 1     | Todo Baru-1         | TODO   | 2024-08-13 01:48:22 | 2024-08-13 01:48:22 | NULL       |
+----+-----------------+---------------------+--------+---------------------+---------------------+------------+
12 rows in set (0.00 sec)
```

### Operasi Update

Agar operasi Update dan Delete berhasil, kita perlu mengubah konfigurasi spoofing pada Adonis terlebih dahulu.

> The form method on an HTML form can only be set to GET, or POST, making it impossible to leverage restful HTTP methods.

Secara teori, form pada HTML hanya dapat diset `GET` atau `POST`. Method `PUT`, `PATCH`, dan `DELETE` merupakan method RESTful yang biasanya dilakukan dengan metode HTTP untuk API.

Namun, kita tetap dapat melakukannya dengan cara konfigurasi spoofing. Buka file `config/app.ts` lalu ganti nilai   `allowMethodSpoofing: false` menjadi  `allowMethodSpoofing: true`, perhatikan tanda komanya jangan sampai terhapus atau nanti akan ada error.

Sekarang kembali ke `todos_controller.ts` dan ubah kode pada fungsi `edit` dan `update`:

```typescript
async edit({ view, params }: HttpContext) {
  const data = await Todo.findBy('id', params.id)
  return view.render("pages/edit", { todo: data })
}

/**
 * Handle form submission for the edit action
 */
async update({ params, request, response }: HttpContext) {

  const todo = await Todo.findByOrFail('id', params.id)
  const body = await request.body()

  todo.title = body.title
  todo.description = body.description
  todo.status = body.status

  await todo.save()

  return response.redirect().toRoute('todo.index')
}
```

Pada kode di atas, fungsi edit akan dijalankan ketika kita ingin melakukan edit menggunakan id dan nantinya akan diarahkan ke halaman `edit.edge` dengan membawakan data todo dalam atribut `todo`.

Sedangkan method `update` akan bekerja ketika tombol submit nantinya ditekan sehingga akan memperbarui data yang sudah kita submit.

Kemudian buat file baru bernama `edit.edge` pada `resources/views/pages` dan masukkan kode di bawah ini:

```jinja
@base()
@slot("content")
<div class="container mt-5">
  <div class="row mb-4">
    <div class="col-6">
      <h5 class="mb-4">Buat Todo Baru</h5>

      <form method="POST" action="{{ route('todo.update', {id: todo.id}) }}?_method=PUT">
        {{ csrfField() }}
        <div class="form-group">
          <label for="title">Title</label>
          <input type="text" class="form-control" id="title" name="title" placeholder="Place your title here..."
            value="{{ todo.title }}">
        </div>
        <div class="form-group">
          <label for="description">Description</label>
          <textarea class="form-control" id="description" rows="3" placeholder="Place your description here...."
            name="description">{{ todo.description }}</textarea>
        </div>
        <div class="form-group">
          <label for="status">Status</label>
          <select class="form-control" id="status" name="status">
            <option value="TODO" {{ todo.status=='TODO' ? 'selected' : '' }}>TODO</option>
            <option value="ONGOING" {{ todo.status=='ONGOING' ? 'selected' : '' }}>ON GOING</option>
            <option value="DONE" {{ todo.status=='DONE' ? 'selected' : '' }}>DONE</option>
          </select>
        </div>
        <div class="form-group">
          <button class="btn btn-md btn-info" type="submit">Submit</button>
        </div>
      </form>
    </div>
  </div>
</div>
@end
@end
```

Dapat dilihat bahwa kita mengambil nilai dari masing-masing objek seperti title, description hingga kita membuat kondisi pada selection untuk memeriksa apakah statusnya todo, ongoing, atau done.

Apabila kalian perhatikan pada bagian action kita menggunakan nilai `action="{{ route('todo.update', {id: todo.id}) }}?_method=PUT"` dimana kita mengaktifkan spoofing pada `_method=PUT`. Artinya kita mengubah request tersebut walaupun methodnya `POST` menjadi `PUT`.

Terakhir, ubah kode `home.edge` pada bagian looping agar menjadi seperti ini:

```typescript
@each(todo in todos)
  <tr>
    <td>{{ todo.title }}</td>
    <td>{{ todo.description }}</td>
    <td>{{ todo.createdAt }}</td>
    <td>
      <span class="badge badge-info text-white ">{{ todo.status }}</span>
    </td>
    <td>
      <div class="btn-group " role="group " aria-label="Basic example ">
        <a href="{{ route('todo.edit', {id: todo.id}) }} " class="btn btn-info text-white ">
          <i class='bx bx-pencil'></i>
        </a>
        <a href="# " class="btn btn-danger text-white ">
          <i class='bx bx-trash'></i>
        </a>
      </div>
    </td>
  </tr>
@end
```

Kita hilangkan bagian check dan kita ubah URL untuk bagian edit dengan `href="{{ route('todo.edit', {id: todo.id}) }} "`, artinya untuk parameter id sesuai kebutuhan dari dasar routing, kita isi dengan nilai id dari todo tersebut.

![alt text](./assets/4.gif)

### Operasi Delete

Pertama, kita perlu mengubah kode pada controller todo secara keseluruhan agar menjadi seperti ini:

```typescript
import type { HttpContext } from '@adonisjs/core/http'
import Todo from '#models/todo'
import { DateTime } from 'luxon'

export default class TodosController {
  /**
   * Display a list of resource
   */
  async index({ view }: HttpContext) {
    const allTodos = await Todo.query().whereNull('deleted_at').orderBy('created_at', 'desc')
    return view.render("pages/home", { todos: allTodos })
  }

  /**
   * Display form to create a new record
   */
  async create({ view }: HttpContext) {
    return view.render("pages/create")
  }

  /**
   * Handle form submission for the create action
   */
  async store({ request, response }: HttpContext) {
    const todo = new Todo()
    const body = await request.body()

    todo.title = body.title
    todo.description = body.description
    todo.status = "TODO"

    await todo.save()

    return response.redirect().toRoute('todo.index')
  }

  /**
   * Show individual record
   */
  async show({ params }: HttpContext) { }

  /**
   * Edit individual record
   */
async edit({ view, params }: HttpContext) {
  const data = await Todo.findBy('id', params.id)
  return view.render("pages/edit", { todo: data })
}

/**
 * Handle form submission for the edit action
 */
async update({ params, request, response }: HttpContext) {

  const todo = await Todo.findByOrFail('id', params.id)
  const body = await request.body()

  todo.title = body.title
  todo.description = body.description
  todo.status = body.status

  await todo.save()

  return response.redirect().toRoute('todo.index')
}

  /**
   * Delete record
   */
  async destroy({ params, response }: HttpContext) {
    const todo = await Todo.findByOrFail('id', params.id)
    todo.deletedAt = DateTime.now()

    await todo.save()

    return response.redirect().toRoute('todo.index')
  }
}
```

Perubahan yang terjadi:

Pertama, kita mengimport library Luxon untuk datetime karena Adonis membutuhkan library tersebut untuk verifikasi tipe data datetime.

Kemudian untuk metode destroy, karena kita menggunakan soft delete, kita mengisi kolom deleted_at agar diisi dengan waktu pada saat ini.

Terakhir, untuk method index kita ubah cara kita menampilkan todo, yaitu kita tampilkan data yang deleted at nya kosong dan diurutkan berdasarkan waktu dibuat.

Terakhir, kita ubah file `home.edge` agar menjadi seperti ini:

```jinja
@base()
@slot("content")
<div class="container mt-5">
  <div class="row mb-4">
    <div class="col-12">
      <h5 class="mb-4">Judul Halaman</h5>
      <table class="table table-hover ">
        <thead>
          <tr>
            <th scope="col ">Title</th>
            <th scope="col ">Description</th>
            <th scope="col ">Created At</th>
            <th scope="col ">Status</th>
            <th scope="col ">Action</th>
          </tr>
        </thead>
        <tbody>
          @each(todo in todos)
          <tr>
            <td>{{ todo.title }}</td>
            <td>{{ todo.description }}</td>
            <td>{{ todo.createdAt }}</td>
            <td>
              <span class="badge badge-info text-white ">{{ todo.status }}</span>
            </td>
            <td>
              <div class="btn-group " role="group " aria-label="Basic example ">
                <a href="{{ route('todo.edit', {id: todo.id}) }} " class="btn btn-info text-white ">
                  <i class='bx bx-pencil'></i>
                </a>
                <form action="{{ route('todo.destroy', {id: todo.id}) }}?_method=DELETE"
                  method="POST"
                  onsubmit="return confirm('Are you sure want to delete data?')">
                  {{ csrfField() }}
                  <button type="submit" class="btn btn-danger text-white ">
                    <i class='bx bx-trash'></i>
                  </button>
                </form>
              </div>
            </td>
          </tr>
          @end
        </tbody>
      </table>
    </div>
  </div>
</div>
@end
@end
```

Kita menambahkan form action untuk menghapus data yang mana action ini akan diarahkan ke fungsi `destroy`.

Tak lupa kita mengisi spoofing URL dengan `_method=DELETE` karena kita akan mengakses RESTful dengan method `DELETE`.

Terakhir jalankan kembali dan lihat hasilnya sebagai berikut:

![alt text](./assets/5.gif)

Sekarang kita bisa lihat juga pada database menjadi seperti ini:

```plain
mysql> select * FROM todos;
+----+-----------------+---------------------+---------+---------------------+---------------------+---------------------+
| id | title           | description         | status  | created_at          | updated_at          | deleted_at          |
+----+-----------------+---------------------+---------+---------------------+---------------------+---------------------+
|  1 | Judul Todo ke-0 | Deskripsi Todo ke-0 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
|  2 | Judul Todo ke-1 | Deskripsi Todo ke-1 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
|  3 | Judul Todo ke-2 | Deskripsi Todo ke-2 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
|  4 | Judul Todo ke-3 | Deskripsi Todo ke-3 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
|  5 | Judul Todo ke-4 | Deskripsi Todo ke-4 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
|  6 | Judul Todo ke-5 | Deskripsi Todo ke-5 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
|  7 | Judul Todo ke-6 | Deskripsi Todo ke-6 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
|  8 | Judul Todo ke-7 | Deskripsi Todo ke-7 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
|  9 | Judul Todo ke-8 | Deskripsi Todo ke-8 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
| 10 | Judul Todo ke-9 | Deskripsi Todo ke-9 | TODO    | 2024-08-13 00:55:12 | 2024-08-13 00:55:12 | NULL                |
| 11 | Todo Test       | Test Todo           | TODO    | 2024-08-13 01:32:31 | 2024-08-13 07:58:51 | 2024-08-13 07:58:51 |
| 12 | Todo Baru-2     | Todo Baru-2         | ONGOING | 2024-08-13 01:48:22 | 2024-08-13 07:58:48 | 2024-08-13 07:58:48 |
+----+-----------------+---------------------+---------+---------------------+---------------------+---------------------+
12 rows in set (0.00 sec)
```


Viola, sudah berhasil menyelesaikan CRUD :smile:
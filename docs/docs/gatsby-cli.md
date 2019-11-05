---
title: Perintah (Gatsby CLI)
tableOfContentsDepth: 2
---

Gatsby *command line interface* (CLI) adalah *entry point* utama untuk memulai dan menjalankan aplikasi Gatsby dan juga kita dapat menggunakan fungsi-fungsinya termasuk untuk menjalankan *development server* dan membangun aplikasi Gatsby saat *deployment*.

_Kami menyediakan dokumentasi serupa yang tersedia dengan gatsby-cli [README](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-cli/README.md), dan [cheat sheet](/docs/cheat-sheet/) kami memiliki semua perintah CLI yang siap untuk dijalankan._

## Cara menggunakan gatsby-cli

Gatsby CLI (`gatsby-cli`) dapat dieksekusi dan digunakan secara global. Gatsby CLI tersedia melalui [npm](https://www.npmjs.com/) dan harus diinstal secara global dengan menjalankan `npm install -g gatsby-cli` untuk dapat digunakan secara lokal.

Jalankan `gatsby --help` untuk bantuan lengkap.

Anda juga dapat menggunakan varian skrip pada `package.json` untuk beberapa perintah tertentu, biasanya terbuka _untuk Anda_ pada sebagian besar [starters](/docs/starters/). Misalnya, jika Anda ingin perintah [`gatsby develop`](#develop) tersedia di aplikasi Anda, buka `package.json` dan tambahkan skrip seperti:

```json:title=package.json
{
  "scripts": {
    "develop": "gatsby develop"
  }
}
```

## Perintah API

### `new`

```
gatsby new [<site-name> [<starter-url>]]
```

#### Argumen

| Argumen    | Deskripsi                                                                                                                                                                                                     |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| site-name   | Nama situs Gatsby Anda, yang juga digunakan untuk membuat direktori proyek.                                                                                                                                      |
| starter-url | Gatsby *starter* URL atau *path* file lokal. Bawaannya yaitu [gatsby-starter-default](https://github.com/gatsbyjs/gatsby-starter-default); lihat dokumen [Gatsby *starters*](/docs/gatsby-starters/) untuk informasi lebih lanjut. |

> Catatan: `site-name` harus terdiri dari huruf dan angka. Jika Anda memberikan `.`, `./` atau `<space>` pada nama tersebut, `gatsby new` akan memberikan informasi terkait kesalahan.

#### Contoh

- Buat situs Gatsby bernama `my-awesome-site` menggunakan *starter* bawaan:

```shell
gatsby new my-awesome-site
```

- Buat nama situs Gatsby dengan nama `my-awesome-blog-site`, menggunakan [gatsby-starter-blog](https://www.gatsbyjs.org/starters/gatsbyjs/gatsby-starter-blog/):

```shell
gatsby new my-awesome-blog-site https://github.com/gatsbyjs/gatsby-starter-blog
```

- Jika Anda mengabaikan kedua argumen tersebut, CLI akan menjalankan *shell* interaktif yang meminta Anda untuk menginput ini:

```shell
gatsby new
? What is your project called? › my-gatsby-project
? What starter would you like to use? › - Use arrow-keys. Return to submit.
❯  gatsby-starter-default
   gatsby-starter-hello-world
   gatsby-starter-blog
   (Use a different starter)
```

Lihat [Dokumen Gatsby starters](https://www.gatsbyjs.org/docs/gatsby-starters/) untuk rincian lebih lanjut.

### `develop`

Setelah Anda menginstal situs Gatsby, buka direktori utama pada proyek Anda dan mulai *development server*:

`gatsby develop`

#### Pilihan

|     Pilihan     | Deskripsi                                       |
| :-------------: | ----------------------------------------------- |
| `-H`, `--host`  | Menetapkan host. Bawaannya yaitu localhost      |
| `-p`, `--port`  | Menetapkan port. Bawaannya yaitu 8000           |
| `-o`, `--open`  | Membuka situs di browser (bawaan) Anda          |
| `-S`, `--https` | Menggunakan HTTPS                               |

Ikuti [Panduan HTTPS Lokal](/docs/local-https/)
untuk mengetahui bagaimana Anda dapat mengatur *development server* HTTPS menggunakan Gatsby.

#### Pratinjau perubahan pada perangkat lain

Anda dapat menggunakan perintah *develop* pada Gatsby dengan opsi host untuk mengakses lingkungan pengembangan Anda di perangkat lain di jaringan yang sama, jalankan:

```shell
gatsby develop -H 0.0.0.0
```

Kemudian terminal akan mencatat informasi seperti biasanya, tetapi juga akan menyertakan URL yang dapat Anda navigasikan dari klien di jaringan yang sama untuk melihat bagaimana situs di-*render*.

```
You can now view gatsbyjs.org in the browser.
⠀
  Local:            http://0.0.0.0:8000/
  On Your Network:  http://192.168.0.212:8000/ // highlight-line
```

**Catatan**: Anda tidak dapat mengunjungi 0.0.0.0:8000 di Windows (tetapi semuanya akan berjalan dengan menggunakan localhost:8000 atau URL "Di Jaringan Anda" pada Windows)

### `build`

Pada *root* situs Gatsby, *compile* aplikasi Anda dan siapkan aplikasi Anda untuk *deployment*:

`gatsby build`

#### Pilihan

|            Pilihan            | Deskripsi                                                                                               |
| :--------------------------: | --------------------------------------------------------------------------------------------------------- |
|       `--prefix-paths`       | Membangun situs dengan jalur tautan yang menggunakan awalan (tetapkan pathPrefix di konfigurasi Anda)                |
|        `--no-uglify`         | Membangun situs tanpa bundel *uglifying* JS (untuk *debugging*)                                                  |
| `--open-tracing-config-file` | Konfigurasi pelacak file (kompatibel dengan OpenTracing). Lihat [Penelusuran Kinerja](/docs/performance-tracing/) |
| `--no-color`, `--no-colors`  | Menonaktifkan output terminal berwarna                                                                          |

Selain opsi pembangunan situs ini, ada beberapa pilihan [variabel lingkungan pembangunan situs](/docs/environment-variables/#build-variables) untuk konfigurasi lebih lanjut yang dapat menyesuaikan cara kerja pembangunan. Misalnya, menetapkan `CI = true` sebagai variabel lingkungan akan menyesuaikan *output* untuk [*dumb terminals*](https://en.wikipedia.org/wiki/Computer_terminal#Dumb_terminals).

### `serve`

Pada *root* situs Gatsby, sediakan versi produksi situs Anda untuk pengujian:

`gatsby serve`

#### Pilihan

|     Pilihan     | Deskripsi                                       |
| :-------------: | ----------------------------------------------- |
| `-H`, `--host`  | Menetapkan host. Bawaannya yaitu localhost      |
| `-p`, `--port`  | Menetapkan port. Bawaannya yaitu 8000           |
| `-o`, `--open`  | Membuka situs di browser (bawaan) Anda          |
| `-S`, `--https` | Menyediakan situs dengan jalur tautan yang menggunakan awalan (jika dibangun dengan pathPrefix di gatsby-config.js Anda). |

### `info`

Pada *root* situs Gatsby, dapatkan informasi lingkungan yang akan diperlukan saat melaporkan *bug*:

`gatsby info`

#### Pilihan

|       Pilihan       | Deskripsi                                                    |
| :-----------------: | -------------------------------------------------------      |
| `-C`, `--clipboard` | Secara otomatis menyalin informasi lingkungan ke *clipboard* |

### `clean`

Pada *root* situs Gatsby, menghapus *cache* (folder `.cache`) dan direktori publik:

`gatsby clean`

Ini berguna sebagai upaya terakhir ketika proyek lokal Anda tampaknya memiliki masalah. Masalah yang dapat diperbaiki ini biasanya meliputi:

- Data lama, misalnya file/resource/etc. ini tidak muncul
- Kesalahan GraphQL, misalnya sumber daya GraphQL ini harusnya ada tetapi ternyata tidak
- Masalah *dependency*, misalnya versi tidak valid, kesalahan *cryptic* di konsol, dll.
- Masalah *plugin*, misalnya mengembangkan *plugin* lokal dan perubahan tampaknya tidak berpengaruh

### `plugin`

Menjalankan perintah yang berkaitan dengan *plugin* gatsby.

#### `docs`

`gatsby plugin docs`

Mengarahkan Anda ke dokumentasi tentang penggunaan dan pembuatan *plugin*.

### Repl

Mendapatkan Node.js REPL (shell interaktif) dengan konteks lingkungan Gatsby Anda:

`gatsby repl`

Gatsby akan meminta Anda untuk mengetik perintah dan *explore*. Ketika itu menunjukkan ini: `gatsby >`

Anda bisa mengetikkan perintah, seperti salah satu dari:

`babelrc`

`components`

`dataPaths`

`getNodes()`

`nodes`

`pages`

`schema`

`siteConfig`

`staticQueries`

Ketika dikombinasikan dengan [GraphQL explorer](/docs/introducing-graphiql/), perintah REPL ini bisa sangat membantu untuk memahami data situs Gatsby Anda.

Untuk informasi lebih lanjut, lihat [Dokumentasi Gatsby REPL](/docs/gatsby-repl/).

### Menonaktifkan *output* berwarna

Selain opsi `--no-color` yang eksplisit, CLI menghargai keberadaan variabel lingkungan `NO_COLOR` (lihat [no-color.org](https://no-color.org/)).

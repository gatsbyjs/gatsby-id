---
title: Cara Singkat
---

Bagian ini dimaksudkan untuk para pengembang tingkat menengah hingga tingkat lanjut. Jika Anda masih baru dengan Gatsby, [buka tutorial kami](/tutorial/)!

## Menggunakan Gatsby CLI

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-quick-start-with-gatsby-create-develop-and-build-gatsby-sites-from-the-command-line"
  lessonTitle="Quick Start with Gatsby: Create, Develop, and Build Gatsby Sites From the Command Line"
/>

**Catatan**: video ini menggunakan `npx`, yang merupakan alat untuk menjalankan sebuah paket npm tanpa harus menginstalnya terlebih dahulu. Menjalankan perintah `npx gatsby new` sama dengan menjalankan `gatsby new` setelah menginstal gatsby-cli di komputer Anda.

<<<<<<< HEAD
### Instal Gatsby CLI.
=======
### Install the Gatsby CLI
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
npm install -g gatsby-cli
```

<<<<<<< HEAD
### Buat situs baru.
=======
> The above command installs Gatsby CLI globally on your machine.

### Create a new site
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
gatsby new gatsby-site
```

<<<<<<< HEAD
### Ubah direktori ke folder situs.
=======
### Change directories into site folder
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
cd gatsby-site
```

<<<<<<< HEAD
### Mulai *server* pengembangan.
=======
### Start development server
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
gatsby develop
```

<<<<<<< HEAD
Gatsby akan memulai *hot-reloading* pada lingkungan pengembangan yang dapat diakses secara bawaan di `localhost:8000`.
=======
Gatsby will start a hot-reloading development environment accessible by default at `http://localhost:8000`.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

Coba ubah laman JavaScript di `src/pages`. Perubahan yang disimpan akan langsung dimuat ulang di browser.

<<<<<<< HEAD
### Buat versi produksi.
=======
### Create a production build
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
gatsby build
```

Gatsby akan melakukan versi produksi yang dioptimalkan untuk situs Anda, menghasilkan HTML statis dan bundel kode JavaScript per rute.

<<<<<<< HEAD
### Menyediakan versi produksi secara lokal.
=======
### Serve the production build locally
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

```shell
gatsby serve
```

Gatsby memulai *server* HTML lokal untuk menguji situs yang Anda buat. Ingatlah untuk membangun situs Anda menggunakan `gatsby build` sebelum menggunakan perintah ini.

### Akses dokumentasi untuk perintah CLI

Untuk melihat dokumentasi secara terperinci terkait perintah CLI, jalankan `gatsby --help` di terminal.

Untuk perintah tertentu, jalankan `gatsby NAMA_PERINTAH --help` contoh `gatsby new --help`.

Untuk informasi lebih lanjut tentang Gatsby CLI, kunjungi bagian [Referensi CLI](/docs/gatsby-cli/) pada dokumen tersebut.

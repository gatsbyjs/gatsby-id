---
title: Mulai Cepat
---

Mulai cepat ini dimaksudkan untuk para pengembang tingkat menengah hingga tingkat lanjut. Untuk pengantar Gatsby, [buka tutorial kami](/tutorial/)!

## Menggunakan Gatsby CLI

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-quick-start-with-gatsby-create-develop-and-build-gatsby-sites-from-the-command-line"
  lessonTitle="Quick Start with Gatsby: Create, Develop, and Build Gatsby Sites From the Command Line"
/>

**Catatan**: video ini menggunakan `npx`, yang merupakan alat untuk menjalankan sebuah paket npm tanpa harus menginstalnya terlebih dahulu. Menjalankan perintah `npx gatsby new` sama dengan menjalankan `gatsby new` setelah menginstal gatsby-cli di komputer Anda.

### Instal Gatsby CLI.

```shell
npm install -g gatsby-cli
```

### Buat situs baru.

```shell
gatsby new gatsby-site
```

### Ubah direktori ke folder situs.

```shell
cd gatsby-site
```

### Mulai *server* pengembangan.

```shell
gatsby develop
```

Gatsby akan memulai *hot-reloading* pada lingkungan pengembangan yang dapat diakses secara bawaan di `localhost:8000`.

Coba ubah laman JavaScript di `src/pages`. Perubahan yang disimpan akan langsung dimuat ulang di browser.

### Buat versi produksi.

```shell
gatsby build
```

Gatsby akan melakukan versi produksi yang dioptimalkan untuk situs Anda, menghasilkan HTML statis dan bundel kode JavaScript per rute.

### Menyediakan versi produksi secara lokal.

```shell
gatsby serve
```

Gatsby memulai *server* HTML lokal untuk menguji situs yang Anda buat. Ingatlah untuk membangun situs Anda menggunakan `gatsby build` sebelum menggunakan perintah ini.

### Akses dokumentasi untuk perintah CLI

Untuk melihat dokumentasi secara terperinci terkait perintah CLI, jalankan `gatsby --help` di terminal.

Untuk perintah tertentu, jalankan `gatsby NAMA_PERINTAH --help` contoh `gatsby new --help`.

Untuk informasi lebih lanjut tentang Gatsby CLI, kunjungi bagian [Referensi CLI](/docs/gatsby-cli/) pada dokumen tersebut.

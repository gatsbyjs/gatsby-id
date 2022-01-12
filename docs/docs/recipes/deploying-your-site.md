---
title: "Resep: Menerapkan Situs Anda"
tableOfContentsDepth: 1
---

Pertunjukan dimulai, Setelah Anda puas dengan situs Anda, Anda siap untuk menggunakannya!

## Persiapan untuk penerapan

### Persyaratan

- [Situs Gatsby](/docs/quick-start)
- [Gatsby CLI](/docs/gatsby-cli) terpasang.

### Petunjuk arah

1. Hentikan server pengembangan Anda jika sedang berjalan (`Ctrl + C` pada baris perintah Anda dalam banyak kasus)

2. Untuk jalur situs standar di direktori root (`/`), jalankan `gatsby build` menggunakan Gatsby CLI pada baris perintah. File yang dibangun sekarang akan berada di folder `public`.

```shell
gatsby build
```

3. Untuk menyertakan jalur situs selain `/` (seperti `/nama-situs/`), atur path prefix dengan menambahkan yang berikut ini ke `gatsby-config.js` Anda dan mengganti `yourpathprefix` dengan path prefix keinginan Anda:


```js:title=gatsby-config.js
module.exports = {
  pathPrefix: `/yourpathprefix`,
}
```

Ada beberapa alasan untuk melakukan ini -- misalnya, menghosting blog yang dibuat dengan Gatsby di domain dengan situs lain yang tidak dibuat di Gatsby. Situs utama akan mengarah ke `example.com`, dan situs Gatsby dengan awalan jalur dapat ditampilkan di `example.com/blog`.

1. Dengan awalan jalur yang disetel di `gatsby-config.js`, jalankan `gatsby build` dengan tanda `--prefix-paths` untuk secara otomatis menambahkan awalan ke awal semua URL situs Gatsby dan tag `<Link>`.

```shell
gatsby build --prefix-paths
```

5. Pastikan situs Anda terlihat sama saat menjalankan `gatsby build` seperti pada `gatsby develop`. Dengan menjalankan `gatsby serve` saat membangun situs, Anda dapat menguji (dan men-debug jika perlu) produk jadi sebelum menerapkannya secara langsung.

```shell
gatsby build && gatsby serve
```

### Sumber daya tambahan

- Jelajahi pembuatan dan penerapan situs contoh di [tutorial bagian satu](/tutorial/part-one/#deploying-a-gatsby-site)
- Pelajari tentang [pengoptimalan kinerja](/docs/performance/)
- Baca tentang [topik terkait penerapan lainnya](/docs/preparing-for-deployment/)
- Lihat [dokumen penerapan](/docs/deploying-and-hosting/) for specific hosting platforms and how to deploy to them

## Menerapkan ke Netlify

Gunakan [`netlify-cli`](https://www.netlify.com/docs/cli/) untuk menerapkan aplikasi Gatsby Anda tanpa meninggalkan antarmuka baris perintah.

### Prasyarat

- Halaman [Situs Gatsby](/docs/quick-start) dengan satu komponen `index.js`
- Paket [netlify-cli](https://www.npmjs.com/package/netlify-cli) terpasang
- [Gatsby CLI](/docs/gatsby-cli) terpasang

### Petunjuk arah

1. Bangun aplikasi gatsby Anda menggunakan `gatsby build`

2. Masuk ke Netlify menggunakan `netlify login`

3. Jalankan perintah `netlify init`. Pilih opsi "Buat & konfigurasikan situs baru".

4. Pilih nama situs web khusus jika Anda mau atau tekan enter untuk menerima yang acak.

5. Pilih [Team](https://www.netlify.com/docs/teams/) kamu.

6. Ubah path ke `public/`

7. Pastikan semuanya terlihat baik-baik saja sebelum digunakan untuk produksi menggunakan `netlify deploy -d . --prod`

### Sumber daya tambahan

- [Hosting di Netlify](/docs/hosting-on-netlify)
- [gatsby-plugin-netlify](/packages/gatsby-plugin-netlify)

## Menyebarkan ke ZEIT Sekarang

Gunakan [Now CLI](https://zeit.co/download) untuk menyebarkan aplikasi Gatsby Anda tanpa meninggalkan antarmuka baris perintah.

### Prasyarat

- Akun [ZEIT Now](https://zeit.co/signup)
- [Situs Gatsby](/docs/quick-start) dengan satu komponen `index.js`
- Paket [Now CLI](https://zeit.co/download) terpasang
- [Gatsby CLI](/docs/gatsby-cli) terpasang

### Petunjuk arah

1. Masuk ke Sekarang CLI menggunakan `now login`

2. Ubah ke direktori aplikasi Gatsby.js Anda di Terminal jika Anda belum melakukannya

3. Jalankan `now` untuk menyebarkannya

### Sumber daya tambahan

- [Menyebarkan ke ZEIT Now](/docs/deploying-to-zeit-now/)

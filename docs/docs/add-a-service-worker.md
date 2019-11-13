---
title: Menambahkan Service Worker
---

## Apa itu service worker

Service worker adalah sebuah skrip yang dijalankan pada browser anda di latar belakang, terpisah dari halaman web, menyediakan fitur yang tidak membutuhkan halaman web atau interaksi user. Service Worker dapat meningkatkan ketersediaan halaman dalam koneksi yang tidak stabil, dan sangat penting untuk membuat pengalaman pengguna yang baik.

Service worker mendukung fitur seperti push notifikasi dan sinkronisasi latar belakang.

## Menggunakan service workers di Gatsby dengan `gatsby-plugin-offline`

Gatsby menyediakan antarmuka plugin yang luar biasa untuk membuat dan memuat service worker ke dalam situs anda [gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

Kamu bisa menggunakan plugin ini bersama dengan [manifest plugin](https://www.npmjs.com/package/gatsby-plugin-manifest). (Jangan lupa untuk mendaftarkan offline plugin setelah manifest plugin sehingga manifest file dapat dimasukan ke dalam service worker).

## Menginstal `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Tambahkan plugin ini ke dalam `gatsby-config.js` anda

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-offline`]
```

## Referensi

- [Service Workers: an Introduction](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)

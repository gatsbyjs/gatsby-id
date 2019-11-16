---
title: Menambahkan Service Worker
---

## Apa itu *service worker*

*Service worker* adalah *script* yang dijalankan oleh peramban web anda di balik layar, terpisah dengan halaman web, membuka pintu untuk fitur-fitur yang tidak memerlukan halaman web atau interaksi dengan pengguna. Hal ini meningkatkan ketersedian situs anda pada koneksi yang kurang lancar, dan sangat penting untuk menciptakan pengalaman pengguna yang baik.

*Service worker* mendukung fitur-fitur seperti *push notification* dan *background sync*.

## Menggunakan *service worker* pada Gatsby dengan `gatsby-plugin-offline`

Gatsby menyediakan antarmuka *plugin* untuk membuat dan memuat *service worker* ke dalam situs anda dengan [gatsby-plugin-offline](https://www.npmjs.com/package/gatsby-plugin-offline).

Anda dapat menggunakan *plugin* ini dengan [manifest plugin](https://www.npmjs.com/package/gatsby-plugin-manifest). (Jangan lupa untuk mendaftarkan *offline plugin* setelah *manifest plugin* agar file *manifest* dapat dimasukkan ke dalam *service worker*).

## Memasang `gatsby-plugin-offline`

`npm install --save gatsby-plugin-offline`

Tambahkan *plugin* ini pada file `gatsby-config.js` Anda

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-offline`]
```

## Referensi

- [Service Worker: sebuah pengantar](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [API Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)

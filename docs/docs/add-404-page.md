---
title: Menambahkan Halaman 404
---

Untuk membuat halaman 404 buat halaman yang jalurnya cocok dengan regex
`^\/?404\/?$` (`/404/`, `/404`, `404/` or `404`). Kerap Anda ingin membuat halaman *React component* di
`src/pages/404.js`.

Gatsby memastikan bahwa halaman 404 Anda dibuat sebagai `404.html` karena banyak platform hosting statis yang menggunakan ini sebagai halaman kesalahan 404 Anda. Jika Anda meng-hosting situs Anda
dengan cara lain, Anda harus menyiapkan aturan khusus untuk menyajikan file ini untuk halaman 404.

Karena Gatsby membuat halaman ini secara default, Anda tidak perlu mengonfigurasi file `gatsby-node.js`.

Saat melakukan pengembangan menggunakan `gatsby develop`, Gatsby menggunakan halaman dasar 404 untuk
mengganti halaman 404 khusus Anda. Namun, Anda masih dapat melihat halaman 404 Anda dengan
mengklik "Preview custom 404 page" untuk memverifikasi bahwa hal ini berfungsi seperti yang diharapkan. Hal ini
berguna ketika Anda sedang melakukan pengembangan sehingga Anda dapat melihat semua halaman yang tersedia.

Gambar di bawah ini menunjukkan halaman dasar 404 yang dibuat Gatsby.
Dalam halaman tersebut juga mencantumkan semua halaman di situs web Anda. Dengan klik "Preview custom 404 page" akan mengizinkan Anda untuk melihat halaman 404 yang Anda buat.
![Gatsby Halaman Dasar 404](images/gatsby-default-404.png)

Gambar di bawah ini menunjukkan halaman 404 khusus.
![Gatsby Halaman 404 yang dimodifikasi](images/gatsby-custom-404.png)

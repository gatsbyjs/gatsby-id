---
title: Menambahkan Halaman 404
---

<<<<<<< HEAD
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
=======
To create a 404 page create a page whose path matches the regex `^\/?404\/?$` (`/404/`, `/404`, `404/` or `404`). Most often you'll want to create a React component page at `src/pages/404.js`.

Gatsby ensures that your 404 page is built as `404.html` as many static hosting platforms default to using this as your 404 error page. If you're hosting your site another way you'll need to set up a custom rule to serve this file for 404 errors.

Because Gatsby creates this page for you by default, there is no need to configure it in your `gatsby-node.js` file.

When developing using `gatsby develop`, Gatsby uses a default 404 page that overrides your custom 404 page. However, you can still preview your 404 page by clicking "Preview custom 404 page" to verify that it's working as expected. This is useful when you're developing so that you can see all the available pages.

The screenshot below shows the default 404 page that Gatsby creates. It also lists out all the pages on your website. Clicking the "Preview custom 404 page" button will allow you to view the 404 page you created.
![Gatsby Default 404 Page](./images/gatsby-default-404.png)

The screenshot below shows the custom 404 page.
![Gatsby Custom 404 Page](./images/gatsby-custom-404.png)
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

---
title: File API
---

Gatsby menggunakan 4 file di *root* proyek Anda untuk mengkonfigurasi situs Anda dan mengendalikan perilakunya. Semua file ini opsional.

- [gatsby-config.js](/docs/api-files-gatsby-config) - Mengaktifkan *plugin*, mendefinisikan data umum situs, dan berisi konfigurasi lain yang terintegrasi dengan lapisan data GraphQL dari Gatsby.
- [gatsby-browser.js](/docs/api-files-gatsby-browser) - Memberikan Anda kendali atas perilaku Gatsby di peramban web. Sebagai contoh, memberikan respon terhadap pengguna yang berpindah rute, atau memanggil fungsi ketika pengguna membuka laman apapun pertama kali.
- [gatsby-node.js](/docs/api-files-gatsby-node) - Memungkinkan Anda untuk merespon *event* pada *build cycle* Gatsby. Sebagai contoh, menambahkan laman secara dinamis, mengubah *node* GraphQL saat dibuat, atau melakukan tindakan setelah proses *build* selesai.
- [gatsby-ssr.js](/docs/api-files-gatsby-ssr) - Mengekspos proses *server-side rendering* Gatsby sehingga Anda dapat mengendalikan bagaimana Gatsby membangun laman HTML Anda.

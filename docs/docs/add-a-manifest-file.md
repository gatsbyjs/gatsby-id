---
title: Menambahkan File Manifest
---

Jika kamu menjalankan [audit dengan menggunakan *Lighthouse*](/docs/audit-with-lighthouse/), mungkin kamu akan mendapatkan notifikasi skor di dalam kategori *"Progressive Web App"*. Mari kita bahas bagaimana cara meningkatkan skor di PWA.

Tetapi hal yang pertama adalah, apa itu PWA?

PWA adalah website biasa yang mengambil keutungan dari browser modern untuk meningkatkan pengalaman dengan fitur - fitur dan manfaat yang mirip seperti aplikasi. Periksa [Gambaran Google's](https://developers.google.com/web/progressive-web-apps/) tentang apa definisi pengalaman di PWA dan [dokumentasi *Progressive web apps (PWAs)*](/docs/progressive-web-app/) untuk belajar bagaimana membuat aplikasi website yang *progressive* di Gatsby.

Sebuah inklusi dari web app manifest adalah satu dari tiga hal yang disetujui secara umum [tentang syarat dasar untuk PWA](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1).

Mengutip [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> Sebuah web app manifest adalah file JSON sederhana yang meminta browser untuk mengenali aplikasi websitemu dan bagaimana seharusnya ketika 'di install' di browser mobile atau desktop.

[Gatsby's manifest plugin](/packages/gatsby-plugin-manifest/) konfigurasi Gatsby untuk membuat sebuah file `manifest.webmanifest` setiap kali website di bangun.

### Menggunakan `gatsby-plugin-manifest`

1.  Menginstall plugin:

```shell
npm install --save gatsby-plugin-manifest
```
2. Tambahkan favicon untuk aplikasimu di bawah `src/images/icon.png`. Iconnya sangat perlu untuk membangun semua gambar untuk file manifest. Untuk informasi lebih lanjut silahkan lihat dokumentasi dari [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).

3. Tambahkan plugin di `plugins` array yang terdapat di file `gatsby-config.js`.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: "GatsbyJS",
        short_name: "GatsbyJS",
        start_url: "/",
        background_color: "#6b37bf",
        theme_color: "#6b37bf",
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: "standalone",
        icon: "src/images/icon.png", // This path is relative to the root of the site.
        // An optional attribute which provides support for CORS check.
        // If you do not provide a crossOrigin option, it will skip CORS for manifest.
        // Any invalid keyword or empty string defaults to `anonymous`
        crossOrigin: `use-credentials`,
      },
    },
  ]
}
```

Itu saja yang kamu butuhkan untuk menambahkan file manifest di website Gatsby. Contoh yang diberikan menggambarkan konfigurasi basis -- silahkan cek referensi di [referensi *plugin*](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) untuk opsi lebih lanjut.

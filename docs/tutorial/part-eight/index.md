---
judul: Mempersiapkan situs untuk Ditayangkan
typora-copy-images-to: ./
disableTableOfContents: true
---

Wow! Anda telah melalui perjalanan belajar yang cukup jauh! mulai dari cara:

- Membuat situs Gatsby yang baru
- Membuat halaman beserta komponennya
- Membuat komponen tampilan atau _style_
- Menambahkan _plugin_ kedalam situs anda
- Sumber dan Perubahan data
- Menggunakan _Graphql_ melakukan pengolahaan data untuk keperluan halaman anda
- Membuat halaman secara terprogram dari data yang Anda miliki

Di bagian akhir berikut ini, Anda akan berjalan beberapa langkah secara umum untuk menyiapkan situs anda untuk ditayangkan, dengan memperkenalkan alat diagnostik situs yang kuat bernama [Lighthouse](https://developers.google.com/web/tools/lighthouse/). Selanjutnya, kami akan memperkenalkan ke beberapa _plugin_ lagi yang nantinya sering Anda gunakan di dalam situs Gatsby Anda.

## Pemeriksaan dengan menggunakan Lighthouse

Mengutip dari [situs web Lighthouse](https://developers.google.com/web/tools/lighthouse/):


> _Lighthouse_ merupakan sebuah sumber terbuka atau bisa disebut _open-source_, yang merupakan alat yang bekerja otomatis untuk peningkatan kualitas halaman web. Anda bisa menjalankannya di beberapa halaman web, baik publik bahkan yang memerlukan autentifikasi. Terdapat pemeriksaan untuk kinerja, kemudahan, _progressive web apps (PWAs)_, dan banyak lagi.

_Lighthouse_ juga termasuk di dalam bagian _Chrome DevTools_. Jalankan _lighthouse_ --  dan kemudian lakukan perbaikan kesalahan yang ditemukannya, serta implementasikan peningkatan yang disarankan -- berikut ini langkah yang bagus sebelum situs anda ditayangkan. membantu memberi Anda kepercayaan diri bahwa situs Anda cepat dan dapat diakses.

Mari coba sekarang!

Pertama, Anda perlu membuat bagian produksi pengembangan situs Gatsby Anda. Server dari pengembangan Gatsby dioptimalkan untuk mempercepat proses pengembangan Namun situs yang dihasilkannya akan sangat mirip dengan versi produksi situs tersebut, meskipun tidak dioptimalkan.

### ✋ Membuat sebuah pengembangan produksi

1.  Hentikan _server_ pengembangan (jika masih berjalan) dan jalankan perintah berikut:

```shell
gatsby build
```
> 💡 Seperti yang telah Anda pelajari di [bagian 1](/tutorial/part-one/), ini menghasilkan berupa pengembangan situs Anda dan menghasilkan file statis yang ditempatkan ke dalam direktori `public`.

2. Lihat lokasi produksi situs secara lokal. jalankan perintah berikut ini:

```shell
gatsby serve
```

<<<<<<< HEAD
Setelah ini dijalankan, Anda dapat melihat situs Anda di [`localhost:9000`](http://localhost:9000).
=======
Once this starts, you can view your site at `http://localhost:9000`.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

### Menjalankan audit Lighthouse

Sekarang Anda akan menjalankan tes _Lighthouse_ pertama Anda.

1.  Jika Anda belum melakukannya, buka situs dalam Mode Penyamaran atau _Incognito Mode_ pada _Chrome_ sehingga tidak ada ekstensi yang mengganggu proses pengujian. Lalu, buka _Chrome DevTools_.

2.  Klik pada tab "_Audit_" di mana Anda akan melihat layar yang terlihat seperti berikut ini:

![Lighthouse audit start](./lighthouse-audit.png)

3.  Klik "_Perform an audit..._" (Semua jenis audit yang tersedia harus dipilih secara _default_). Kemudian klik "_Run audit_". (Selanjutnya akan membutuhkan satu menit atau lebih untuk menjalankan audit). Setelah audit selesai, Anda akan melihat hasil yang terlihat seperti ini:

![Lighthouse audit start](./lighthouse-audit-results.png)

Seperti yang Anda lihat, kinerja Gatsby anda sangat bagus, tetapi Anda kehilangan beberapa hal untuk _PWA, Accessibility, Best Practices, and SEO_ yang akan meningkatkan skor Anda (dan dalam proses berikut ini membuat situs Anda jauh lebih ramah bagi pengunjung dan mesin pencari).

## Menambahkan sebuah file _manifest_

Sepertinya Anda memiliki skor yang cukup tidak menarik di kategori "_Progressive Web App_". Mari kita atasi ini.

Namun, apa sebenarnya _PWA_ itu?

Mereka adalah situs web biasa yang memanfaatkan fungsionalitas dari mesin pencari _modern_ untuk menambah pengalaman web seperti fitur aplikasi. Lihat [ikhtisar dari Google](https://developers.google.com/web/progressive-web-apps/) yang menjelaskan pengalaman pada fitur _PWA_.

Pencantuman _manifest_ pada aplikasi web adalah salah satu dari tiga syarat yang diterima secara umum, berikut [persyaratan dasar untuk _PWA_](https://alistapart.com/article/yes-that-web-project-should-be-a-pwa#section1).

Kutipan dari [Google](https://developers.google.com/web/fundamentals/web-app-manifest/):

> _Manifest_ pada aplikasi web adalah file berupa _JSON_ sederhana yang memberi tahu mesin pencari tentang aplikasi web Anda dan bagaimana seharusnya berperilaku ketika di-'_install_' pada perangkat seluler atau pada pengguna desktop.

[_Plugin manifest_ Gatsby](/packages/gatsby-plugin-manifest/) untuk mengkonfigurasi Gatsby dengan membuat file `manifest.webmanifest` di setiap pembuatan situs.

### ✋ Menggunakan `gatsby-plugin-manifest`

1.  Menambahkan _plugin_:

```shell
npm install --save gatsby-plugin-manifest
```

2. Tambahkan _favicon_ untuk aplikasi Anda di bawah `src/images/icon.png`. Untuk keperluan tutorial ini, jika Anda tidak memiliki satupun yang tersedia bisa Anda gunakan [contoh ikon berikut](https://raw.githubusercontent.com/gatsbyjs/gatsby/master/docs/tutorial/part-eight/icon.png). Ikon sangat diperlukan untuk membuat semua gambar pada _manifest_. Untuk informasi lebih lanjut, lihat dokumen berikut ini [`gatsby-plugin-manifest`](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-plugin-manifest/README.md).


3. Tambahkan _plugin_ ke dalam _array_ `plugins` pada file` gatsby-config.js` Anda.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
  ]
}
```

Ini semua yang anda butuhkan cukup dengan menambahkan _manifest_ ke dalam situs web Gatsby anda. Contoh yang diberikan merupakan contoh konfigurasi dasar -- Lihat [referensi _plugin_](/packages/gatsby-plugin-manifest/?=gatsby-plugin-manifest#automatic-mode) untuk pilihan lainnya.

## Menambahkan dukungan _Offline_

Persyaratan lain agar situs web memenuhi syarat sebagai _PWA_ adalah penggunaan [_service worker_](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API). Sebuah _service worker_ berjalan di latar belakang, menentukan untuk melayani bagian jaringan atau konten yang di-_cache_ atau disembunyikan berdasarkan konektivitas, untuk memungkinkan pengalaman yang dapat dikelola tanpa hambatan saat anda _offline_.

[_Plugin offline_ Gatsby's](/packages/gatsby-plugin-offline/) membuat situs Gatsby anda dapat bekerja secara _offline_ dan lebih tahan terhadap kondisi jaringan yang buruk, dengan menciptakan sebuah _service worker_ untuk situs Anda.

### ✋ Tambahkan `gatsby-plugin-offline`

1.  Menambahkan _plugin_:

```shell
npm install --save gatsby-plugin-offline
```

2.  Tambahkan _plugin_ ke dalam _array_ `plugins` pada file` gatsby-config.js` Anda.

```javascript:title=gatsby-config.js
{
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    // highlight-next-line
    `gatsby-plugin-offline`,
  ]
}
```

Hanya itu saja yang anda butuhkan untuk memulai menggunakan _service worker_ dengan Gatsby.

> 💡 _Plugin offline_ harus terdaftar setelah plugin _manifest_ sehingga _plugin offline_ dapat menyimpan _cache_ `manifest.webmanifest` yang dibuat.

## Menambahkan _metadata_ pada halaman

Menambahkan _metadata_ ke dalam halaman (seperti judul atau deskripsi) merupakan kunci dalam membantu mesin pencari seperti _Google_ memahami konten Anda dan memutuskan kapan akan muncul di hasil pencarian.

[_React Helmet_](https://github.com/nfl/react-helmet) adalah _package_ yang menyediakan komponen dari _React_ untuk mengelola antarmuka di bagian [kop dokumen atau _document head_](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head)anda.

[_Plugin react helmet_](/packages/gatsby-plugin-react-helmet/) Gatsby menyediakan dukungan bersifat sementara atau bisa disebut _drop-in_ untuk _rendering data server_ yang nantinya ditambahkan dengan _React Helmet_. Dengan menggunakan _plugin_ ini, atribut yang Anda tambahkan ke _React Helmet_ akan ditambahkan juga ke dalam halaman _HTML_ statis yang dibuat oleh Gatsby.

### ✋ Menggunakan `React Helmet` dan` gatsby-plugin-react-helmet`

1.  Menambahkan kedua _package_:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2.  Pastikan Anda memiliki konfigurasi `_description_` dan `_author_` di dalam objek `_siteMetadata_` Anda. Tambahkan juga _plugin_ `gatsby-plugin-react-helmet` ke dalam _array `plugins`_ di dalam file `gatsby-config.js` Anda.

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
    // highlight-start
    description: `A simple description about pandas eating lots...`,
    author: `gatsbyjs`,
    // highlight-end
  },
  plugins: [
    {
      resolve: `gatsby-plugin-manifest`,
      options: {
        name: `GatsbyJS`,
        short_name: `GatsbyJS`,
        start_url: `/`,
        background_color: `#6b37bf`,
        theme_color: `#6b37bf`,
        // Enables "Add to Homescreen" prompt and disables browser UI (including back button)
        // see https://developers.google.com/web/fundamentals/web-app-manifest/#display
        display: `standalone`,
        icon: `src/images/icon.png`, // This path is relative to the root of the site.
      },
    },
    `gatsby-plugin-offline`,
    // highlight-next-line
    `gatsby-plugin-react-helmet`,
  ],
}
```

3. Di dalam direktori `src/components`, buat file bernama `seo.js` dan tambahkan berikut ini:

```jsx:title=src/components/seo.js
import React from "react"
import PropTypes from "prop-types"
import Helmet from "react-helmet"
import { useStaticQuery, graphql } from "gatsby"

function SEO({ description, lang, meta, title }) {
  const { site } = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
            description
            author
          }
        }
      }
    `
  )

  const metaDescription = description || site.siteMetadata.description

  return (
    <Helmet
      htmlAttributes={{
        lang,
      }}
      title={title}
      titleTemplate={`%s | ${site.siteMetadata.title}`}
      meta={[
        {
          name: `description`,
          content: metaDescription,
        },
        {
          property: `og:title`,
          content: title,
        },
        {
          property: `og:description`,
          content: metaDescription,
        },
        {
          property: `og:type`,
          content: `website`,
        },
        {
          name: `twitter:card`,
          content: `summary`,
        },
        {
          name: `twitter:creator`,
          content: site.siteMetadata.author,
        },
        {
          name: `twitter:title`,
          content: title,
        },
        {
          name: `twitter:description`,
          content: metaDescription,
        },
      ].concat(meta)}
    />
  )
}

SEO.defaultProps = {
  lang: `en`,
  meta: [],
  description: ``,
}

SEO.propTypes = {
  description: PropTypes.string,
  lang: PropTypes.string,
  meta: PropTypes.arrayOf(PropTypes.object),
  title: PropTypes.string.isRequired,
}

export default SEO
```

Kode di atas mengatur _default_ untuk _tag metadata_ Anda secara umum dan memberi Anda komponen `<SEO>` yang dikerjakan dengan santai pada proyek Anda. Cukup keren, bukan?

4.  Sekarang, Anda dapat menggunakan komponen `<SEO>` di _template_ dan halaman Anda serta meneruskan _props_ ke sana. Sebagai contoh, tambahkan ke _template_ `blog-post.js` Anda seperti berikut ini:

```jsx:title=src/templates/blog-post.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"
// highlight-next-line
import SEO from "../components/seo"

export default ({ data }) => {
  const post = data.markdownRemark
  return (
    <Layout>
      // highlight-start
      <SEO title={post.frontmatter.title} description={post.excerpt} />
      // highlight-end
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </Layout>
  )
}

export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
      // highlight-next-line
      excerpt
    }
  }
`
```

Contoh di atas berdasarkan dari [_Gatsby Starter Blog_](/starters/gatsbyjs/gatsby-starter-blog/). Dengan melewatkan _props_ ke dalam komponen `<SEO>`, Anda dapat secara dinamis mengubah _metadata_ untuk sebuah _posting_. Dalam hal ini, _postingan blog_ `_title_` dan `_excerpt_` (jika ada file _markdown_ di dalam posting _blog_) maka `_siteMetadata_` akan digunakan sebagai ganti properti _default_ di dalam file `gatsby-config.js` Anda.

Sekarang, jika Anda menjalankan audit _Lighthouse_ kembali seperti yang dijelaskan sebelumnya di atas, Anda harus mendekati nilai 100! meski itu bukan merupakan nilai yang sempurna

> 💡 mengenai bacaan dan contoh lebih lanjut, dapat dilihat bagian [Menambahkan Komponen _SEO_](/docs/add-seo-component/) dan [Dokumen _React Helmet_](https://github.com/nfl/react-helmet#example)!

## Mari membuatnya menjadi lebih baik

Di bagian ini, kami telah menunjukkan kepada Anda beberapa alat khusus Gatsby untuk meningkatkan kinerja situs Anda dan persiapan untuk ditayangkan.

_Lighthouse_ adalah alat yang hebat untuk perbaikan dan pembelajaran situs -- Lanjutkan dengan mencari melalui umpan balik terperinci yang diberikannya dan terus membuat situs Anda menjadi lebih baik!

## Langkah Selanjutnya

### Dokumentasi Resmi

- [Dokumentasi Resmi](https://www.gatsbyjs.org/docs/): Lihat Dokumentasi Resmi kami untuk _[Memulai Cepat](https://www.gatsbyjs.org/docs/quick-start/)_, _[Panduan Lengkap](https://www.gatsbyjs.org/docs/preparing-your-environment/)_, _[Referensi API](https://www.gatsbyjs.org/docs/gatsby-link/)_, dan masih banyak lagi.

### _Plugins_ Resmi

- [_Plugins_ Resmi](https://github.com/gatsbyjs/gatsby/tree/master/packages): Daftar lengkap semua _Plugin_ Resmi yang dikelola oleh Gatsby.

### _Starters_ Resmi

<<<<<<< HEAD
1.  [_Gatsby's Default Starter_](https://github.com/gatsbyjs/gatsby-starter-default): Mulailah proyek Anda dengan kerangka _default_ ini. _Starter_ setengah jadi ini dikirimkan bersama file konfigurasi utama Gatsby yang mungkin Anda butuhkan. _[contoh kerja](http://gatsbyjs.github.io/gatsby-starter-default/)_
2.  [_Gatsby's Blog Starter_](https://github.com/gatsbyjs/gatsby-starter-blog): _Gatsby Starter_ untuk membuat _blog_ yang luar biasa dan sangat cepat. _[contoh kerja](http://gatsbyjs.github.io/gatsby-starter-blog/)_
3.  [_Gatsby's Hello-World Starter_](https://github.com/gatsbyjs/gatsby-starter-hello-world): _Gatsby Starter_ dengan hal-hal mendasar yang diperlukan untuk sebuah situs Gatsby. _[contoh kerja](https://gatsby-starter-hello-world-demo.netlify.com/)_
=======
1.  [Gatsby's Default Starter](https://github.com/gatsbyjs/gatsby-starter-default): Kick off your project with this default boilerplate. This barebones starter ships with the main Gatsby configuration files you might need. _[working example](https://gatsbyjs.github.io/gatsby-starter-default/)_
2.  [Gatsby's Blog Starter](https://github.com/gatsbyjs/gatsby-starter-blog): Gatsby starter for creating an awesome and blazing-fast blog. _[working example](https://gatsbyjs.github.io/gatsby-starter-blog/)_
3.  [Gatsby's Hello-World Starter](https://github.com/gatsbyjs/gatsby-starter-hello-world): Gatsby Starter with the bare essentials needed for a Gatsby site. _[working example](https://gatsby-starter-hello-world-demo.netlify.com/)_
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Itu saja, sobat

Sebenarnya tidak cukup hanya untuk mengandalkan tutorial ini saja. Ada [Tutorial Tambahan](/tutorial/additional-tutorials/) untuk memeriksa kasus penggunaan yang lebih terperinci.

Ini hanya permulaan, teruskan!

- Apakah Anda membuat sesuatu yang keren? Bagikan di _Twitter_, beri _tag_ [#buildwithgatsby](https://twitter.com/search?q=%23buildwithgatsby), dan [_@mention_ kami](https://twitter.com/gatsbyjs)!
- Apakah Anda menulis posting blog keren tentang apa yang Anda pelajari? Bagikan itu juga!
- Berkontribusi! kunjungi bagian berikut ini [_open issues_](https://github.com/gatsbyjs/gatsby/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) melalui _repo_ gatsby dan [Menjadi kontributor](/contributing/how-to-contribute/).

lihat dokumen [bagaimana cara berkontribusi](/contributing/how-to-contribute/) untuk lebih membuat banyak ide.

Kami tidak sabar untuk melihat apa yang Anda lakukan sekanjutnya 😄.

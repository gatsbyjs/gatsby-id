---
judul: Membuat Komponen layout Bertingkat
typora-copy-images-to: ./
disableTableOfContents: true
---

Selamat Datang di bagian ketiga

## Apa saja yang ada didalam tutorial ini?

Didalam bagian ini, anda akan belajar tentang _plugins_ dari Gatsby dan pembuatan komponen _layout_ atau tata letak.

_Plugin_ Gatsby ini merupakan paket dari komponen-komponen Javascript yang berfungsi membantu menambah fungsionalitas ke sebuah situs Gatsby. Gatsby dirancang agar dapat dikembangkan, yang berarti _plugin_ dapat memperluas dan memodifikasi apa saja yang dilakukan Gatsby.

Komponen _Layout_ merupakan bagian dari situs anda yang nantinya bisa anda bagikan di beberapa halaman. Misalnya, situs umumnya akan memiliki komponen _layout_ dengan _header_ dan _footer_ bersama. Hal-hal umum lainnya untuk ditambahkan ke dalam _layout_ adalah menu _sidebar_ dan / atau navigasi. Di halaman ini misalnya, tajuk di bagian atas adalah bagian dari komponen _layout_ gatsbyjs.org.

mari selami bagian ketiga.

## Penggunaan _Plugin_

Anda mungkin mengetahui gagasan dari _plugin_. Banyak sistem perangkat lunak yang mendukung penambahan _plugin_ khusus untuk menambah fungsionalitas baru atau bahkan memodifikasi inti kerja dari perangkat lunak. _Plugin_ Gatsby juga bekerja dengan cara yang sama.

Anggota komunitas (seperti anda!) Dapat berkontribusi _plugin_ (sejumlah kecil kode JavaScript) yang kemudian dapat digunakan orang lain ketika membangun situs Gatsby mereka.

> Sudah ada ratusan plugin! Jelajahi [Perpustakaan _Plugin_](/plugins/) Gatsby.

Tujuan kami dengan adanya _plugin_ adalah membuatnya mudah untuk diinstal dan digunakan. Kemungkinan anda akan menggunakan _plugin_ di hampir setiap situs Gatsby yang anda bangun. Saat mengerjakan seluruh tutorial anda akan memiliki banyak kesempatan untuk berlatih memasang dan menggunakan _plugin_.

Untuk pengantar awal menggunakan plugin, anda akan menginstal dan mengimplementasikan plugin Gatsby untuk Typography.js.

[_Typography.js_](https://kyleamathews.github.io/typography.js/) adalah sebuah perpustakaan dari Javasript yang menghasilkan bentuk dasar tampilan dari _typography_ secara keseluruhan untuk situs anda. Perpustakaan ini memiliki sebuah [_plugin_ dari Gatsby yang sesuai](/packages/gatsby-plugin-typography/) yang mempermudah penggunaannya di situs Gatsby anda.

### ✋ Membuat sebuah situs baru menggunakan Gatsby

Seperti yang kami sebutkan di [bagian kedua](/tutorial/part-two/),pada titik ini alangkah baiknya dengan menutup jendela terminal yang tampil dan juga file dari tutorial sebelumnya, untuk menjaga semuanya tetap bersih pada bagian Desktop anda. lalu buka jendela terminal baru dan jalankan perintah berikut untuk membuat situs Gatsby baru didalam direktori yang disebut `tutorial-bagian-tiga` dan kemudian pindah ke direktori baru ini:

```shell
gatsby new tutorial-part-three https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-three
```

### ✋ Menambahkan dan konfigurasi `gatsby-plugin-typography`

Ada dua langkah utama untuk menggunakan _plugin_: Menambahkan dan konfigurasi.

1. Menambahkan _package_ dari _NPM_ `gatsby-plugin-typography`.

```shell
npm install --save gatsby-plugin-typography react-typography typography typography-theme-fairy-gates
```

> Catatan: _Typography.js_ memerlukan beberapa _packages_ tambahan, itu termasuk dalam instruksi. Persyaratan tambahan seperti ini akan tercantum dalam instruksi "_install_" dari masing-masing penggunaan _plugin_.

2. Lakukan perubahan pada file `gatsby-config.js` yang berada pada struktur bagian utama proyek anda dengan cara berikut:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`
      }
    }
  ]
}
```

`gatsby-config.js` adalah file khusus lain yang secara otomatis akan dikenali Gatsby. Di sinilah Anda perlu menambahkan _plugin_ dan konfigurasi situs lainnya.

> jika anda tertarik bisa kunjungi informasi lebih lanjut berikut ini, [dokumen mengenai gatsby-config.js](/docs/gatsby-config/).

3. _Typography.js_ memerlukan file untuk konfigurasi. Buatlah direktori baru bernama `utils` didalam direktori `src`. Kemudian tambahkan file baru bernama `typography.js` ke dalam direktori `utils` dan salin bagian berikut ke dalam file tersebut:

```javascript:title=src/utils/typography.js
import Typography from "typography"
import fairyGateTheme from "typography-theme-fairy-gates"

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```

4. Mulai jalankan server untuk pengembangan.

```shell
gatsby develop
```

Setelah Anda memuat situs, jika Anda memeriksa _HTML_ yang dihasilkan menggunakan alat pengembang _Chrome_, Anda akan melihat bahwa _plugin_ _typography_ menambahkan elemen `<style>` ke elemen `<head>` dengan CSS yang dihasilkannya:

![typography-styles](typography-styles.png)

### ✋ Buat beberapa perubahan konten dan gaya

Salin berikut ini ke dalam `src/pages/index.js` Anda sehingga dapat melihat
efek lebih baik dari CSS yang dihasilkan oleh `Typography.js`.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
)
```

Situs anda akan terlihat seperti berikut ini:

![no-layout](no-layout.png)

Mari kita lakukan perbaikan secara cepat. Banyak situs memiliki satu kolom teks yang berpusat di tengah halaman. Untuk membuat ini, tambahkan gaya berikut ke
`<div>` pada `src/pages/index.js`.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  // highlight-next-line
  <div style={{ margin: `3rem auto`, maxWidth: 600 }}>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </div>
)
```

![with-layout2](with-layout2.png)

Manis bukan. Anda telah berhasil menambahkan dan mengkonfigurasi _plugin_ Gatsby pertama Anda!

## Membuat komponen _layout_

Saatnya memulai belajar mengenai komponen-komponen dari _layout_. Agar siap untuk bagian ini, tambahkan beberapa halaman baru ke proyek Anda, seperti halaman _about_ dan halaman _contact_.

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div>
    <h1>About me</h1>
    <p>I’m good enough, I’m smart enough, and gosh darn it, people like me!</p>
  </div>
)
```

```jsx:title=src/pages/contact.js
import React from "react"

export default () => (
  <div>
    <h1>I'd love to talk! Email me at the address below</h1>
    <p>
      <a href="mailto:me@example.com">me@example.com</a>
    </p>
  </div>
)
```

Mari kita lihat seperti apa tampilan halaman yang baru:

![about-uncentered](about-uncentered.png)

Hmm. Akan lebih baik jika konten dari kedua halaman baru ini dipusatkan seperti halaman _index_. Dan akan lebih menyenangkan memiliki semacam navigasi global sehingga mudah bagi pengunjung untuk menemukan dan mengunjungi masing-masing sub-halaman.

Anda akan mulai mengatasi perubahan ini dengan membuat komponen _layout_ pertama Anda.

### ✋ Membuat komponen _layout_ pertama anda

1. Buat sebuah direktori baru pada `src/components`.

2. Buat komponen _layout_ yang sangat mendasar pada `src/components/layout.js`:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

3. Tambahkan komponen _layout_ yang baru ini ke dalam komponen halaman `src/pages/index.js` Anda:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout" // highlight-line

export default () => (
  <Layout> {/* highlight-line */}
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </Layout> {/* highlight-line */}
)
```

![with-layout2](with-layout2.png)

Manis bukan, _layout_-nya bekerja! Konten halaman _index_ Anda masih berada terpusat ditengah.

Namun cobalah menavigasi ke `/about/`, atau `/contact/`. Konten pada halaman-halaman tersebut masih tidak akan terpusat ditengah.

4. Tambahkan komponen _layout_ di `about.js` dan `contact.js` (seperti yang Anda lakukan untuk `index.js` pada langkah sebelumnya).

Konten ketiga halaman Anda terpusat ditengah berkat komponen _layout_ tunggal yang dibagikan ini!

### ✋ Menambahkan judul situs

1. Tambahkan baris berikut ke komponen _layout_ baru Anda:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    <h3>MySweetSite</h3> {/* highlight-line */}
    {children}
  </div>
)
```

Jika Anda membuka salah satu dari tiga halaman Anda, Anda akan melihat judul yang sama ditambahkan, misalnya halaman `/about/`:

![with-title](with-title.png)

### ✋ Tambahkan tautan navigasi antar halaman

1. Salin bagian berikut ini ke file komponen _layout_ Anda:

```jsx:title=src/components/layout.js
import React from "react"
// highlight-start
import { Link } from "gatsby"

const ListLink = props => (
  <li style={{ display: `inline-block`, marginRight: `1rem` }}>
    <Link to={props.to}>{props.children}</Link>
  </li>
)
// highlight-end

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    {/* highlight-start */}
    <header style={{ marginBottom: `1.5rem` }}>
      <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
        <h3 style={{ display: `inline` }}>MySweetSite</h3>
      </Link>
      <ul style={{ listStyle: `none`, float: `right` }}>
        <ListLink to="/">Home</ListLink>
        <ListLink to="/about/">About</ListLink>
        <ListLink to="/contact/">Contact</ListLink>
      </ul>
    </header>
    {/* highlight-end */}
    {children}
  </div>
)
```

![with-navigation2](with-navigation.png)

Dan tepat di sana Anda memilikinya! Ketiga halaman situs dengan dasar navigasi global.

_Tantangan:_ Dengan kekuatan "komponen _layout_" baru Anda, coba tambahkan _header_, _footer_, navigasi global, _sidebars_, dll ke situs Gatsby Anda!

## Apa yang akan terjadi selanjutnya?

Lanjutkan ke [tutorial bagian empat](/tutorial/part-four/) di mana Anda akan mulai belajar tentang lapisan data Gatsby dan membuat halaman secara pemrograman!

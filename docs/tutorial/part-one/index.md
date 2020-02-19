---
title: Kenali *Bulding Blocks* Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

Pada [**bagian sebelumnya**](/tutorial/part-zero/), Anda telah menyiapkan lingkungan pengembangan lokal Anda dengan memasang perangkat lunak yang diperlukan dan membuat situs Gatsby pertama Anda menggunakan [**starter “hello world”**](https://github.com/gatsbyjs/gatsby-starter-hello-world). Sekarang, coba selami lebih dalam kode yang dihasilkan oleh starter itu

## Menggunakan starter Gatsby

Pada [**tutorial bagian nol**](/tutorial/part-zero/), Anda telah membuat sebuah situs baru berdasarkan starter “hello world” menggunakan perintah berikut:

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

Ketika membuat sebuah situs Gatsby baru, kamu menggunakan perintah struktur berikut untuk membuat sebuah situs baru berdasarkan setiap starter Gatsby yang ada:

```shell
gatsby new [NAMA_DIREKTORI_SITUS] [URL_DARI_STARTER_RESITORI_GITHUB]
```

Jika Anda menghilangkan URL dari bagian akhir, Gatsby akan secara otomatis menghasilkan situs untuk Anda berdasarkan pada [**starter standar**](https://github.com/gatsbyjs/gatsby-starter-default). Untuk bagian tutorial ini, tetap dengan situs “Hello World” yang sudah Anda buat di tutorial bagian nol

### ✋ Buka kodenya

Di editor kode Anda, buka kode yang dibuat untuk situs “Hello World” Anda dan lihat berbagai direktori dan berkas yang terdapat dalam direktori ‘hello-world’. Seharusnya terlihat seperti ini:

![Proyek Hello World project pada VS Code](01-hello-world-vscode.png)

_Catatan: Sekali lagi, editor yang ditampilkan di sini adalah Visual Studio Code. Jika Anda menggunakan editor yang berbeda, itu akan terlihat sedikit berbeda._

Mari kita lihat kode yang memberdayakan beranda.

> 💡 Jika Anda menghentikan server pengembangan setelah menjalankan `gatsby develop` di bagian sebelumnya, mulai lagi sekarang — saatnya untuk membuat beberapa perubahan pada situs hello-world!

## Membiasakan dengan halaman Gatsby

Buka direktori `/src` di editor kode Anda. Di dalamnya ada satu direktori: `/pages`.

Buka berkas di `src/pages/index.js`. Kode dalam berkas ini membuat komponen yang berisi satu div dan beberapa teks — dengan tepat, “Hello world!”

### ✋ Buat perubahan pada beranda “Hello World”

1. Ubah teks “Hello World!” Menjadi “Hello Gatsby!” dan simpan berkas tersebut. Jika windows Anda bersebelahan, Anda dapat melihat bahwa perubahan kode dan konten Anda tercermin hampir secara instan di browser setelah Anda menyimpan berkas.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./02-demo-hot-reloading.mp4"></source>
  <p>Sorry! Your browser doesn't support this video.</p>
</video>

> 💡 Gatsby menggunakan **hot reload** untuk mempercepat proses pengembangan Anda. Pada dasarnya, ketika Anda menjalankan server pengembangan Gatsby, berkas situs Gatsby sedang “diawasi” di latar belakang — setiap kali Anda menyimpan berkas, perubahan Anda akan segera tercermin di browser. Anda tidak perlu me-refresh halaman atau memulai kembali server pengembangan — perubahan Anda baru saja muncul.

2. Sekarang Anda dapat membuat perubahan Anda sedikit lebih terlihat. Coba ganti kode pada `src/pages/ index.js` dengan kode di bawah ini dan simpan lagi. Anda akan melihat perubahan pada teks — warna teks akan menjadi ungu dan ukuran font akan lebih besar.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
)
```

> 💡 Kami akan membahas lebih lanjut tentang penataan style di Gatsby pada [**bagian dua**](/tutorial/part-two/) tutorial.

3.  Hapus penataan ukuran font, ubah teks “Hello Gatsby!” Ke tajuk tingkat-satu, dan tambahkan paragraf di bawah tajuk.

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  {/* highlight-start */}
  <div style={{ color: `purple` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
  {/* highlight-end */}
  </div>
)
```

![Lebih banyak perubahan dengan hot reload](03-more-hot-reloading.png)

4.  Tambahkan gambar. (Dalam hal ini, gambar acak dari Unsplash).

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <div style={{ color: `purple` }}>
    <h1>Hello Gatsby!</h1>
    <p>What a world.</p>
    {/* highlight-next-line */}
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

![Tambah Gambar](04-add-image.png)

### Tunggu… HTML di JavaScript kami?

_Jika Anda terbiasa dengan React dan JSX, silakan lewati bagian ini._ Jika Anda belum pernah bekerja dengan React framework sebelumnya, Anda mungkin bertanya-tanya apa yang dilakukan HTML dalam fungsi JavaScript. Atau mengapa kami mengimpor `react` pada baris pertama tetapi tampaknya tidak menggunakannya di mana pun. Hibrida “HTML-in-JS” ini sebenarnya merupakan ekstensi sintaks dari JavaScript, untuk React, disebut JSX. Anda dapat mengikuti tutorial ini tanpa pengalaman sebelumnya dengan React, tetapi jika Anda ingin tahu, inilah primer singkatnya…

Pertimbangkan konten asli dari berkas `src/pages/index.js`:

```jsx:title=src/pages/index.js
import React from "react"

export default () => <div>Hello world!</div>
```

Dalam JavaScript murni, tampilannya seperti ini:

```javascript:title=src/pages/index.js
import React from "react"

export default () => React.createElement("div", null, "Hello world!")
```

Sekarang Anda dapat melihat penggunaan impor `'react'`! Tapi tunggu. Anda sedang menulis JSX, bukan HTML dan JavaScript murni. Bagaimana peramban membacanya? Jawaban singkatnya: Tidak. Situs Gatsby hadir dengan alat bantu yang telah diatur untuk mengubah kode sumber Anda menjadi sesuatu yang dapat ditafsirkan oleh peramban.

## Membangun dengan komponen

Beranda yang baru saja Anda edit dibuat dengan mendefinisikan komponen halaman. Apa sebenarnya "komponen" itu?

Didefinisikan secara luas, komponen adalah *building blocks* untuk situs Anda; Ini adalah potongan kode mandiri yang menggambarkan bagian UI (antarmuka pengguna).

Gatsby dibangun di atas React. Ketika kita berbicara tentang menggunakan dan mendefinisikan **komponen**, kita benar-benar berbicara tentang **Komponen React** - potongan kode mandiri (biasanya ditulis dengan JSX) yang dapat menerima input dan mengembalikan elemen React menggambarkan bagian dari UI.

Salah satu perubahan mental besar yang Anda buat ketika mulai membangun dengan komponen (jika Anda sudah menjadi pengembang) adalah sekarang CSS, HTML, dan JavaScript Anda digabungkan secara erat dan sering kali bahkan dalam berkas yang sama.

Sementara perubahan yang tampaknya sederhana, ini memiliki implikasi yang mendalam tentang bagaimana Anda berpikir tentang membangun situs web.

Ambil contoh membuat button khusus. Di masa lalu, Anda akan membuat class CSS (mungkin `.primary-button`) dengan style khusus Anda dan kemudian menggunakannya kapan pun Anda ingin menerapkan style tersebut. Sebagai contoh:

```html
<button class="primary-button">Click me</button>
```

Di dunia komponen, Anda malah membuat komponen `PrimaryButton` dengan style button Anda dan menggunakannya di seluruh situs Anda seperti:

<!-- prettier-ignore -->
```jsx
<PrimaryButton>Click me</PrimaryButton>
```

Komponen menjadi *building blocks* dasar situs Anda. Alih-alih dibatasi pada *building blocks* yang disediakan peramban, misal `<button />`, Anda dapat dengan mudah membuat blok baru yang secara elegan memenuhi kebutuhan proyek Anda.

### ✋ Menggunakan komponen halaman

Setiap komponen React yang didefinisikan dalam `src/pages/*.js` akan secara otomatis menjadi halaman. Mari kita lihat aksi ini.

Anda sudah memiliki berkas `src/pages/index.js` yang disertakan dengan starter “Hello World”. Mari kita buat halaman about.

1. Buat berkas baru di `src/pages/about.js`, salin kode berikut ke berkas baru, dan simpan.

```jsx:title=src/pages/about.js
import React from "react"

export default () => (
  <div style={{ color: `teal` }}>
    <h1>About Gatsby</h1>
    <p>Such wow. Very React.</p>
  </div>
)
```

2.  Navigasi ke http://localhost:8000/about/.

![Halaman about yang baru](05-about-page.png)

Hanya dengan meletakkan komponen React dalam berkas `src/pages/about.js`, Anda sekarang memiliki halaman yang dapat diakses di `/about`.

### ✋ Menggunakan sub-komponen

Katakanlah beranda dan halaman about keduanya menjadi cukup besar dan Anda menulis ulang banyak hal. Anda dapat menggunakan sub-komponen untuk memecah UI menjadi bagian yang dapat digunakan kembali. Kedua halaman Anda memiliki tajuk `<h1>` — buat komponen yang akan menjelaskan `Header`.

1.  Buat direktori baru di `src/components` dan berkas di dalam direktori itu bernama `header.js`.
2.  Tambahkan kode berikut ke berkas `src/components/header.js` yang baru.

```jsx:title=src/components/header.js
import React from "react"

export default () => <h1>This is a header.</h1>
```

3.  Ubah berkas `about.js` untuk mengimpor komponen `Header`. Ganti markup `h1` dengan `<Header />`:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header" // highlight-line

export default () => (
  <div style={{ color: `teal` }}>
    <Header /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Menambahkan komponen Header](06-header-component.png)

Di peramban, teks header “About Gatsby” sekarang harus diganti dengan “This is a header.” Tapi Anda tidak ingin halaman “About” mengatakan “This is a header.” Anda ingin mengatakan, “About Gatsby”.

4.  Kembali ke `src/components/header.js` dan buat perubahan berikut:

```jsx:title=src/components/header.js
import React from "react"

export default props => <h1>{props.headerText}</h1> {/* highlight-line */}
```

5.  Kembali ke `src/pages/about.js` dan buat perubahan berikut:

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="About Gatsby" /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Mengirimkan data ke header](07-pass-data-header.png)

Sekarang Anda akan melihat teks header “About Gatsby” Anda lagi!

### Apa itu “props”?

Sebelumnya Anda mendefinisikan komponen React sebagai bagian dari kode yang dapat digunakan kembali yang menggambarkan UI. Untuk membuat potongan-potongan yang dapat digunakan kembali ini dinamis, Anda harus dapat menyediakannya dengan data yang berbeda. Anda melakukannya dengan input yang disebut “props”. Props adalah (cukup tepat) properti yang disediakan untuk komponen React.

Di `about.js` Anda mengirimkan prop `headerText` dengan nilai `"About Gatsby"` ke sub-komponen `Header` yang diimpor:

```jsx:title=src/pages/about.js
<Header headerText="About Gatsby" />
```

Di dalam `header.js`, komponen header akan menerima prop `headerText` (karena Anda telah menuliskan itu). Jadi Anda dapat mengaksesnya seperti ini:

```jsx:title=src/components/header.js
<h1>{props.headerText}</h1>
```

> 💡 Di JSX, Anda dapat menanamkan ekspresi JavaScript apa pun dengan membungkusnya dengan `{}`. Ini adalah bagaimana Anda dapat mengakses properti `headerText` (atau “prop!”) Dari objek “props”.

Jika Anda telah memberikan properti lain ke komponen `<Header />` Anda, seperti...

```jsx:title=src/pages/about.js
<Header headerText="About Gatsby" arbitraryPhrase="is arbitrary" />
```

...Anda juga dapat mengakses prop `arbitraryPhrase`: `{props.arbitraryPhrase}`.

6. Untuk menekankan bagaimana ini membuat komponen Anda dapat digunakan kembali, tambahkan komponen `<Header />` tambahan ke halaman about, tambahkan kode berikut ke berkas `src/pages/about.js`, dan simpan.

```jsx:title=src/pages/about.js
import React from "react"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Header headerText="About Gatsby" />
    <Header headerText="It's pretty cool" /> {/* highlight-line */}
    <p>Such wow. Very React.</p>
  </div>
)
```

![Duplikasi header untuk menunjukkan penggunaan kembali](08-duplicate-header.png)

Dan di sana Anda memilikinya; Header kedua - tanpa menulis ulang kode apa pun - dengan mengirimkan data yang berbeda menggunakan props.

### Menggunakan komponen tata letak

Komponen tata letak adalah untuk bagian dari situs yang ingin Anda bagikan di banyak halaman. Misalnya, situs Gatsby biasanya memiliki komponen tata letak dengan header dan footer bersama. Hal-hal umum lainnya untuk ditambahkan ke tata letak termasuk bilah sisi dan/atau menu navigasi.

Anda akan menjelajahi komponen tata letak pada [**bagian tiga**](/tutorial/part-three/).

## Menghubungkan antar halaman

Anda akan sering ingin menghubungkan antar halaman — Mari kita lihat routing di situs Gatsby.

### ✋ Menggunakan komponen `<Link />`

1.  Buka komponen halaman index (`src/pages/index.js`), impor komponen `<Link /> ` dari Gatsby, tambahkan komponen `<Link />` di atas header, dan berikan properti `to` dengan nilai `"/contact/"` untuk pathname:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby" // highlight-line
import Header from "../components/header"

export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Contact</Link> {/* highlight-line */}
    <Header headerText="Hello Gatsby!" />
    <p>What a world.</p>
    <img src="https://source.unsplash.com/random/400x200" alt="" />
  </div>
)
```

Ketika Anda mengklik tautan "Contact" baru di beranda, Anda akan melihat ...

![Halaman pengembangan Gatsby 404](09-dev-404.png)

... halaman pengembangan Gatsby 404. Mengapa? Karena Anda mencoba menautkan ke halaman yang belum ada.

2.  Sekarang Anda harus membuat komponen halaman untuk halaman "Contact" baru Anda di `src/pages/contact.js` dan minta tautannya kembali ke beranda:

```jsx:title=src/pages/contact.js
import React from "react"
import { Link } from "gatsby"
import Header from "../components/header"

export default () => (
  <div style={{ color: `teal` }}>
    <Link to="/">Home</Link>
    <Header headerText="Contact" />
    <p>Send us a message!</p>
  </div>
)
```

Setelah Anda menyimpan berkas, Anda harus melihat halaman contact dan dapat menghubungkannya dengan beranda.

<video controls="controls" loop="true">
  <source type="video/mp4" src="./10-linking-between-pages.mp4"></source>
  <p>Sorry! Your browser doesn't support this video.</p>
</video>

Komponen Gatsby `<Link />` untuk menghubungkan antar halaman di dalam situs Anda. Untuk tautan eksternal ke halaman yang tidak ditangani oleh situs Gatsby Anda, gunakan tag HTML `<a>` biasa.

## Men-deploy situs Gatsby

Gatsby.js adalah _generator situs modern_, yang berarti tidak ada server untuk men-setup atau basis data rumit untuk digunakan. Sebagai gantinya, perintah Gatsby `build` menghasilkan direktori file HTML dan JavaScript statis yang dapat Anda gunakan untuk layanan hosting situs statis.

Coba gunakan [Surge](http://surge.sh/) untuk men-deploy situs web Gatsby pertama Anda. Surge adalah salah satu dari banyak "static site hosts" yang memungkinkan untuk men-deploy situs Gatsby.

Jika sebelumnya Anda belum memasang &amp; mengatur Surge, buka jendela terminal baru dan instal alat baris perintah mereka:

```shell
npm install --global surge

# Lalu buat akun (gratis)
surge login
```

Selanjutnya, buat situs Anda dengan menjalankan perintah berikut di terminal di root situs Anda (tip: pastikan Anda menjalankan perintah ini di root situs Anda, dalam hal ini di folder hello-world, yang Anda bisa lakukan dengan membuka tab baru di jendela yang sama dengan yang Anda gunakan untuk menjalankan `gatsby develop`):

```shell
gatsby build
```

Proses build mungkin memakan waktu 15-30 detik. Setelah build selesai, sangat menarik untuk melihat berkas-berkas yang baru saja disiapkan oleh perintah `gatsby build`.

Lihatlah daftar berkas yang dihasilkan dengan mengetikkan perintah terminal berikut ke root situs Anda, yang akan memungkinkan Anda melihat direktori `public`:

```shell
ls public
```

dan terakhir deploy situs Anda dengan menerbitkan berkas yang dihasilkan ke surge.sh.

```shell
surge public/
```

Setelah ini selesai berjalan, Anda akan melihat sesuatu di terminal Anda seperti:

![Tangkapan layar penerbitan situs Gatsby dengan Surge](surge-deployment.png)

Buka alamat web yang terdaftar di baris terbawah (`lowly-pain.surge.sh` dalam hal ini) dan Anda akan melihat situs Anda yang baru diterbitkan! Kerja bagus!

## ➡️ Apa Selanjutnya?

Di bagian ini Anda:

- Belajar tentang starter Gatsby, dan cara menggunakannya untuk membuat proyek baru
- Belajar tentang sintaks JSX
- Belajar tentang komponen
- Mempelajari tentang komponen dan sub-komponen halaman Gatsby
- Belajar tentang "props" React dan menggunakan kembali komponen React

Sekarang, lanjut ke [** menambahkan style ke situs Anda **](/tutorial/part-two/)!

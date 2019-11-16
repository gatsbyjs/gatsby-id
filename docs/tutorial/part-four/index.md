---
judul : Data di Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

Selamat datang di panduan bagian 4 ! Setengah jalan ! Semoga semuanya dimulai dengan perasaan menggembirakan

## Ringkasan dari setengah bagian pertama dari panduan

Sejauh ini, anda telah belajar bagaimana menggunakan React.js betapa bergunanya hal tersebut untuk membuat komponenmu sendiri sehingga dapat membuat blok bangunan untuk websites

Anda juga telah menjelajahi komponen-komponen desain menggunakan modul CSS

## Apa yang ada didalam panduan ini ?

Dalam 4 bagian selanjutnya dari panduan ini(termasuk ini), anda akan mendalami lapisan data Gatsby, yang mana merupakan fitur yang sangat kuat dari Gatsby yang memungkinkan anda secara mudah membuat situs dari Markdown, Wordpress, headless CMSsm dan berbagai sumber data lainnya.

*Catatan* layer data Gatsby dipersembahkan oleh GraphQL. Untuk panduan yang lebih mendalam tentang GraphQL, kami merekomendasikan [bagaimana caranya GraphQL](https://www.howtographql.com/). 

## Data di Gatsby

Sebuah website mempunyai empat bagian : HTML, CSS, JS dan data. Bagian awal dari panduan ini memfokuskan pada HTML, CSS dan JS. Sekarang mari belajar bagaimana caranya menggunakan data di Gatsby

** Apakah data itu?**

Kebanyakan pegiat komputer akan menjawab seperti ini : data merupakan hal yang seperti "strings". bilangan bulat ('42'). objek ('{pizza: true}'), dsb

Untuk tujuan pekerjaan di Gatsby, namun, jawaban yang lebih tepat adalah "segala sesuatu hidup diluar komponen react"

Sejuah ini, anda telah menulis teks dan menambahkan gambar secara langsung dalam komponen. Yang mana hal tersebut merupakan langkah yang luar biasa untuk membangun kebanyakan website. Tetapi, sering kali anda ingin menyimpan data diluar komponen dan kemudian membawa data ke dalam komponen sesuai kebutuhan anda.

Jika anda membangun sebuah situs dengan Wordpress (sehingga kontributor lain memiliki antarmuka yang bagus untuk menambahkan dan memelihara konten) dan Gatsby, data untuk situs (halaman dan kiriman) ada dalam WordPress sehingga anda dapat melakukan Pull data tersebut sesuai kebutuhan, dalam komponen anda.

Data juga dapat digunakan dalam jenis file seperti Markdown, CSV, dsb. sebaik database dan segala macam API

** Layer data Gatsby memungkinkan anda menarik data dari sini ( dan sumber lainnya) secara langsung kedalam komponen anda** dalam bentuk dan kondisi yang anda inginkan

## Menggunakan data tak tersetruktur Vs GraphQL

### Haruskah saya menggunakan GraphQL dan sumber plugin untuk menarik data ke dalam situs Gatsby ?

Tentu tidak ! Anda dapat menggunakan node API 'createPages' untuk menarik data tak tersruktur ke dalam halaman Gatsby secara langsung, daripada melalui data layer GraphQL. Ini adalah pilihan yang bagus untuk situs kecil, sementara GraphQL dan sumber-sumber plugin dapat mempersingkat waktu dengan situs yang lebih kompleks

Lihat [Menggunakan Gatsby tanpa GraphQL](/docs/Menggunakan Gatsby tanpa GraphQL/) panduan untuk belajar bagaimana menarik data ke dalam situs Gatsby anda menggunakan node API 'membuat halaman' dan untuk melihat contoh situs

### kapan saya menggunakan data tak tersetruktur Vs GraphQL?

Jika anda membuat situs kecil, salah satu cara yang efisien untuk membuat situs yaitu dengan menarik data tak tersetruktur seperti yang diuraikan di paduan ini, menggunakan API 'createPages' dan jika situsnya menjadi lebih kompleks, anda beralih membangun situs yang lebih kompleks  atau anda suka mentransformasikan data, ikuti langkah berikut:

1. Periksa [Perpustakaan plugin](/plugind/) untuk melihat jika sumber dan atau tranformasi plugin yang anda suka untuk digunakan sudah ada
2. Jika belum ada, baca [Pembuatan plugin](/docs/creating-plugins/) buatlah sesuai keinginan anda.

### Bagaimana layer data Gatsby menggunakan GraphQL untuk menarik data ke dalam komponen

Ada beberapa pilihan untuk memuat data ke komponen react. Salah satu yang paling populer dan paling berguna adalah teknologi yang dinamakan [GraphQL](http://graphql.org/) 

GraphQL ditemukan pada Facebook untuk membantu teknisi produksi menarik data yang dibutuhkan ke komponen

GraphQL adalah q atau query dan l atau languege yang artinya bahasa permintaan. Jika anda familiar dengan SQL, graphQL juga memiliki cara kerja yang sama. Menggunakan sebuah syntax khusus, anda menggambarkan data yang anda inginkan dalam komponen anda dan kemudian data itu diberikan kepadamu

Gatsby menggunakan GraphQL untuk memungkinkan komponen untuk mendeklarasikan data yang mereka inginkan

## Membuat sebuah contoh situs

Buat situs baru yang lain untuk tutorial ini. anda akan membangun sebuah blog Markdown yang dinamakan "Panda Banyak Makan", situs itu didedikasikan untuk memnunjukkan gambar dan video terbaik dari berbagai makanan panda. Sepanjang jalan, anda akan mendalami GraphQL dan dengan dukungan dari Gatsby Markdown. 

Buka sebuah jendela tutorial baru dan ikuti sejumlah penrintah untuk membuat situs Gatby baru dalam sebuah arahan yang bernama "panduan bagian empat". kemudian navigasikan ke direktori yang baru.

```shell
gatsby new tutorial-part-four https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-four
```

Kemudian pasang beberapa hal dibutuhkan lainmya pada bagian yang sama pada folder projek anda. Anda akan menggunakan tema tipografi 'Kirkham' dan anda akan mencoba sebuah pustakan CSS-in-JS, ["emotion]((https://emotion.sh/))  


```shell
npm install --save gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/core
```
Persiapkan sebuah situs yang sama dengan apa yang anda butuhkan  di [Bagian Empat](/tutorial/part-three) Situs ini akan mempunyai komponen layout dan dua halaman komponen.

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
import { Link } from "gatsby"

import { rhythm } from "../utils/typography"

export default ({ children }) => (
  <div
    css={css`
      margin: 0 auto;
      max-width: 700px;
      padding: ${rhythm(2)};
      padding-top: ${rhythm(1.5)};
    `}
  >
    <Link to={`/`}>
      <h3
        css={css`
          margin-bottom: ${rhythm(2)};
          display: inline-block;
          font-style: normal;
        `}
      >
        Pandas Eating Lots
      </h3>
    </Link>
    <Link
      to={`/about/`}
      css={css`
        float: right;
      `}
    >
      About
    </Link>
    {children}
  </div>
)
```

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>Amazing Pandas Eating Things</h1>
    <div>
      <img
        src="https://2.bp.blogspot.com/-BMP2l6Hwvp4/TiAxeGx4CTI/AAAAAAAAD_M/XlC_mY3SoEw/s1600/panda-group-eating-bamboo.jpg"
        alt="Group of pandas eating bamboo"
      />
    </div>
  </Layout>
)
```

```jsx:title=src/pages/about.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <h1>About Pandas Eating Lots</h1>
    <p>
      We're the only site running on your computer dedicated to showing the best
      photos and videos of pandas eating lots of food.
    </p>
  </Layout>
)
```

```javascript:title=src/utils/typography.js
import Typography from "typography"
import kirkhamTheme from "typography-theme-kirkham"

const typography = new Typography(kirkhamTheme)

export default typography
export const rhythm = typography.rhythm
```

`gatsby-config.js`(Harus di bagian utama folder projek anda, bukan dibawah src)

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Tambahkan file diatas dan jalankan `gatsby develop`, seperti biasa dan anda harus mengikuti langkah berikut:

![mulai](start.png)
Anda mempunyai situs kecil lain dengan sebuah tata letak dan dua buah halaman

Sekarang anda dapat memulai berquery

## GraphQL query pertama anda

Ketika membuat situs, anda kemungkinan ingin menggunakan kembali beberapa data seperti judul situs contohnya. Lihat pada halaman '/about/'. Anda akan memperhatikan bahwa anda memiilki judul situs ('Panda banyak makan) di kedua tata letak komponen (kepala situs) serta di '<h1 />' dari halaman'about.js (kepala halaman)

Tetapi bagaimana jika amda ingin mengubah judul situs pada kemudian hari? Anda harus mencari judul di semua komponen dan mengedit setiap contohnya. Ini rumit dan rawan kesalahan, terlebih jika lebih besar seperti situs yang lebih kompleks. Sebagai gantinya, anda dapat menyimpan judul di suatu lokasi dan referensikan lokasi tersebut ke file yang lain, ubah judul dalam satu tempat yang sama dan Gatsby akan _pull_ judul terbaru ke file referensi tersebut.

Sebuah tempat untuk sekumpulan bit data ini adalah 'siteMetadata' sebuah objek di file 'gatsby-config.js'. Tambahkan judul situs anda ke file 'gatsby-config.js'

```javascript:title=gatsby-config.js
module.exports = {
  // highlight-start
  siteMetadata: {
    title: `Judul dari siteMetadata`,
  },
  // highlight-end
  plugins: [
    `gatsby-plugin-emotion`,
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```

Jalankan ulang server pengembangan

### Gunakan sebuah halaman query

Sekarang judul situs tersedia untuk diquerykan; tambahkan hal itu ke file 'about.js' menggunakan [halaman query](/docs/page-query): 

```jsx:title=src/pages/about.js
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Layout from "../components/layout"

// highlight-next-line
export default ({ data }) => (
  <Layout>
    <h1>About {data.site.siteMetadata.title}</h1> {/* highlight-line */}
    <p>
      Kami satu-satunya situs yang ada dikomputer anda yang didedikasikan untuk menunjukkan foto dan video terbaik dari panda yang banyak memakan
    </p>
  </Layout>
)

// highlight-start
export const query = graphql`
  query {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end
```
Itu Berhasil

[Judul halaman ditarik dari sitemetadata](site-metadata-title.png)

GraphQL query dasar yang mengambil 'judul' di 'about.js' milikmu , maka perubahanmya menjadi
```graphql:title=src/pages/about.js

{
  site {
    siteMetadata {
      title
    }
  }
}
```

> 💡 In Pada [bagian lima](/tutorial/part-five/#introducing-graphiql), anda akan menemui sebuah alat yang memungkinkan kita secara interaktiv menjelajahi data yang tersedia melalui GraphQL dan membantu memformulasikan query seperti diatas.

Halaman query di luar dari definisi komponen == oleh konvensi pada akhir halaman file komponen -- hanya tersedia di halaman komponen.

### Menggunakan sebuah Query statis

[Querystatis] (/docs/static-query/) adalah sebuah API baru diperkenalkan di Gatsby versi 2 yang mana memungkinkan selain halaman komponen (seperti komponen 'layout.js' anda), untuk mengambil data menggunakan query GraphQL. Mari gunakan itu untuk memperkenalkan versi terkait ['useStaticQuery'](/docs/use-static-query/). 

Lanjutkan dan buat beberapa perubahan ke file 'src/components/layout.js' anda untuk menggunakan kaitan 'usestaticquery' dan sebuah '[data.site.siteMetadata.title]` referensikan penggunaan tersebut pada data ini. Ketika sudah selesai. file anda akan menjadi seperti ini :  

```jsx:title=src/components/layout.js
import React from "react"
import { css } from "@emotion/core"
// highlight-next-line
import { useStaticQuery, Link, graphql } from "gatsby"

import { rhythm } from "../utils/typography"
// highlight-start
export default ({ children }) => {
  const data = useStaticQuery(
    graphql`
      query {
        site {
          siteMetadata {
            title
          }
        }
      }
    `
  )
  return (
    // highlight-end
    <div
      css={css`
        margin: 0 auto;
        max-width: 700px;
        padding: ${rhythm(2)};
        padding-top: ${rhythm(1.5)};
      `}
    >
      <Link to={`/`}>
        <h3
          css={css`
            margin-bottom: ${rhythm(2)};
            display: inline-block;
            font-style: normal;
          `}
        >
          {data.site.siteMetadata.title} {/* highlight-line */}
        </h3>
      </Link>
      <Link
        to={`/about/`}
        css={css`
          float: right;
        `}
      >
        About
      </Link>
      {children}
    </div>
    // highlight-start
  )
}
// highlight-end
```

Kesuksesan Lainnya....🎉

![Judul halaman dan judul layout keduanya diambil dari siteMetadata](site-metadata-two-titles.png)
Kenapa menggunakan dua query yang berbeda disini? Contoh ini menjelaskan secara singkat jenis jenis query, bagaimana formatnya dan dimana dapat digunakan. Untuk sekarang, simpan dalam pikiranmu bahwa hanya halaman yang dapat membuat halaman query. Selain komponen, tata letak dapat menggunakan query statis. tutorial [Bagian 7](/tutorial/part-seven/) yang mana menjelaskan hal tersebut secara mendalam.

Tapi ayo kembali ke judul sesungguhnya

Salah satu prinsip utama dari Gatsby adalah _kreator membutuhkan koneksi sesegera mungkin ke apa saja yang mereka buat_ [hat tip to Bret Victor](http://blog.ezyang.com/2012/02/transcript-of-inventing-on-principle/)). Dengan kata lain, ketika anda membuat beberapa perubahan kode anda harus sesegera mungkin melihat efek dari perubahan tersebut. Anda memanipulasikan masukan dari Gatsby dan dapat melihat perubahan tampilan yang ditampilkan di layar. 

Hampir dimana mana, perubahan yang anda buat akan sesegera mungkin berpengaruh. Edit file 'gatsby-config.js' lagi. kali ini rubah 'judul' kembali ke 'panda banyak makan'. Seharunya perubahannya sangat cepat di situs anda.

![Kedua judul mengatakan panda banyak makan](pandas-eating-lots-titles.png)

|## apa selanjutnya ?

Selanjutnya, anda akan mempelajari tentang bagaimana menarik data ke situs Gatsby anda menggunakan GraphQL dengan sumber plugin di tutorial [bagian lima](/tutorial/part-five/) 
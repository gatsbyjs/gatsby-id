---
title: Transformer plugins
typora-copy-images-to: ./
disableTableOfContents: true
---

> Tutorial ini adalah bagian dari seri tentang lapisan data Gatsby. Pastikan Anda telah membaca [bagian 4](/tutorial/part-four/) dan [bagian 5](/tutorial/part-five/) terlebih dahulu sebelum melanjutkan tutorial ini.

## Apa yang ada pada tutorial ini?

Tutorial sebelumnya menunjukkan bagaimana *source plugins* membawa data _kedalam_ sistem data Gatsby. Dalam tutorial ini, Anda akan belajar bagaimana *plugins _transform_* _mengubah_ konten mentah yang dibawa oleh *source plugins*. Kombinasi *source plugins* dan *transformer plugins* dapat menangani semua sumber data dan transformasi data yang mungkin Anda perlukan saat membangun situs Gatsby.

## *Transformer plugins*

Seringkali, format data yang Anda dapatkan dari *source plugins* tidak seperti yang Anda ingin gunakan untuk
membangun situs web Anda. Sistem file pada *source plugins* memungkinkan Anda melakukan *query* data
pada file tetapi bagaimana jika Anda ingin meminta data _didalam_ file?

Untuk memungkinkan ini, Gatsby mendukung *transformer plugins* yang menggunakan konten mentah
dari *source plugins* dan _mengubahnya_ menjadi sesuatu yang lebih bermanfaat.

Misalnya, file markdown. Markdown bagus untuk menulis tetapi ketika Anda membangun
laman dengan itu, Anda perlu markdown menjadi HTML.

Tambahkan file markdown ke situs Anda di
`src/pages/sweet-pandas-eating-sweets.md` (Ini akan menjadi markdown *blog post*
pertama Anda) dan pelajari cara mentransformasikannya ke HTML menggunakan *transformer plugins* dan
GraphQL.

```markdown:title=src/pages/sweet-pandas-eating-sweets.md
---
title: "Sweet Pandas Eating Sweets"
date: "2017-08-10"
---

Pandas are really sweet.

Here's a video of a panda eating sweets.

<iframe width="560" height="315" src="https://www.youtube.com/embed/4n0xNbfJLR8" frameborder="0" allowfullscreen></iframe>
```

Setelah Anda menyimpan file, lihat `/my-files/` kembali—file markdown baru berada di
konten. Ini adalah fitur yang sangat kuat dari Gatsby. Seperti contoh
`siteMetadata` tadi, *source plugins* dapat me-*live-reload* data.
`gatsby-source-filesystem` selalu memindai file baru untuk ditambahkan dan kapan
itu akan menjalankan kembali *queries* Anda.

Tambahkan *transformer plugin* yang dapat mengubah file markdown:

```shell
npm install --save gatsby-transformer-remark
```

Kemudian tambahkan ke `gatsby-config.js` seperti biasa:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    `gatsby-transformer-remark`, // highlight-line
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

Mulai ulang server pengembangan lalu *refresh* (atau buka lagi) GraphiQL dan lihat 
*autocomplete*-nya:

![markdown-autocomplete](markdown-autocomplete.png)

Pilih `allMarkdownRemark` lagi dan jalankan seperti yang Anda lakukan untuk `allFile`. Anda akan
melihat di sana file markdown yang baru Anda tambahkan. Jelajahi *fields* yang
tersedia di *node* `MarkdownRemark`.

![markdown-query](markdown-query.png)

Baik! Semoga, beberapa dasar tersebut mulai menuju tempatnya. *Source plugins* membawa
data _ke_ sistem data Gatsby dan _transformer_ *plugins* mengubah konten mentah
yang dibawa oleh *source plugins*. Pola ini dapat menangani semua sumber data dan
transformasi data yang mungkin Anda perlukan saat membangun situs Gatsby.

## Buat daftar file markdown Anda di `src/pages/index.js`

Sekarang Anda harus membuat daftar file markdown di halaman depan. Seperti kebanyakan
blog, Anda ingin berakhir dengan daftar tautan di halaman depan yang menunjuk ke masing-masing
blog *posting*. Dengan GraphQL Anda dapat melakukan _query_ untuk daftar blog markdown saat ini
sehingga Anda tidak perlu mempertahankan daftar secara manual.

Seperti dengan halaman `src/pages/my-files.js`, ganti `src/pages/index.js` dengan
contoh berikut ini untuk menambahkan permintaan GraphQL dengan beberapa HTML awal dan *styling*.

```jsx:title=src/pages/index.js
import React from "react"
import { graphql } from "gatsby"
import { css } from "@emotion/core"
import { rhythm } from "../utils/typography"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      <div>
        <h1
          css={css`
            display: inline-block;
            border-bottom: 1px solid;
          `}
        >
          Amazing Pandas Eating Things
        </h1>
        <h4>{data.allMarkdownRemark.totalCount} Posts</h4>
        {data.allMarkdownRemark.edges.map(({ node }) => (
          <div key={node.id}>
            <h3
              css={css`
                margin-bottom: ${rhythm(1 / 4)};
              `}
            >
              {node.frontmatter.title}{" "}
              <span
                css={css`
                  color: #bbb;
                `}
              >
                — {node.frontmatter.date}
              </span>
            </h3>
            <p>{node.excerpt}</p>
          </div>
        ))}
      </div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allMarkdownRemark {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          excerpt
        }
      }
    }
  }
`
```

Sekarang halaman depan akan terlihat seperti:

![frontpage](frontpage.png)

Tapi satu blog *post* Anda terlihat agak sepi. Jadi mari kita tambahkan satu lagi di
`src/pages/pandas-and-bananas.md`

```markdown:title=src/pages/pandas-and-bananas.md
---
title: "Pandas and Bananas"
date: "2017-08-21"
---

Do Pandas eat bananas? Check out this short video that shows that yes! pandas do
seem to really enjoy bananas!

<iframe width="560" height="315" src="https://www.youtube.com/embed/4SZl1r2O_bY" frameborder="0" allowfullscreen></iframe>
```

![two-posts](two-posts.png)

Yang dimana terlihat hebat! Kecuali… urutan posting salah.

Tapi ini mudah untuk diperbaiki. Saat melakukan *query* koneksi dari beberapa jenis, Anda dapat melewatkan
berbagai argumen untuk permintaan GraphQL. Anda dapat `sort` dan `filter` *nodes*, atur bagaimana
banyak *nodes* untuk `lewati`, dan pilih `limit` dari berapa banyak *nodes* yang akan diambil. Dengan
mengatur operator yang kuat ini, Anda dapat memilih data yang Anda inginkan—dalam format yang Anda
perlukan.

Dalam *query* GraphQL halaman indeks Anda, ubah `allMarkdownRemark` ke
`allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC })`. _Catatan: Ada 3 garis bawah antara `frontmatter` dan `date`._ Simpan
ini dan urutannya harus diperbaiki.

Coba buka GraphiQL dan mainkan dengan berbagai opsi pengurutan. Anda dapat mengurutkan
koneksi `allFile` bersama dengan koneksi lain.

Untuk dokumentasi lebih lanjut tentang operator *query* kami, kunjungi [panduan referensi GraphQL](/docs/graphql-reference/)

## Tantangan

Coba buat halaman baru yang berisi sebuah blog *post* dan lihat apa yang terjadi pada daftar blog *post* di beranda!

## Apa yang akan terjadi selanjutnya?

Ini bagus! Anda baru saja membuat halaman indeks tempat Anda melakukan *query* pada file markdown Anda
dan menghasilkan daftar judul *post* dan kutipan blog. Tetapi Anda tidak ingin hanya melihat kutipan, Anda ingin halaman yang sebenarnya untuk file markdown Anda.

Anda dapat terus membuat halaman dengan menempatkan komponen React di `src/pages`. Namun, selanjutnya Anda 
akan mempelajari bagaimana cara _programmatically_ membuat halaman dari _data_. Gatsby _tidak_
terbatas untuk membuat halaman dari file seperti kebanyakan *static site generators*. Gatsby memungkinkan
Anda menggunakan GraphQL untuk meminta _data_ dan _map_ hasil *query* Anda ke _halaman_—semuanya pada
*build time*. Ini adalah ide yang sangat kuat. Anda akan mengeksplorasi implikasinya dan
cara untuk menggunakannya dalam tutorial berikutnya, di mana Anda akan belajar cara [membuat laman dari data *programmatically*](/tutorial/part-seven/).

---
title: "*Source* Plugin"
typora-copy-images-to: ./
disableTableOfContents: true
---

> Tutorial ini adalah bagian dari seri tentang data layer Gatsby. Pastikan Anda telah melewati [part 4](/tutorial/part-four/) sebelum ke sini.

## Apa yang ada di toturial ini?

Di dalam tutorial ini, Anda akan belajar tentang bagaimana cara menarik data ke situs Gatsby Anda menggunakan GraphQL dan _source_ plugin. Namun, sebelum Anda belajar tentang plugin ini, Anda pasti ingin tahu caranya menggunakan sesuatu yang di sebut GraphiQL, alat yang membantu Anda menyusun kueri dengan benar.

## Pengantar GraphiQL

GraphiQL adalah _integrated development environment_ (IDE) untuk GraphQL. Ini adalah alat yang ampuh (dan luar biasa) yang akan sering Anda gunakan saat membangun situs web Gatsby.

Anda dapat mengaksesnya ketika server pengembangan situs Anda berjalan, biasanya di
<http://localhost:8000/___graphql>.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="/graphiql-explore.mp4"></source>
  <p>Browser Anda tidak mendukung elemen video.</p>
</video>

Lihat pada "tipe" `Site` dan lihat kolom apa yang tersedia di dalamnya, termasuk objek `siteMetadata` yang Anda minta sebelumnya. Coba buka GraphiQL dan mainkan dengan data Anda! Tekan <kbd>Ctrl + Space</kbd> (atau gunakan <kbd>Shift + Space</kbd> sebagai alternatif pintasan keyboard) untuk membuka jendela _autocomplete_ dan <kbd>Ctrl + Enter</kbd> untuk menjalankan kueri GraphQL. Anda akan menggunakan GraphiQL lebih banyak melalui tutorial yang tersisa.

## Menggunakan GraphiQL *Explorer*

GraphiQL *Explorer* memungkinkan Anda untuk membangun kueri penuh secara interaktif dengan mengklik bidang dan input yang tersedia tanpa proses mengetik kueri berulang dengan tangan.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-build-a-graphql-query-using-gatsby-s-graphiql-explorer"
  lessonTitle="Membuat kueri GraphQL menggunakan Gatsby GraphiQL Explorer"
/>

## _Source_ plugin

Data di situs Gatsby dapat berasal dari mana saja: APIs, databases, CMSs, local files, dll.

_Source_ plugin menggambil data dari sumbernya. Misalnya plugin _source filesystem_ tahu cara mengambil data dari sistem file. WordPress plugin tahu cara mengambil data dari API WordPress.

Tambahkan [`gatsby-source-filesystem`](/packages/gatsby-source-filesystem/) dan jelajahi cara kerjanya.

Pertama, install plugin di _root_ projek:

```shell
npm install --save gatsby-source-filesystem
```

Selanjutnya tambahkan ini ke `gatsby-config.js` Anda:

```javascript:title=gatsby-config.js
module.exports = {
  siteMetadata: {
    title: `Pandas Eating Lots`,
  },
  plugins: [
    // highlight-start
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
    // highlight-end
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

Simpan itu dan mulai ulang server pengembangan gatsby. Kemudian buka kembali GraphiQL.

Di panel penjelajah, Anda akan melihat `allFile` dan `file` tersedia sebagai pilihan:

![graphiql-filesystem](graphiql-filesystem.png)

Klik dropdown `allFile`. Posisikan kursor Anda setelah `allFile` di area permintaan, dan lalu ketik <kbd>Ctrl + Enter</kbd>. Ini akan mengisi `id` untuk setiap file terlebih dahulu. Tekan "Mainkan" untuk menjalankan kueri:

![filesystem-query](filesystem-query.png)

Di panel Exploere, bidang `id` telah dipilih secara otomatis. Tentukan pilihan untuk lebih banyak bidang dengan mencentang kotak yang sesuai pada bidang tersebut. Tekan "Mainkan" untuk menjalankan kueri lagi, dengan bidang baru:

![pilihan-pada-filesystem-explorer](filesystem-explorer-options.png)

Alternatifnya, Anda dapat menambahkan bidang dengan menggunakan pintasan _autocomplete_ (<kbd>Ctrl + Space</kbd>). Ini akan menampilkan bidang yang dapat diminta pada node `File`.

![filesystem-autocomplete](filesystem-autocomplete.png)

Coba tambahkan sejumlah bidang ke kueri Anda, dengan menekan <kbd>Ctrl + Enter</kbd>
setiap kali menjalankan kueri kembali. Anda akan melihat hasil _query_ yang diperbarui:

![allfile-query](allfile-query.png)

Hasilnya adalah array dari `File` "nodes" (_node_ adalah nama mewah untuk objek di "_graph_"). Setiap objek `File` _node_ memiliki bidang yang Anda minta.

## Membuat halaman dengan GraphQL _query_

Membangun halaman baru dengna Gatsby sering dimulai dengan GraphiQL. Anda pertama-tama membuat sketsa
kueri data dengan bermain di GraphiQL lalu salin ini ke halaman komponen React
untuk mulai membangun UI.

Ayo Coba ini.

Buat file baru di `src/pages/my-files.js` dengan `allFile` GraphQL _query_ Anda baru saja
dibuat

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data) // highlight-line
  return (
    <Layout>
      <div>Hello world</div>
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

Baris `console.log(data)` disorot lebih tinggi. Ini sering membantu ketika
membuat komponen baru untuk mencetak data yang Anda dapatkan dari GraphQL _query_
sehingga Anda dapat menjelajahi data di konsol browser Anda sambil membuat UI.

Jika Anda menggunjungi halaman baru di `/my-files/` dan buka konsol browser Anda
Anda akan melihat sesuatu seperti:

![data-di-konsol](data-in-console.png)

Bentuk data sama dengan bentuk dari GraphQL _query_.

Tambahkan beberapa kode ke komponen Anda untuk mencetak File data.

```jsx:title=src/pages/my-files.js
import React from "react"
import { graphql } from "gatsby"
import Layout from "../components/layout"

export default ({ data }) => {
  console.log(data)
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>My Site's Files</h1>
        <table>
          <thead>
            <tr>
              <th>relativePath</th>
              <th>prettySize</th>
              <th>extension</th>
              <th>birthTime</th>
            </tr>
          </thead>
          <tbody>
            {data.allFile.edges.map(({ node }, index) => (
              <tr key={index}>
                <td>{node.relativePath}</td>
                <td>{node.prettySize}</td>
                <td>{node.extension}</td>
                <td>{node.birthTime}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
      {/* highlight-end */}
    </Layout>
  )
}

export const query = graphql`
  query {
    allFile {
      edges {
        node {
          relativePath
          prettySize
          extension
          birthTime(fromNow: true)
        }
      }
    }
  }
`
```

Dan sekarang buka [http://localhost:8000/my-files](http://localhost:8000/my-files)… 😲

![halaman-my-files](my-files-page.png)

## Apa selanjutnya?

Sekarang Anda telah belajar bagaimana _source_ plugin membawa data ke sistem data Gatsby. Di tutorial selanjutnya, Anda akan belajar bagaimana plugin transformer membawa data mentah yang dibawa oleh _source_ plugin. Kombinasi _source_ plugin dan plugin transformer dapat menangani semua sumber data dan transformasi data yang Anda perlukan saat membangun situs Gatsby. Pelajari tentang plugin transformer di [bagian ke 6 dari tutorial tutorial](/tutorial/part-six/).

---
title: Secara terprogram membuat halaman dari data
typora-copy-images-to: ./
disableTableOfContents: true
---

> Tutorial ini adalah bagian dari rangkaian tentang _data layer_ Gatsby. Pastikan Anda telah melewati [bagian 4](/tutorial/part-four/), [bagian 5](/tutorial/part-five/), dan [bagian 6](/tutorial/part-six/) sebelum melanjutkan di sini.

## Apa yang ada di tutorial ini?

Di tutorial sebelumnya, Anda telah membuat halaman indeks yang mengambil file _markdown_ dan menghasilkan daftar dari judul postingan blog beserta kutipannya. Tapi, tentu Anda tidak ingin hanya melihat kutipan saja, Anda ingin melihat halaman sebenarnya dari file _markdown_.

Anda bisa melanjutkan untuk membuat halaman dengan menempatkan komponen React di `src/pages`. Namun, sekarang Anda akan belajar bagimana untuk secara terprogram membuat halaman dari _data_. Gatsby _tidak_ terbatas hanya membuat halaman dari _files_ seperti kebanyakan generator halaman statis. Gatsby mengijinkan Anda menggunakan GraphQL untuk mengambil _data_ dan _memetakan_ hasil dari _query_ ke semua _halaman_ pada saat _build time_. Ini adalah ide yang sangat _powerful_. Anda akan mengeksplorasi maksud dan cara menggunakannya di tutorial ini.

Mari kita mulai.

## Membuat _slugs_ untuk halaman

Membuat halaman baru memiliki dua langkah:

1.  Menghasilkan "_path_" atau "_slug_" untuk halaman.
2.  Membuat halaman.

_**Catatan**: Seringkali sumber data akan secara langsung memberikan slug atau nama tujuan untuk konten — ketika bekerja dengan salah satu sistem (contohnya sebuah CMS), Anda tidak harus membuat sendiri slugs seperti yang Anda lakukan untuk file markdown._

Untuk membuat halaman _markdown_, Anda akan belajar menggunakan dua APIs Gatsby: [`onCreateNode`](/docs/node-apis/#onCreateNode) dan [`createPages`](/docs/node-apis/#createPages). Keduanya adalah APIs utama yang akan sering Anda lihat digunakan di banyak situs dan plugin.

Kami melakukan yang terbaik untuk membuat APIs Gatsby mudah diimplementasikan. Untuk implementasi API, Anda akan mengkespor sebuah fungsi dari API `gatsby-node.js`.

Jadi, begini cara melakukannya. Di folder bagian atas (_root_) situs anda, buat sebuah file dengan nama `gatsby-node.js`. Kemudian tambahkan sebagai berikut:

```javascript:title=gatsby-node.js
exports.onCreateNode = ({ node }) => {
  console.log(node.internal.type);
};
```

`onCreateNode` adalah fungsi yang akan dipanggil oleh Gatsby ketika _node_ baru telah berhasil dibuat (atau diperbaharui).

_Stop_ dan _restart_ server _development_. Setelah itu, Anda akan melihat beberapa _node_ telah dibuat dan ditampilkan di konsol _terminal_.

Pergunakan API untuk menambahkan _slugs_ pada halaman _markdown_ Anda ke `MarkdownRemark` _nodes_.

Ubah fungsi Anda, sehingga _logs_ hanya menampilkan `MarkdownRemark` nodes.

```javascript:title=gatsby-node.js
exports.onCreateNode = ({ node }) => {
  // highlight-start
  if (node.internal.type === `MarkdownRemark`) {
    console.log(node.internal.type);
  }
  // highlight-end
};
```

Anda ingin menggunakan setiap nama file _markdown_ untuk membuat _slug_ dari halaman. Sehingga `pandas-and-bananas.md` akan menjadi `/pandas-and-bananas/`. Tapi bagaimana Anda mendapatkan nama file dari _node_ `MarkdownRemark`? Untuk mendapatkannya, Anda harus meneruskan (_traverse_) "_node graph_" ke _parent node `File`_, karena _node `File`_ memiliki data yang Anda butuhkan dari _disk_. Untuk melakukannya, ubah fungsi anda lagi:

```javascript:title=gatsby-node.js
// highlight-next-line
exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    // highlight-start
    const fileNode = getNode(node.parent);
    console.log(`\n`, fileNode.relativePath);
    // highlight-end
  }
};
```

Setelah _restart_ server _development_, Anda seharusnya melihat _relative paths_ untuk dua file _markdown_ ditampilkan di layar _terminal_.

![markdown-relative-path](markdown-relative-path.png)

Sekarang Anda harus membuat _slugs_. Karena logika untuk membuat _slugs_ dari nama _file_ akan rumit, maka plugin `gatsby-source-filesystem` telah memiliki fungsi untuk membuat _slugs_.
Mari gunakan pluginnya.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`); // highlight-line

exports.onCreateNode = ({ node, getNode }) => {
  if (node.internal.type === `MarkdownRemark`) {
    console.log(createFilePath({ node, getNode, basePath: `pages` })); // highlight-line
  }
};
```

Fungsi tersebut menangani pencarian _parent `File` node_ bersamaan dengan pembuatan _slug_. Jalankan lagi server _development_ dan Anda akan melihat dua _slugs_ ditampilkan di _terminal_, satu untuk setiap file _markdown_.

Sekarang Anda dapat menambahkan _slugs_ baru secara langsung ke dalam _nodes_ `MarkdownRemark`. Hal ini sangat _powerful_, karena data apapun yang Anda tambahkan ke _nodes_ akan tersedia untuk diambil nanti dengan GraphQL. Jadi, hal ini akan memudahkan untuk mendapatkan _slug_ ketika nanti akan membuat halaman.

Untuk melakukannya, Anda akan menggunakan fungsi dari API yaitu [`createNodeField`](/docs/actions/#createNodeField). Fungsi ini mengijinkan Anda untuk membuat _field_ tambahan pada _nodes_ yang dibuat oleh _plugins_ lain. Hanya pembuat asli dari _node_ yang dapat langsung mengubah semua _node_ dari _plugin_ lain (termasuk `gatsby-node.js` Anda) harus menggunakan fungsi ini untuk membuat tambahan _fields_.

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`);
// highlight-next-line
exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions; // highlight-line
  if (node.internal.type === `MarkdownRemark`) {
    // highlight-start
    const slug = createFilePath({ node, getNode, basePath: `pages` });
    createNodeField({
      node,
      name: `slug`,
      value: slug
    });
    // highlight-end
  }
};
```

_Restart_ server _development_ dan _refresh_ GraphiQL. Kemudian jalankan perintah GraphQL berikut untuk melihat _slugs_ Anda yang baru:

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        fields {
          slug
        }
      }
    }
  }
}
```

Sekarang _slugs_ telah dibuat, Anda dapat membuat halaman.

## Membuat Halaman

Di tempat yang sama dengan file `gatsby-node.js`, tambahkan seperti berikut:

```javascript:title=gatsby-node.js
const { createFilePath } = require(`gatsby-source-filesystem`);

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions;
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` });
    createNodeField({
      node,
      name: `slug`,
      value: slug
    });
  }
};

// highlight-start
exports.createPages = async ({ graphql, actions }) => {
  // **Note:** The graphql function call returns a Promise
  // see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise for more info
  const result = await graphql(`
    query {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `);

  console.log(JSON.stringify(result, null, 4));
};
// highlight-end
```

Anda akan menambahkan implementasi dari [`createPages`](/docs/node-apis/#createPages), ini adalah API yang dipanggil oleh Gatsby sehingga _plugins_ dapat membuat halaman.

Seperti disinggung pada awal bagian dari tutorial ini, langkah-langkah untuk membuat halaman secara terprogram adalah:

1.  Mengambil data dengan GraphQL
2.  Memetakan hasil _query_ ke halaman

Kode diatas adalah langkah pertama untuk membuat halaman dari _markdown_ Anda, saat Anda menggunakan fungsi yang disediakan `graphql` untuk mengambil _markdown slugs_ yang telah Anda buat sebelumnya. Kemudian hasil dari _query_ Anda akan menampilkan yang terlihat seperti:

![query-markdown-slugs](query-markdown-slugs.png)

Anda membutuhkan satu hal tambahan diluar _slug_ untuk membuat halaman: sebuah format komponen halaman.
Seperti semua yang ada di Gatsby, halaman terprogram juga menggunakan komponen React.
Ketika membuat halaman, Anda perlu menentukan komponen mana yang akan digunakan.

Buat folder di `src/templates`, kemudian tambahkan kode di bawah ini, ke dalam _file_ dengan nama `src/templates/blog-post.js`.

```jsx:title=src/templates/blog-post.js
import React from "react";
import Layout from "../components/layout";

export default () => {
  return (
    <Layout>
      <div>Hello blog post</div>
    </Layout>
  );
};
```

Kemudian perbaharui `gatsby-node.js`

```javascript:title=gatsby-node.js
const path = require(`path`); // highlight-line
const { createFilePath } = require(`gatsby-source-filesystem`);

exports.onCreateNode = ({ node, getNode, actions }) => {
  const { createNodeField } = actions;
  if (node.internal.type === `MarkdownRemark`) {
    const slug = createFilePath({ node, getNode, basePath: `pages` });
    createNodeField({
      node,
      name: `slug`,
      value: slug
    });
  }
};

exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions; // highlight-line
  const result = await graphql(`
    query {
      allMarkdownRemark {
        edges {
          node {
            fields {
              slug
            }
          }
        }
      }
    }
  `);

  // highlight-start
  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: path.resolve(`./src/templates/blog-post.js`),
      context: {
        // Data passed to context is available
        // in page queries as GraphQL variables.
        slug: node.fields.slug
      }
    });
  });
  // highlight-end
};
```

Jalankan ulang server _development_ dan halaman Anda akan dibuat! Cara mudah untuk mencari halaman baru yang telah dibuat adalah dengan membuka halaman secara acak, karena Gatsby akan membantu menunjukkan daftar halaman dari situs. Jika anda mengakses <http://localhost:8000/sdf>, Anda akan melihat halaman baru yang telah dibuat.

![new-pages](new-pages.png)

Klik salah satu dari halaman, maka Anda akan melihat:

![hello-world-blog-post](hello-world-blog-post.png)

Hal ini sedikit membosankan dan bukan yang Anda inginkan. Sekarang Anda bisa mengambil data dari postingan _markdown_. Ubah `src/templates/blog-post.js` ke:

```jsx:title=src/templates/blog-post.js
import React from "react";
import { graphql } from "gatsby"; // highlight-line
import Layout from "../components/layout";

// highlight-start
export default ({ data }) => {
  const post = data.markdownRemark;
  // highlight-end
  return (
    <Layout>
      {/* highlight-start */}
      <div>
        <h1>{post.frontmatter.title}</h1>
        <div dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
      {/* highlight-end */}
    </Layout>
  );
};

// highlight-start
export const query = graphql`
  query($slug: String!) {
    markdownRemark(fields: { slug: { eq: $slug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`;
// highlight-end
```

Dan…

![blog-post](blog-post.png)

Keren!

Langkah terakhir adalah untuk menghubungkan halaman baru Anda dari halaman indeks.

Kembali ke `src/pages/index.js`, ambil _markdown slugs_ Anda, dan buat penghubung.

```jsx:title=src/pages/index.js
import React from "react";
import { css } from "@emotion/core";
import { Link, graphql } from "gatsby"; // highlight-line
import { rhythm } from "../utils/typography";
import Layout from "../components/layout";

export default ({ data }) => {
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
            {/* highlight-start */}
            <Link
              to={node.fields.slug}
              css={css`
                text-decoration: none;
                color: inherit;
              `}
            >
              {/* highlight-end */}
              <h3
                css={css`
                  margin-bottom: ${rhythm(1 / 4)};
                `}
              >
                {node.frontmatter.title}{" "}
                <span
                  css={css`
                    color: #555;
                  `}
                >
                  — {node.frontmatter.date}
                </span>
              </h3>
              <p>{node.excerpt}</p>
            </Link> {/* highlight-line */}
          </div>
        ))}
      </div>
    </Layout>
  );
};

export const query = graphql`
  query {
    allMarkdownRemark(sort: { fields: [frontmatter___date], order: DESC }) {
      totalCount
      edges {
        node {
          id
          frontmatter {
            title
            date(formatString: "DD MMMM, YYYY")
          }
          // highlight-start
          fields {
            slug
          }
          // highlight-end
          excerpt
        }
      }
    }
  }
`;
```

Dan selesai! Blog berfungsi, meskipun kecil!

## Tantangan

Coba lebih banyak bermain-main dengan situs Anda. Coba tambahkan beberapa file _markdown_. Coba ambil data lain dari _nodes_ `MarkdownRemark` dan tambahkan hasilnya ke halaman utama atau halaman posting blog.

Pada tutorial ini, Anda telah belajar dasar dari pembuatan situs dengan _data layer_ Gatsby's. Anda telah belajar darimana sumber data dan cara mengubah data dengan _plugins_, bagaimana menggunakan GraphQL untuk _memetakan_ data ke halaman, dan kemudian bagaimana untuk membangun _template komponen halaman_ tempat Anda mengambil data untuk setiap halaman.

## Apa tutorial selanjutnya?

Sekarang anda telah membangun situs dengan Gatsby, kemudian apa selanjutnya?

- Bagikan situs Gatsby anda ke Twitter dan lihat apa yang orang lain telah buat dengan mencari #gatsbytutorial! Pastikan untuk menyertakan @gatsbyjs dan _hashtag_ #gatsbytutorial di Tweet Anda :)
- Anda dapat melihat beberapa [contoh situs](https://github.com/gatsbyjs/gatsby/tree/master/examples#gatsby-example-websites)
- Cari tahu lebih lanjut [plugins](/docs/plugins/)
- Lihat yang [orang lain buat dengan Gatsby](/showcase/)
- Lihat dokumentasi [Gatsby's APIs](/docs/api-specification/), [nodes](/docs/node-interface/), atau [GraphQL](/docs/graphql-reference/)

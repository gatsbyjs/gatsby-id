---
title: Resep
tableOfContentsDepth: 2
---

<!-- Basic template for a Gatsby recipe:

## Task to accomplish.
1-2 sentences about it. The more concise and focused, the better!

### Prerequisites
- System/version requirements
- Everything necessary to set up the task
- Including setting up accounts at other sites, like Netlify
- See [docs templates](/docs/docs-templates/) for formatting tips

### Directions
Step-by-step directions. Each step should be repeatable and to-the-point. Anything not critical to the task should be omitted.

#### Live example (optional)
A live example may not be possible depending on the nature of the recipe, in which case it is fine to omit.

### Additional resources
- Tutorials
- Docs pages
- Plugin READMEs
- etc.

See [docs templates](/docs/docs-templates/) in the contributing docs for more help.
-->

Menginginkan yang di tengah-tengah antara [tutorial lengkap](/tutorial/) dan merayap di [dokumentasi](/docs/)?. Berikut ini panduan meracik untuk membuat sesuatu, Gatsby style.

## 1. Halaman dan Tata Letak

### Struktur proyek

Di dalam proyek Gatbsy, Anda kemungkinan akan menemui sebagian atau semua dari direktori dan berkas sebagai berikut:

```
|-- /.cache
|-- /plugins
|-- /public
|-- /src
    |-- /pages
    |-- /templates
    |-- html.js
|-- /static
|-- gatsby-config.js
|-- gatsby-node.js
|-- gatsby-ssr.js
|-- gatsby-browser.js
```

Beberapa berkas penting dan definisinya:

- `gatsby-config.js` — konfigurasi opsi untuk situs Gatsby, dengan metadata untuk judul proyek, deskripsi, plugin, dan lainnya.
- `gatsby-node.js` — implementasi Gatsby Node.js API untuk kustomisasi dan memperluas pengaturan standar yang berefek pada saat proses build
- `gatsby-browser.js` — kustomisasi dan memperluas pengaturan standar yang berefek pada peramban, menggunakan API peramban Gatsby
- `gatsby-ssr.js` — menggunakan API dari Gatsby server-side rendering untuk kustomisasi pengaturan standar yang berefek pada server-side rendering 

#### Sumber daya tambahan

- Untuk tur dari semua direktori dan berkas yang umum, bacalah dokumentasi di [Struktur Proyek Gatsby]((/docs/gatsby-project-structure/))
- Untuk baris perintah yang umum, cek [Dokumentasi Gastby CLI](/docs/gatsby-cli)
- Cek [Gatsby Cheat Sheet](/docs/cheat-sheet/) untuk informasi yang dapat didownload dalam sekejap

### Membuat halaman secara otomatis

Inti dari Gatsby adalah secara otomatis mengubah komponen React di `src/pages` menjadi berbagai halaman dengan beberapa URL.
Sebagai contoh, komponen `src/pages/index.js` dan `src/pages/about.js` akan otomatis membuat beberapa halaman pada situs dengan halaman index (`/`) dan `/about`.

#### Prasyarat

- Sebuah [Situs Gatsby](/docs/quick-start)
- [Gatsby CLI](/docs/gatsby-cli) telah terinstall

#### Petunjuk

1. Buatlah sebuah direktori `src/pages` jika situs Anda belum memilikinya.
2. Tambahkan sebuah berkas komponen ke direktori halaman:

```jsx:title=src/pages/about.js
import React from "react"

const AboutPage = () => (
  <main>
    <h1>Tentang Pengarang</h1>
    <p>Selamat datang di situs Gatsby.</p>
  </main>
)

export default AboutPage
```

3. Jalankan `gatsby develop` untuk memulai development server.
4. Kunjungi halaman baru anda melalui peramban: `http://localhost:8000/about`

#### Sumber daya tambahan

- [Membuat dan memodifikasi halaman](/docs/creating-and-modifying-pages/)

### Menghubungkan antar halaman

Routing di Gatsby mengandalkan pada komponen `<Link />`.

#### Prasyarat

- Sebuah situs Gatsby dengan dua komponen halaman: `index.js` dan `contact.js`
- Komponen Gatsby `<Link />`
- [Gatsby CLI](/docs/gatsby-cli/) untuk menjalankan `gatsby develop`

#### Petunjuk

1. Bukalah komponen halaman index (`src/pages/index.js`), impor komponen `<Link />` dari Gatsby, tambahkan komponen `<Link />` di atas header, dan beri `to` property dengan value `"/contact/"` untuk nama path-nya, sebagai berikut:

```jsx:title=src/pages/index.js
import React from "react"
import { Link } from "gatsby"

export default () => (
  <div style={{ color: `purple` }}>
    <Link to="/contact/">Kontak</Link>
    <p>Dunia yang luarbiasa.</p>
  </div>
)
```

2. Jalankan `gatsby develop` dan buka halaman index. Anda akan menemui sebuah tautan yang bisa mengarahkan ANda ke halaman kontak ketika ditekan!

> **Catatan**: Komponen Gatsby `<Link />` adalah sebuah sampul dari [komponen link `@reach/router`](https://reach.tech/router/api/Link). Untuk informasi lebih lanjut mengenai komponen Gatsby `<Link />`, dapat dilihat di [Referensi API untuk `<Link />`](/docs/gatsby-link/).

### Membuat sebuah komponen tata letak

Adalah hal yang umum ketika membungkus halaman dengan sebuah komponen tata letak React, yang mana untuk memungkinkan membagikan markup, styles, dan fungsionalitas lintas halaman.

#### Prasyarat

- Sebuah situs Gatsby

#### Petunjuk

1. Buatlah sebuah komponen tata letak di `src/components`, dimana komponen child-nya akan dioper sebagai props:

```jsx:title=src/components/layout.js
import React from "react"

export default ({ children }) => (
  <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
    {children}
  </div>
)
```

2. Impor dan gunakan komponen tata letak di sebuah halaman:

```jsx:title=src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => (
  <Layout>
    <Link to="/contact/">Kontak</Link>
    <p>Dunia yang luarbiasa.</p>
  </Layout>
)
```

#### Sumber daya tambahan

- Buat sebuah komponen tata letak di [tutorial bab ketiga](/tutorial/part-three/#your-first-layout-component)
- Styling dengan [Komponen Tata letak](/docs/layout-components/)

### Membuat halaman secara terprogram dengan createPage

You can create pages programmatically in the `gatsby-node.js` file with helper methods Gatsby provides.

#### Prasyarat

- Sebuah [Situs Gatsby](/docs/quick-start)
- Satu berkas `gatsby-node.js`

#### Petunjuk

1. Pada `gatsby-node.js`, tambahkan sebuah ekspor untuk `createPages`

```javascript:title=gatsby-node.js
// highlight-start
exports.createPages = ({ actions }) => {
  // ...
}
// highlight-end
```

2. Destructure `createPage` action dari action yang tersedia, sehingga bisa dipanggil dengan sendirinya, dan tambahkan atau ambil data

```javascript:title=gatsby-node.js
exports.createPages = ({ actions }) => {
  // highlight-start
  const { createPage } = actions
  // pull in or use whatever data
  const dogData = [
    {
      name: "Fido",
      breed: "Sheltie",
    },
    {
      name: "Sparky",
      breed: "Corgi",
    },
  ]
  // highlight-end
}
```

3. Loop melalui data di `gatsby-node.js` dan sediakan path, template, dan context (data akan dioper di pageContext props) untuk `createPage` pada tiap-tiap invocation.

```javascript:title=gatsby-node.js
exports.createPages = ({ actions }) => {
  const { createPage } = actions

  const dogData = [
    {
      name: "Fido",
      breed: "Sheltie",
    },
    {
      name: "Sparky",
      breed: "Corgi",
    },
  ]
  // highlight-start
  dogData.forEach(dog => {
    createPage({
      path: `/${dog.name}`,
      component: require.resolve(`./src/templates/dog-template.js`),
      context: { dog },
    })
  })
  // highlight-end
}
```

4. Buat sebuah komponen React untuk ditampilkan sebagai template pada halaman Anda yang telah digunakan pada `createPage`

```jsx:title=src/templates/dog-template.js
import React from "react"

export default ({ pageContext: { dog } }) => (
  <section>
    {dog.name} - {dog.breed}
  </section>
)
```

5. Jalankan `gatsby develop` arahkan ke path menuju salah satu halaman yang telah Anda buat (contoh pada `http://localhost:8000/Fido`) untuk melihat data yang telah Anda oper untuk ditampilan pada halaman

#### Sumber daya tambahan

- Bab tutorial [membuat halaman secara terprogram dari data](/tutorial/part-seven/)
- Panduan referensi [menggunakan Gatsby tanpa GraphQL](/docs/using-gatsby-without-graphql/)
- [Contoh repo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-createPage) untuk resep ini

## 2. Styling dengan CSS

Banyak cara untuk menambah styles pada situs Anda; Gatsby memberikan dukungan untuk hampir semua pilihan yang bisa dilakukan, melalui plugin resmi dan komunitas.

### Menggunakan berkas CSS global tanpa komponen Tata letak

#### Prasyarat

- Satu [Situs Gatsby](/docs/quick-start/) yang sudah ada dengan komponen halaman index
- Satu berkas `gatsby-browser.js`

#### Petunjuk

1. Buatlah sebuah berkas CSS global sebagai `src/styles/global.css` dan tempel yang di bawa ini pada berkas:

```css:title=src/styles/styles/global.css
html {
  background-color: lavenderblush;
}

p {
  color: maroon;
}
```

2. Impor berkas CSS global pada berkas `gatsby-browser.js` sebagai berikut:

```javascript:gatsby-browser.js
import "./src/styles/global.css"
```

> **Catatan:** Anda juga dapat menggunakan `require('./src/styles/global.css')` untuk impor berkas CSS global pada berkas `gatsby-config.js`.

3. Jalankan `gatsby-develop` untuk mengamati pengaplikasian styling global pada situs Anda.

> **Catatan:** Pendekatan ini bukanlah yang terbaik jika Anda menggunakan CSS-in-JS untuk styling situs Anda, dalam hal ini halaman tata letak dengan semua komponen bersama (shared components) harus digunakan. Hal ini akan diulas pada resep selanjutnya.

#### Sumber daya tambahan

- Lebih lanjut mengenai [menambah styles global tanpa komponen tata letak](/docs/global-css/#adding-global-styles-without-a-layout-component)

### Menggunakan styles global pada komponen tata letak

#### Prasyarat

- Satu [Situs Gatsby](/docs/quick-start/) dengan komponen halaman index

#### Petunjuk

Anda dapat menambah styles global pada [komponent tata letak bersama](/tutorial/part-three/#your-first-layout-component). Komponen ini digunakan pada hal yang umum di seluruh situs, contohnya pada header dan footer.

1. Jika anda belum memiliki satu pun, buatlah sebuah direktori pada situs Anda di `/src/components`.

2. Pada direktori komponent, buatlah dua berkas: `layout.css` dan `layout.js`.

3. Tambahkan yang berikut ini pada `layout.css`:

```css:title=/src/components/layout.css
body {
  background: red;
}
```

4. Sunting `layout.js` untuk impor berkas CSS dan keluaran dari markup layout:

```jsx:title=/src/components/layout.js
import React from "react"
import "./layout.css"

export default ({ children }) => <div>{children}</div>
```

5. Sekarang sunting beranda situs Anda pada `/src/pages/index.js` dan gunakan komponen tata letak yang baru:

```jsx:title=/src/pages/index.js
import React from "react"
import Layout from "../components/layout"

export default () => <Layout>Halo dunia!</Layout>
```

#### Sumber daya tambahan

- [Styling Standar dengan Berkas CSS Global](/docs/global-css/)
- [Selebihnya mengenai komponen tata letak](/tutorial/part-three)

### Menggunakan Styled Components

#### Prasyarat

- Satu [Situs Gatsby](/docs/quick-start/) yang sudah ada dengan komponen halaman index
- [gatsby-plugin-styled-components, styled-components, dan babel-plugin-styled-components](/packages/gatsby-plugin-styled-components/) terpasang di `package.json`

#### Petunjuk

1. Pada berkas `gatsby-config.js` tambahkan `gatsby-plugin-styled-components`

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
}
```

2. Buka komponen halaman index (`src/pages/index.js`) dan impor `styled-components`package.

3. Hias komponen dengan membuat style blocks untuk tiap-tiap tipe elemen.

4. Terapkan pada halaman dengan cara memuat styled components  pada JSX

```jsx:title=src/pages/index.js
import React from "react"
import styled from "styled-components" //highlight-line

const Container = styled.div`
  margin: 3rem auto;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
`

const Avatar = styled.img`
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
`

const Username = styled.h2`
  margin: 0 0 12px 0;
  padding: 0;
`

const User = props => (
  <>
    <Avatar src={props.avatar} alt={props.username} />
    <Username>{props.username}</Username>
  </>
)

export default () => (
  <Container>
    <h1>Tentang Styled Components</h1>
    <p>Styled Components yang keren</p>
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
    />
  </Container>
)
```

4. Jalankan `gatsby develop` untuk melihat perubahannya

#### Sumber daya tambahan

- [Info lebih lanjut menggunakan Styled Components](/docs/styled-components/)
- [Pelajaran Egghead](https://egghead.io/lessons/gatsby-style-gatsby-sites-with-styled-components)

### Menggunakan Modul CSS

#### Prasyarat

- Satu [Situs Gatsby](/docs/quick-start/) yang sudah ada dengan komponen halaman index

#### Petunjuk

1. Buatlah sebuah modul CSS `src/pages/index.module.css` dan tempel berikut ini pada modul:

```css:title=src/components/index.module.css
.feature {
  margin: 2rem auto;
  max-width: 500px;
}
```

2. Impor modul CSS sebagai objek JSX `style` pada berkas `index.js` dengan memodifikasi halaman tersebut sebagai berikut:

```jsx:title=src/pages/index.js
import React from "react"

// highlight-start
import style from "./index.module.css"

export default () => (
  <section className={style.feature}>
    <h1>Menggunakan Modul CSS</h1>
  </section>
)
// highlight-end
```

3. Jalankan `gatsby develop` untuk melihat perubahan.

**Catatan:**
Perhatikan bahwa ekstensi berkas adalah `.module.css` bukan `.css`, karena Gatsby akan mengenalnya sebagai modul CSS.

#### Sumber daya tambahan

- Selengkapnya [Menggunakan Modul CSS](/tutorial/part-two/#css-modules)
- [Contoh langsung menggunakan Modul CSS](https://github.com/gatsbyjs/gatsby/blob/master/examples/using-css-modules)

### Menggunakan Sass/SCSS

Sass adalah sebuah ekstensi dari CSS yang membereikan Anda fitur lanjutan seperti kaidah nested, variables, mixins, dan banyak lagi.

Sass memiliki 2 sintaks. Sintaks paling banyak digunakan adalah "SCSS", dan ini adalah versi CSS yang sudah ditingkatkan. Artinya seluruh sintaks CSS yang valid, valid juga untuk SCSS. Berkas SCSS menggunakan ekstensi .scss

Sass akan menghimpun berkas .scss dan .sass menjadi berkas .css untuk Anda, dan Anda dapat menulis stylesheet dengan lebih banyak fitur lanjutan.

#### Prasyarat

- Sebuah [Situs Gatsby](/docs/quick-start)

#### Petunjuk

1. Pasang plugin Gatsby [gatsby-plugin-sass](https://www.gatsbyjs.org/packages/gatsby-plugin-sass/) dan `node-sass`.

`npm install --save node-sass gatsby-plugin-sass`

2. Muat plugin pada berkas `gatsby-config.js` Anda.

```javascript:title=gatsby-config.js
plugins: [`gatsby-plugin-sass`],
```

3. Tulis stylesheet Anda sebagai berkas `.sass` atau `.scss` dan impor mereka. Jika Anda belum tahu caranya impor styles, coba lihat [Styling dengan CSS](/docs/recipes/#2-styling-with-css)

```css:title=styles.scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

```css:title=styles.sass
$font-stack:    Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

```javascript
import "./styles.scss"
import "./styles.sass"
```

_Note: Anda dapat menggunakan berkas Sass/SCSS sebagai modul, seperti yang telah dijelaskan pada resep sebelumnya mengenai modul CSS, dengan perbedaan ekstensinya haruslah .scss atau .sass, bukan .css_

#### Sumber daya tambahan

- [Perbedaan antara .sass dan .scss](https://responsivedesign.is/articles/difference-between-sass-and-scss/)
- [Panduan Sass dari situs resmi sass](https://sass-lang.com/guide)
- [Tutorial lengkap instalasi Sass dengan penjelasan dan sumber daya yang lebih lengkap](https://www.gatsbyjs.org/docs/sass/)

### Menambah Font Lokal

#### Prasyarat

- Sebuah [Situs Gatsby](/docs/quick-start)
- Berkas font: `.woff2`, `.ttf`, etc.

#### Petunjuk

1. Salin sebuah berkas font ke proyek Gatsby Anda, seperti `src/fonts/fontname.woff2`.

```
src/fonts/fontname.woff2
```

2. Impor asset font ke sebuah berkas CSS untuk menggabungkannya ke situs Gatsby Anda:

```css:title=src/css/typography.css
@font-face {
  font-family: "Font Name";
  src: url("../fonts/fontname.woff2");
}
```

**Catatan:** Pastikan nama font direferensikan dari CSS yang relevan, contoh:

```css:title=src/components/layout.css
body {
  font-family: "Font Name", sans-serif;
}
```

Dengan menargetkan elemen HTML `body`, font Anda akan diterapkan pada sebagian teks di halaman. CSS tambahan dapat diarahkan ke elemen lainnya, contoh `button` atau `textarea`.

Jika font tidak memperbarui setelah mengikuti langkah-langkah di atas, pastikan untuk menggantikan font-family yang sudah ada dengan CSS yang relevan.

#### Sumber daya tambahan

- Selengkapnya [impor aset ke berkas](/docs/importing-assets-into-files/)

### Menggunakan Emotion

[Emotion](https://emotion.sh) adalah pustaka CSS-in-JS yang mantap, mendukung inline CSS styles dan styled components sekaligus. Anda dapat menggunakan masing-masing fitur secara sendiri ataupun berbarengan.

#### Prasyarat

- Sebuah [Situs Gatsby](/docs/quick-start)

#### Petunjuk

1. Pasang [Plugin Gatsby Emotion](/packages/gatsby-plugin-emotion/) dan Emotion package.

```shell
npm install --save gatsby-plugin-emotion @emotion/core @emotion/styled
```

2. Tambahkan plugin `gatsby-plugin-emotion` ke dalam berkas `gatsby-config.js` Anda:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-plugin-emotion`],
}
```

3. Jika Anda tidak punya, buatlah sebuah halaman di situs Gatsby anda pada `src/pages/emotion-sample.js`.

Impor inti package `css` dari Emotion. Anda dapat menggunakan `css` prop untuk menambahkan [Style Emotion objek](https://emotion.sh/docs/object-styles) pada elemen apa saja pada sebuah komponen.

```jsx:title=src/pages/emotion-sample.js
import React from "react"
import { css } from "@emotion/core"

export default () => (
  <div>
    <p
      css={{
        background: "pink",
        color: "blue",
      }}
    >
      Halaman ini menggunakan Emotion.
    </p>
  </div>
)
```

4. Untuk menggunakan [styled components](https://emotion.sh/docs/styled) dari Emotion, impor paket dan definisikan menggunakan fungsi `styled`.

```jsx:title=src/pages/emotion-sample.js
import React from "react"
import styled from "@emotion/styled"

const Content = styled.div`
  text-align: center;
  margin-top: 10px;
  p {
    font-weight: bold;
  }
`

export default () => (
  <Content>
    <p>Halaman ini menggunakan Emotion.</p>
  </Content>
)
```

#### Sumber daya tambahan

- [Menggunakan Emotion di Gatsby](/docs/emotion/)
- [Situs Emotion](https://emotion.sh)
- [Memulai dengan Emotion dan Gatsby](https://egghead.io/lessons/gatsby-getting-started-with-emotion-and-gatsby)

### Menggunakan Font Google 

Hosting [Font Google](https://fonts.google.com/) Anda sendiri di lokal pada sebuah proyek berarti font tersebut tidak akan di-fetch melalui jejaring internet ketika situs dimuat, akan meningkatkan kecepatan situs Anda sampai dengan ~300 milidetik pada desktop dan `+ detik pada 3G. Juga rekomendasi untuk memberikan batas penggunaan font kustom hanya untuk hal yang penting demi kinerja yang baik.

#### Prasyarat

- Sebuah [Situs Gatsby](/docs/quick-start)
- [Gatsby CLI](/docs/gatsby-cli/) sudah terpasang
- Memilih package font dari [proyel typefaces](https://github.com/KyleAMathews/typefaces)

#### Petunjuk

1. Jalankan `npm install --save typeface-your-chosen-font`, menggantikan `your-chosen-font` dengan nama font yang ingin Anda pasang dari [proyek typefaces](https://github.com/KyleAMathews/typefaces).

Contoh untuk memuat font 'Source Sans Pro' yang populer seperti ini: `npm install --save typeface-source-sans-pro`.

2. Tambahkan `import "typeface-your-chosen-font"` pada template tata letak, komponen halaman, atau `gatsby-browser.js`.

```jsx:title=src/components/layout.js
import "typeface-your-chosen-font"
```

3. Apabila sudah diimpor, nama font ini dapat digunakan pada stylesheet CSS, modul CSS, atau CSS-in-JS.

```css:title=src/components/layout.css
body {
  font-family: "Font Pilihan Anda";
}
```

_CATATAN: Untuk contoh di atas, deklarasi css yang tepat akan menjadi `font-family: 'Source Sans Pro';`_

#### Sumber daya tambahan

- [Typography.js](/docs/typography-js/) - Pilihan lain untuk menggunakan font Google pada situs Gatsby
- [The Typefaces Project Docs](https://github.com/KyleAMathews/typefaces/blob/master/README.md)
- [Dokumentasi Proyek Typefaces](https://github.com/KyleAMathews/typefaces/blob/master/README.md)
- [Contoh langsung pada blog Kyle Mathews](https://www.bricolage.io/typefaces-easiest-way-to-self-host-fonts/)

## 3. Bekerja dengan starter

[Starter](/docs/starters/) adalah boilerplate situs Gatsby yang disokong secara resmi atau bersama dengan komunitas.

### Menggunakan starter

#### Prasyarat

- [Gatsby CLI](/docs/gatsby-cli) terpasang

#### Petunjuk

1. Pilih starter yang ingin Anda gunakan. (_The [Pustaka Starter](/starters/?v=2) adalah tempat terbaik untuk meninjau!_)

2. Buat situs baru menggunakan starter. Pada termina, jalankan:

```shell
gatsby new {nama-proyek-anda} {tautan-starter}
```

> _Jangan jalankan persis seperti yang ada pada contoh -- ingat untuk menggantu {nama-proyek-anda} dan {tautan-starter}!_

3. Jalankan situs baru Anda:

```shell
cd {nama-proyek-anda}
gatsby develop
```

#### Sumber daya tambahan

- Ikuti [panduan lebih detail](/docs/starters/) menggunakan starter Gatsby.
- Belajar menggunakan [Gatsby CLI](/docs/gatsby-cli) perangkat untuk menggunakan starter di [tutorial bab pertama](/tutorial/part-one/#using-gatsby-starters)
- Jelajahi [Pustaka Starter](/starters/?v=2)
- Cek Gatsby [starter resmi standar](https://github.com/gatsbyjs/gatsby-starter-default)

## 4. Bekerja dengan tema

Sebuah tema Gatsby membungkus struktur Gatsby (fungsionalitas, sumber data, desain) ke dalam satu paket yang bisa dipasang. Ini artinya pengaturan dan fungsionalitas tidak secara langsung tertulis pada proyek Anda, tetapi sudah dibuat dalam suatu versi, diatur secara sentral, dan terpasang sebagai dependency. Anda dapat secara mudah memperbarui tema, membuat tema secara bersama-sama, bahkan bertukar tema yang cocok dan sesuai satu sama lain.

- Baca selengkapnya [Apa itu Tema Gatsby?](/docs/themes/what-are-gatsby-themes)

### Membuat situs baru menggunakan starter tema


Membuat situs berdasarkan starter yang menstruktur tema, sama prosesnya dengan membuat situs berdasarkan starter yang tidak menstruktur tema. Pada contoh ini Anda dapat menggunakan [starter untuk membuat situs baru yang menggunakan tema blog Gatsby resmi](https://github.com/gatsbyjs/gatsby-starter-blog-theme).

#### Prasyarat

- [Gatsby CLI](/docs/gatsby-cli) terpasang

#### Petunjuk

1. Buatlah sebuat situs berdasarkan starter tema blog:

```shell
gatsby new {nama-proyek-anda} https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

2. Jalankan situs baru Anda:

```shell
cd {nama-proyek-anda}
gatsby develop
```

#### Sumber daya tambahan

- Belajar cara menggunakan tema Gatsby yang sudah diseddiakan di [panduan konsep yang lebih pendek](/docs/themes/using-a-gatsby-theme) atau lebih detail [tutorial selangkah demi selangkah](/tutorial/using-a-theme).

### Build tema baru

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-the-gatsby-theme-workspace-starter-to-begin-building-a-new-theme"
  lessonTitle="Menggunakan Starter Ruang Kerja Tema Gatsby untuk Memulai Build sebuah Tema Baru"
/>

#### Prasyarat

- [Gatsby CLI](/docs/gatsby-cli) terpasang

* [Yarn](https://yarnpkg.com/lang/en/docs/install/#mac-stable) terpasang

#### Petunjuk

1. Buatlah sebuah ruang kerja tema baru menggunakan [Starter ruang kerja tema Gatsby](https://github.com/gatsbyjs/gatsby-starter-theme-workspace):

```shell
gatsby new {nama-proyek-anda} https://github.com/gatsbyjs/gatsby-starter-theme-workspace
```

2. Jalankan situs contoh tersebut pada ruang kerja:

```shell
yarn workspace example develop
```

#### Sumber daya tambahan

- Ikuti [panduan selengkapnya](/docs/themes/building-themes/) menggunakan starter ruang kerja tema Gatsby.
- Belajar bagaimana cara build tema Anda pada [Kursus video pembuatan tema Gatsby pada Egghead](https://egghead.io/courses/gatsby-theme-authoring), atau pada [kursus video tambahan](/tutorial/building-a-theme).

## 5. Sumber data

Sumber data pada Gatsby disokong dengan plugin; Plugin mengambil data dari sumber yang mereka miliki (contoh plugin `gatsby-source-filesystem` mengambil data dari berkas sistem, plugin `gatsby-source-wordpress` mengambul data dari API WordPress, dsb). Anda juga dapat meletakkan data pada sumber Anda sendiri.

### Menambahkan data ke GraphQL


[Lapisan data GraphQL](/docs/querying-with-graphql/) Gatsby menggunakan simpul(node) untuk sekumpulan data. Plugin sumber(source) Gatsby menambahkan simpul sumber yang dapat anda query, tetapi juga Anda dapat membuat simpul sumber Anda sendiri. Untuk menambahkan data kustom pada lapisan data GraphQL, Gatsby memberikan metode yang dapat Anda atur.

Resep ini menunjukkan kepada Anda bagaimana menambah kustom data menggunakan `createNode()`.

#### Petunjuk

1. Pada `gatsby-node.js` menggunakan `sourceNodes()` dan `actions.createNode()` untuk membuat dan ekspor simpul yang dapat men-query data.


```javascript:title=gatsby-node.js
exports.sourceNodes = ({ actions, createNodeId, createContentDigest }) => {
  const pokemons = [
    { name: "Pikachu", type: "electric" },
    { name: "Squirtle", type: "water" },
  ]

  pokemons.forEach(pokemon => {
    const node = {
      name: pokemon.name,
      type: pokemon.type,
      id: createNodeId(`Pokemon-${pokemon.name}`),
      internal: {
        type: "Pokemon",
        contentDigest: createContentDigest(pokemon),
      },
    }
    actions.createNode(node)
  })
}
```

2. Jalankan `gatsby develop`.

   > _Catatan: Setelah membuat perubahan pada `gatsby-node.js` Anda perlu untuk menjalankan ulang `gatsby develop` untuk melihat perubahan yang terjadi._

3. Query data (pada GraphQL atau di komponen Anda).

```graphql
query MyPokemonQuery {
  allPokemon {
    nodes {
      name
      type
      id
    }
  }
}
```

#### Sumber daya tambahan

- Contoh singkat menggunakan plugin `gatsby-source-filesystem` pada [tutorial bab lima](/tutorial/part-five/#source-plugins)
- Search available source plugins in the [Gatsby library](/plugins/?=source)
- Cari sumber plugin yang tersedia di [pustaka Gatsby](/plugins/?=source)
- Paham sumber dar plugin dengan build salah satunya dari [Pixabay tutorial plugin sumber](/docs/pixabay-source-plugin-tutorial/)
- Fungsi createNode [dokumentasi](/docs/actions/#createNode)

### Sumber data Markdown untuk post dan halaman blog dengan GrapghQL

Anda dapat meletakkan data Markdown dan menggunakan [`createPages` API](/docs/actions/#createPage) Gatsby untuk membuat halaman secara dinamis.

Resep ini menampilkan bagaimana cara membuat halaman dari berkas Markdown pada sistem berkas lokal Anda mengginakan lapisan dara GraphQL Gatsby.

#### Prasyarat

- Sebuah [situs Gatsby](/docs/quick-start) dengan berkas `gatsby-config.js`
- [Gatsby CLI](/docs/gatsby-cli) terpasang
- [gatsby-source-filesystem plugin](/packages/gatsby-source-filesystem) terpasang
- [gatsby-transformer-remark plugin](/packages/gatsby-transformer-remark) terpasang
- Berkas `gatsby-node.js`

#### Petunjuk

1. Pada `gatsby-config.js`, konfigurasi `gatsby-transformer-remark` dengan `gatsby-source-filesystem` untuk menangkap berkas Markdown dari sebuat berkas sumber. Ini merupakan tambahan dari catatan `gatsby-source-filesystem`, contohnya di bawah ini:

```js:title=gatsby-config.js
module.exports = {
  plugins: [
    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `content`,
        path: `${__dirname}/src/content`,
      },
    },
  ]
```

2. Tambahkan sebuah post Markdown pada `src/content`,  sekaligus sebuah sampul depan untuk judul, tanggal, dan path, dengan beberapa konten awal untuk body dari sebuah post:

```markdown:title=src/content/my-first-post.md
---
title: Post Pertamaku
date: 2019-07-10
path: /post-pertamaku
---

Ini post pertamaku di Gatsby menggunakan Markdown!
```


3. Mulai peladen(server) pengembangan dengan `gatsby develop`, arahkan ke GraphQL explorer pada `http://localhost:8000/___graphql`, dan tulis query untuk mendapatkan semua dara markdown:

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        frontmatter {
          path
        }
      }
    }
  }
}
```

<iframe
  title="Query untuk semua markdown"
  src="https://q4xpb.sse.codesandbox.io/___graphql?explorerIsOpen=false&query=%7B%0A%20%20allMarkdownRemark%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D"
  width="600"
  height="300"
/>

4. Tambahkan kode JavaScript untuk membuat halaman dari post Markdown ketika build dengan cara menyalin query GraphQL ke dalam `gatsby-node.js` dan looping sampai hasilnya:

```js:title=gatsby-node.js
const path = require(`path`)

exports.createPages = async ({ actions, graphql }) => {
  const { createPage } = actions

  const result = await graphql(`
    {
      allMarkdownRemark {
        edges {
          node {
            frontmatter {
              path
            }
          }
        }
      }
    }
  `)
  if (result.errors) {
    console.error(result.errors)
  }

  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.frontmatter.path,
      component: path.resolve(`src/templates/post.js`),
    })
  })
}
```

5. Tambahkan sebuah template post di `src/templates`, termasuk sebuah query GraphhQL untuk membuat halaman secara dinamis dari konten Markdwon ketika build:

```jsx:title=src/templates/post.js
import React from "react"
import { graphql } from "gatsby"

export default function Template({ data }) {
  const { markdownRemark } = data // data.markdownRemark holds your post data
  const { frontmatter, html } = markdownRemark
  return (
    <div className="blog-post">
      <h1>{frontmatter.title}</h1>
      <h2>{frontmatter.date}</h2>
      <div
        className="blog-post-content"
        dangerouslySetInnerHTML={{ __html: html }}
      />
    </div>
  )
}

export const pageQuery = graphql`
  query($path: String!) {
    markdownRemark(frontmatter: { path: { eq: $path } }) {
      html
      frontmatter {
        date(formatString: "MMMM DD, YYYY")
        path
        title
      }
    }
  }
`
```

6. Jalankan `gatsby develop` untuk menjalankan ulang peladen pengembangan. Untuk melihat hasil post pada peramban: `http://localhost:8000/my-first-post`

#### Sumber daya tambahan

- [Tutorial: Membuat halaman secara terprogram dengan data](/tutorial/part-seven/)
- [Membuat dan memodifikasi halaman](/docs/creating-and-modifying-pages/)
- [Menambahkan halaman Markdown](/docs/adding-markdown-pages/)
- [Panduan untuk membuat halaman dari data secara terprogram](/docs/programmatically-create-pages-from-data/)
- [Contoh repo](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-sourcing-markdown) untuk resep ini

### Menarik data dari sumber eksternal dan membuat halaman tanpa GraphQL

Anda tidak perlu menggunakan lapisan data GraphQL untuk memasukkan data pada halaman, [meskipun ada beberapa alasan mengapa harus mempertimbangkan GraphQL](/docs/why-gatsby-uses-graphql/). Anda dapat menggunakan simpul API `createPages` untuk menarik data yang tak terstruktur ke dalam situs Gatsby secara langsung daripada melalui GraphQL dan plugin sumber.

Pada resep ini, Anda akan membuat halaman secara dinamis dari data yang didapat dari [PokéAPI’s REST endpoints](https://www.pokeapi.co/). [Contoh lengkap](https://github.com/jlengstorf/gatsby-with-unstructured-data/) dapat ditemukan pada GitHub.

#### Prasyarat

- Situs Gatsby dengan berkas `gatsby-node.js`
- [Gatsby CLI](/docs/gatsby-cli) terpasang
- Paket [axios](https://www.npmjs.com/package/axios) terpasang melalui npm

#### Petunjuk

1. Pada `gatsby-node.js`, tambahkan kode JavaScript untuk mendapatkan data dari PokéAPI dan secara terprogram membuat halaman index: 

```js:title=gatsby-node.js
const axios = require("axios")

const get = endpoint => axios.get(`https://pokeapi.co/api/v2${endpoint}`)

const getPokemonData = names =>
  Promise.all(
    names.map(async name => {
      const { data: pokemon } = await get(`/pokemon/${name}`)
      return { ...pokemon }
    })
  )
exports.createPages = async ({ actions: { createPage } }) => {
  const allPokemon = await getPokemonData(["pikachu", "charizard", "squirtle"])

  // Create a page that lists Pokémon.
  createPage({
    path: `/`,
    component: require.resolve("./src/templates/all-pokemon.js"),
    context: { allPokemon },
  })
}
```

2. Buat sebuah template untuk menampilkan Pokémon pada beranda: 

```js:title=src/templates/all-pokemon.js
import React from "react"

export default ({ pageContext: { allPokemon } }) => (
  <div>
    <h1>Lihat, itu Pokémon!</h1>
    <ul>
      {allPokemon.map(pokemon => (
        <li key={pokemon.id}>
          <img src={pokemon.sprites.front_default} alt={pokemon.name} />
          <p>{pokemon.name}</p>
        </li>
      ))}
    </ul>
  </div>
)
```

3. Jalankan `gatsby develop` untuk mendapatkan data, build halaman, dan memulai peladen pengembangan.
4. Buka beranda Anda di peramban: `http://localhost:8000`

#### Sumber daya tambahan

- [Repo data lengkap Pokemon](https://github.com/jlengstorf/gatsby-with-unstructured-data/)
- Selengkapnya menggunakan data tak terstruktur [Menggunakan Gatsby tanpa GraphQL](/docs/using-gatsby-without-graphql/)
- Kapan dan bagaimana [query data dengan GraphQL](/docs/querying-with-graphql/) untuk situs Gatsby yang lebih rumit

### Konten sumber dari Drupal

#### Prasyarat

- Sebuah [situs Gatsby](/docs/quick-start)
- Sebuah situs [Drupal](http://drupal.org)
- [Modul JSON:API](https://www.drupal.org/project/jsonapi) terpasang dan aktif pada situs Drupal

#### Petunjuk

1. Pasang plugin `gatsby-source-drupal`.

```
npm install --save gatsby-source-drupal
```

2. Ubah berkas`gatsby-config.js` untuk mengaktifkannya, kemudian konfigurasi.

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-drupal`,
      options: {
        baseUrl: `https://situs-anda`,
        apiBase: `api`, // pilihan, standarnya `jsonapi`
      },
    },
  ],
}
```

3. Jalankan peladen pengembangan dengan cara `gatsby develop`, dan buka GraphQL explorer pada `http://localhost:8000/___graphql`. Pada tab Explorer, Anda akan melihat tipe-tipe simpul, misalnya `allBlockBlock` untuk blok Drupal, dan satu untuk tiap tipe konten di situs Drupal Anda. Sebagai contoh, jika Anda memiliki tipe konten "Halaman", akan tersedia sebagai `allNodePage`. Untuk query semua simpul "Halaman" untuk judul dan body, gunakan query sebagaimana berikut ini:

```graphql
{
  allNodePage {
    edges {
      node {
        title
        body {
          value
        }
      }
    }
  }
}
```

4. Untuk menggunakan data Drupal Anda, buatlah sebuah halaman baru di situs Gatsby anda di `src/pages/drupal.js`. Halaman ini akan membuat daftar keseluruhan semua simpul "Halaman" Drupal. 

_**Catatan:**Schema GraphQL yang tepat persis bergantung kepada bagaimana Anda membuat struktur dari instance Drupal_

```jsx:title=src/pages/drupal.js
import React from "react"
import { graphql } from "gatsby"

const DrupalPage = ({ data }) => (
  <div>
    <h1>Halaman Drupal</h1>
    <ul>
    {data.allNodePage.edges.map(({ node, index }) => (
      <li key={index}>
        <h2>{node.title}</h2>
        <div>
          {node.body.value}
        </div>
      </li>
    ))}
   </ul>
  </div>
)

export default DrupalPage

export const query = graphql`
  {
  allNodePage {
    edges {
      node {
        title
        body {
          value
        }
      }
    }
  }
}
```

5. Ketika peladen pengembangan berjalan, Anda dapat melihat halaman baru dengan mengunjungi `http://localhost:8000/drupal`.

#### Sumber daya tambahan

- [Menggunakan Drupal yang terpisah dengan Gatsby](/blog/2018-08-13-using-decoupled-drupal-with-gatsby/)
- [Selengkapnya sumber dari Drupal](/docs/sourcing-from-drupal)
- [Tutorial: Membuat halaman dari data secara terprogram](/tutorial/part-seven/)

## 6. Query data

### Query data dengan Halaman Query

Anda dapat menggunakan label `graphql` untuk query data pada halaman situs Gatsby Anda. Hal ini memberikan Anda akses kepada aja saja termasuk lapisan data Gatsby, seperti metadata, plugin sumber, gambar, dan lainnya. 

#### Petunjuk

1. Impor `graphql` dari `gatsby`.

2. Ekspor sebuah nama konstan `query` dan atur nilainya menjadi template `graphql` dengan query antara dua backtick.

3. Oper `data` sebagai prop pada komponen.

4. Variabel `data` menyimpan query data dan dapat dirujuk pada JSX untuk menghasilkan HTML.

```jsx:title=src/pages/index.js
import React from "react"
// highlight-next-line
import { graphql } from "gatsby"

import Layout from "../components/layout"

// highlight-start
export const query = graphql`
  query HomePageQuery {
    site {
      siteMetadata {
        title
      }
    }
  }
`
// highlight-end

// highlight-next-line
const IndexPage = ({ data }) => (
  <Layout>
    // highlight-next-line
    <h1>{data.site.siteMetadata.title}</h1>
  </Layout>
)

export default IndexPage
```

#### Sumber daya tambahan

- [GraphQL dan Gatsby](/docs/graphql/): paham bentuk data yang diharapkan
- [Selebihnya mengenai query data di halaman dengan GraphQL](/docs/page-query/)
- [MDN untuk Tagged Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) seperti yang digunakan pada GraphQL

### Query data dengan komponen StaticQuery

`StaticQuery` adalah komponen untuk menerima data dari lapisan data Gatsby pada [komponen bukan halaman](/docs/static-query/), seperti header, navigasi, atau komponen child lainnya.

#### Petunjuk

1. The `StaticQuery` Component requires two render props: `query` and `render`.
1. Komponen `StaticQuery` membutuhkan dua prop untuk render: `query` dan `render`.

```jsx:title=src/components/NonPageComponent.js
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const NonPageComponent = () => (
  <StaticQuery
    query={graphql` // highlight-line
      query NonPageQuery {
        site {
          siteMetadata {
            title
          }
        }
      }
    `}
    render={(
      data // highlight-line
    ) => (
      <h1>
        Querying title from NonPageComponent with StaticQuery:
        {data.site.siteMetadata.title}
      </h1>
    )}
  />
)

export default NonPageComponent
```

2. Anda sekarang dapat menggunakan komponen tersebut seperti yang akan anda lakukan terhadap [komponen lainnya](/docs/building-with-components#non-page-components) dengan cara mengimpor ke dalam halaman yang lebih besar dari komponen JSX dan markup HTML.

### Query data dengan hook useStaticQuery 

Sejak gatsby v2.1.0, Anda dapat menggunakan hook `useStaticQuery` untuk query data pada fungsi JavaScript daripada terhadap komponen. Sintak ini menghapus kebutuhan akan komponen `<StaticQuery>` untuk membungkus apa saja, yang mana beberapa orang melihatnya sebagai suatu yang lebih sederhana untuk ditulis.

The `useStaticQuery` hook takes a GraphQL query and returns the requested data. It can be stored in a variable and used later in your JSX templates.

Hook `useStaticQuery` menggunakan GraphQL query dan mengembalikan data yang diminta. Data tersebut dapat diletakkan pada variabel dan digunakan di kemudian hari pada template JSX Anda.

#### Prasyarat

- Anda akan membutuhkan React dan ReactDOM 16.8.0 ke atas  Gatsby akan selalu memperbarui dan memperhatikan hal ini
- Bacaan rekomendasi: [Kaidah React Hooks](https://reactjs.org/docs/hooks-rules.html)

#### Petunjuk

1. Impor `useStaticQuery` dan `graphql` dari `gatsby` untuk menggunakan query hook pada data.

2. Pada permulaan stateless functional component, tetapkan sebuah variabel untuk nilai `useStaticQuery` dengan query `graphql` Anda yang dioper sebagai argumen.

3. Pada JSX kode dikembalikan dari komponen Anda, dan Anda dapat merujuk variable tersebut untuk menanganu balikan data.

```jsx:title=src/components/NonPageComponent.js
import React from "react"
import { useStaticQuery, graphql } from "gatsby" //highlight-line

const NonPageComponent = () => {
  // highlight-start
  const data = useStaticQuery(graphql`
    query NonPageQuery {
      site {
        siteMetadata {
          title
        }
      }
    }
  `)
  // highlight-end
  return (
    <h1>
      Querying title from NonPageComponent: {data.site.siteMetadata.title}{" "}
      //highlight-line
    </h1>
  )
}

export default NonPageComponent
```

#### Sumber daya tambahan

- [Lebih lanjut mengenati Static Query untuk query data di komponen](/docs/static-query/)
- [Perbedaan antara static query dan page query](/docs/static-query/#how-staticquery-differs-from-page-query)
- [Lebih lanjut mengenai hook useStaticQuery](/docs/use-static-query/)
- [Visualisasikan data Anda dengan GraphQL](/docs/introducing-graphiql/)

### Membatasi dengan GraphQL

Ketika query data dengan GraphQL, Anda dapat membatasi jumlah hasil balikan dengan jumlah yang spesifik. Ini sangat membantu jika Anda hanya butuh sedikit data atau butuh untuk [data paginasi](/docs/adding-pagination/).

Untuk membatasi data, Anda akan nutuh situs Gatsby dengan beberapa simpul pada lapisan data GraphQL. Semua situs memiliki beberapa simpul seperti `allSitePage` dan `sitePage` yang dibuat secara otomatis: selebihnya dapat ditambahkan dengan cara memasang plugin sumber seperti `gatsby-source-filesystem` in `gatsby-config.js`.

#### Prasyarat

- Sebuah [situs Gatsby](/docs/quick-start/)

#### Petunjuk

1. Jalankan `gatsby develop` untuk memulai peladen pengembangan.
2. Buka tab di peramban Anda: `http://localhost:8000/___graphql`.
3. Tambahkan sebuah query pada editor dengan fields `allSitePage` untuk memulai sebagai berikut:

```graphql
{
  allSitePage {
    edges {
      node {
        id
        path
      }
    }
  }
}
```

4. Tambahkan `limit` argumen pada `allSitePage` field dan tambahkan nilai integer `3`.

```graphql
{
  allSitePage(limit: 3) { // highlight-line
    edges {
      node {
        id
        path
      }
    }
  }
}
```

5. Pilih tombol play pada halaman GraphQL dan data pada field `edges` akan dibatasi jumlahnya seperti yang sudah dispesifikasi

#### Sumber daya tambahan

- Belajar mengenai [API simpul data pada GraphQL Gatsby](/docs/node-interface/)
- [Rujukan GraphQL Gatsby untuk membuat batasan](/docs/graphql-reference/#limit)
- Contoh langsung:

<iframe
  title="Limiting returned data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(limit%3A%203)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Mengurutkan (sorting) dengan GraphQL

Urutan dari hasil Anda dapat dibuat spesifik dengan argumen `sort` GraphQL. Anda dapat menetapkan field mana yang akan diurutkan (sort by dan sort in).

Pada resep ini, Anda akan membutuhkan situs Gatsby dengan kumpulan simpul untuk mengurutkan pada lapisan data GraphQL, Semua situs memiliki beberapa simpul seperti `allSitePage` yang dibuat otomatis: selebihnya dapat ditambahkan dengan memasang plugin sumber. 

#### Prasyarat

- Sebuah [situs Gatsby](/docs/quick-start)
- Field yang dapat di-query dengan awalan `all`, contoh `allSitePage`

#### Petunjuk

1. Jalankan `gatsby develop` untuk memulai peladen pengembangan.
2. Buka GraphQL explorer pada tab peramban: `http://localhost:8000/___graphql`.
3. Tambah satu query pada editor dengan field pada `allSitePage` untuk memulai sebagai berikut:

```graphql
{
  allSitePage {
    edges {
      node {
        id
        path
      }
    }
  }
}
```

4. Tambah argumen `sort` pada field `allSitePage` dan beri sebuah objek dengan atribut `fields` dan `order`. Nilai pada `fields` dapat sebuah field atau sebuah array dari fields untuk diurutkan (pada contoh ini menggunakan `path` field), `order` dapat antara `ASC` untuk naik atau `DESC` untuk turun. 

```graphql
{
  allSitePage(sort: {fields: path, order: ASC}) { // highlight-line
    edges {
      node {
        id
        path
      }
    }
  }
}

```

5. Tekan tombol play pada halaman GraphQL dan balikan data akan diurutkan secara naik dengan field `path`.

#### Sumber daya tambahan

- [GraphQL Gatsby rujukan untuk mengurutkan](/docs/graphql-reference/#sort)
- Belajar mengenai [API data simpul GraphQL Gatsby](/docs/node-interface/)
- Contoh langsung:

<iframe
  title="Sorting data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allSitePage(sort%3A%20%7Bfields%3A%20path%2C%20order%3A%20ASC%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20path%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Menyaring (filtering) dengan GraphQLsby-transformer-remark` in `gatsby-config.js` to produce `allMarkdownRemark`.

Hasil query dapat disaring dengan operator seperti `eq` (equals), `ne` (not equals), `in`, dan `regex` pada field yang spesifik.

Pada resep ini, Anda akan membutuhkan situs Gatsby dengan kumpulan simpul untuk menyaring lapisan data GraphQL. Semua situs memiliki beberapa simpul seperti `allSitePage` yang dibuat secara otomatis: selebihnya dapat ditambahkan dengan cara memasang sumber dan plugin transformer seperti `gatsby-source-filesystem` dan `gatsby-transformer-remark` pada `gatsby-config.js` untuk menghasilkan `allMarkdownRemark`.

#### Prasyarat

- Sebuah [situs Gatsby](/docs/quick-start)
- Field yang dapat di-query dengan awalan `all`, contoh `allSitePage` atau `allMarkdownRemark`

#### Petunjuk

1. Jalankan `gatsby develop` untuk memulai peladen pengembangan.
2. Buka GraphQL explorer pada tab peramban: `http://localhost:8000/___graphql`.
3. Tambah satu query pada editor dengan field yang diawali dengan 'all' seperti `allMarkdownRemark` (artinya akan memberikan balikan daftar dari simpul-simpul)

```graphql
{
  allMarkdownRemark {
    edges {
      node {
        frontmatter {
          title
          categories
        }
      }
    }
  }
}
```

4. Tambah argumen `filter` pada field `allMarkdownRemark` dan beri sebuah objek dengan field yang akan Anda saring (filter by). Pada contoh ini, konten Markdown akan disaring dengan atribut `categories` pada metadata frontmatter. Nilai selanjutnya adalah operator: pada hal ini `eq`, atau equals (sama), dengan nilai 'makhluk magis'.

```graphql
{
  allMarkdownRemark(filter: {frontmatter: {categories: {eq: "makhluk magis"}}}) { // highlight-line
    edges {
      node {
        frontmatter {
          title
          categories
        }
      }
    }
  }
}
```

5. Tekan tombol play pada halaman GraphQl. Data yang sesuai dengan parameter filter akan dibalikkan, pada hal ini hanya berkas Markdown yang ditandai dengan kategori 'makhlus magis'.

#### Sumber daya tambahan

- [Rujukan GraphQL Gatsby untuk filtering](/docs/graphql-reference/#filter)
- [Daftar lengkap operator yang tepat](/docs/graphql-reference/#complete-list-of-possible-operators)
- Belajar mengenai [simpul pada API data GraphQL Gatsby](/docs/node-interface/)
- Contoh langsung:

<iframe
  title="Filtering data"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20allMarkdownRemark(filter%3A%20%7Bfrontmatter%3A%20%7Bcategories%3A%20%7Beq%3A%20%22magical%20creatures%22%7D%7D%7D)%20%7B%0A%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20frontmatter%20%7B%0A%20%20%20%20%20%20%20%20%20%20title%0A%20%20%20%20%20%20%20%20%20%20categories%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Istilah lain dari Query GraphQL

Anda dapat mengganti nama sitilah dari field yang ada pada query GraphQL.

Jika anda akan menggunakan dua query pada sumber data yang sama, Anda dapat menggunakan nama/istilah lain untuk menghindari tumbukan query pada nama/istilah yang sama

#### Petunjuk

1. Jalankan `gatsby develop` untuk memulai peladen pengembangan.
2. Buka GraphQL explorer pada tab peramban: `http://localhost:8000/___graphql`.
3. Tambahkan satu query pada editor menggunakan dua field dengan nama yang sama seperti `allFile`

```graphql
{
  allFile {
    totalCount
  }
  allFile {
    pageInfo {
      currentPage
    }
  }
}
```

4. Tambahkan nama/istilah yang akan digunakan untuk field apa saja, sebelum field yang ada pada schema GraphQL, dipisahkan dengan titik dua. (Contoh `[alias-name]: [original-name]`)

```graphql
{
  fileCount: allFile { // highlight-line
    totalCount
  }
  filePageInfo: allFile { // highlight-line
    pageInfo {
      currentPage
    }
  }
}
```

5. Tekan tombol play pada halaman GraphQL dan dua objek dengan nama lain yang sudah Anda berikan akan menjadi keluarannya.

#### Sumber daya tambahan

- [GraphQL Gatsby rujukan untuk memberikan nama lain](/docs/graphql-reference/#aliasing)
- Contoh langsung:

<iframe
  title="Using aliases"
  src="https://711808k40x.sse.codesandbox.io/___graphql?query=%7B%0A%20%20fileCount%3A%20allFile%20%7B%20%0A%20%20%20%20totalCount%0A%20%20%7D%0A%20%20filePageInfo%3A%20allFile%20%7B%0A%20%20%20%20pageInfo%20%7B%0A%20%20%20%20%20%20currentPage%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&explorerIsOpen=false"
  width="600"
  height="300"
/>

### Fragmen Query GraphQL

Fragmen GraphQL adalah bingkahan yang dapat dibagi oleh query dan dapat digunakan kembali.

Anda mungkin ingin menggunakannya untuk membagi berbagai field antar query atau untuk menempatkan sebuah komponen dengan data yang digunakan.

#### Petunjuk

1. Deklarasikan sebuah template string `graphql` dengan Fragmen di dalamnya. Fragmen sebaiknya dibuat dengan kata kunci `fragment`, nama, tipe GraphQL terkait (pada hal ini tipe `Site`, didemonstrasikan sebagai `on Site`), dan field yang membentuk fragmen:

```jsx
export const query = graphql`
  // highlight-start
  fragment SiteInformation on Site {
    title
    description
  }
  // highlight-end
`
```

2. Sekarang, muat fragmen pada query untuk tipe field yang telah dispesifikasikan oleh fragmen. Sekaligus muat field tersebut tanpa harus mendeklarasikan semuanya secara terpisah.

```diff
export const pageQuery = graphql`
  query SiteQuery {
    site {
-     title
-     description
+   ...SiteInformation
    }
  }
`
```

**Catatan**: Fragmen tidak perlu untuk diimpor pada Gatsby. Ekspor sebuah query dengan Fragmen membuat Fragmen tersebut tersedia pada _semua_ query pada proyek Anda.

Fragmen dapat dibuat nested di dalam fragmen lainnya, dan penggunaan banyak fragmen dapat digunakan pada query yang sama.

#### Sumber daya tambahan

- [Contoh repo menggunakan fragmen secara sederhana](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-fragments)
- [Rujukan fragmen GraphQL Gatsby](/docs/graphql-reference/#fragments)
- [Fragmen gambar Gatsby](/docs/gatsby-image/#image-query-fragments)
- [Contoh repo dengan data yang ditempatkan](https://github.com/gatsbyjs/gatsby/tree/master/examples/gatsbygram)

## 7. Bekerja dengan Gambar

### Impor gambar ke dalam komponen dengan webpack

Gambar dapat diimpor ke dalam modul JavaScript dengan webpack. Proses ini otomatis memperkecil dan menyalin gambar ke berkas `public` situs Anda, memberikan URL gambar dinamis untuk Anda melalui elemen HTML `<img>` seperti path umum lainnya.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-import-a-local-image-into-a-gatsby-component-with-webpack"
  lessonTitle="Import a Local Image into a Gatsby Component with webpack"
/>

#### Prasyarat

- Sebuah [Gatsby Site](/docs/quick-start) dengan sebuah berkas `.js` yang diekspor ke komponen React
- Sebuah gambar (`.jpg`, `.png`, `.gif`, `.svg`, etc.) pada direktori `src`

#### Petunjuk

1. Impor berkas Anda dari path-nya pada berkas `src`:

```jsx:title=src/pages/index.js
import React from "react"
// Menunjukkan webpack bahwa berkas JS menggunakan gambar ini
import FiestaImg from "../assets/fiesta.jpg" // highlight-line
```

2. Pada `index.js` tambahkan sebuah tag `<img>` dengan `src` sebagai nama yang Anda gunakan ketika impor dari webpack (pada `FiestaImg`), dan tambahkan sebuah attribut `alt` [mendeskripsikan gambar](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"
import FiestaImg from "../assets/fiesta.jpg"

export default () => (
  // Hasil impor adalah URL dari gambar Anda
  <img src={FiestaImg} alt="A dog smiling in a party hat" /> // highlight-line
)
```

3. Jalankan `gatsby develop` untuk memulai peladen pengembangan.
4. Lihat gambar Anda pada peramban: `http://localhost:8000/`

#### Sumber daya tambahan

- [Contoh repo impor sebuah gambar dengan webpack](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-webpack-image)
- [Selebihnya mengenai teknik manipulasi gambar di Gatsby](/docs/images-and-files/)

### Referensi sebuah gambar pada berkas `static`

Sebuah alternatif untuk impor asset dengan webpack, berkas `static` mengizinkan akses konten yang mana otomatis tersalin ke berkas `public` setelah ter-build.

Ini adalah sebuah **rute pelarian** untuk [kasus spesifik](/docs/static-folder/#when-to-use-the-static-folder), dan beragam metode lainnya seperti [impor dengan webpack](#import-an-image-into-a-component-with-webpack) merupakan rekomendasi untuk pengoptimalan performa dari Gatsby.

<EggheadEmbed
  lessonLink="https://egghead.io/lessons/gatsby-use-a-local-image-from-the-static-folder-in-a-gatsby-component"
  lessonTitle="Use a local image from the static folder in a Gatsby component"
/>

#### Prasyarat

- Sebuah [Gatsby Site](/docs/quick-start) dengan sebuah berkas `.js` yang diekspor ke komponen React
- Sebuah gambar (`.jpg`, `.png`, `.gif`, `.svg`, etc.) pada direktori `src`

#### Petunjuk

1. Pastikan gambar pada berkas `static` Anda terletak pada root proyek Anda. Struktur proyek Anda mungkin akan seperti ini:

```
├── gatsby-config.js
├── src
│   └── pages
│       └── index.js
├── static
│       └── fiesta.jpg
```

2. Pada `index.js`, tambahkan tag `<img>` dengan `src` sebagai path relatif pada berkas dari direktori `static`, dan tambahkan atribut `alt` [mendeskripsikan gambar](https://webaim.org/techniques/alttext/):

```jsx:title=src/pages/index.js
import React from "react"

export default () => (
  <img src={`fiesta.jpg`} alt="Seekor anjing tersenyum pada " /> // highlight-line
)
```

3. Jalankan `gatsby develop` untuk memulai peladen pengembangan.
4. Lihat gambar anda pada peramban: `http://localhost:8000/`

#### Sumber daya tambahan

- [Contoh repo yang mereferensikan sebuah gambar pada berkas statis](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipe-static-image)
- [Menggunakan Folder Static](/docs/static-folder/)
- [Selengkapnya teknik manipulasi gambar pada Gatsby](/docs/images-and-files/)

### Optimisasi dan query gambar lokal dengan gatsby-image

Plugin `gatsby-image` dapat meringankan beban yang berkaitan dengan optimisasi gambar pada situs Anda. Ini akan merawat beban termasuk membuat beberapa ukuran gambar dan dimuat dalam waktu bersamaan.

Gatsby akan membuat sumber daya yang teroptimisasi yang mana dapat di-query dengan GraphQL dan dioper pada komponen gambar Gatsby. 

#### Prasyarat

- Paket `gatsby-image`, `gatsby-transformer-sharp`, dan `gatsby-plugin-sharp` terpasang dan ditambahkan pada array plugin di `gatsby-config`
- [Gambar bersumber](/packages/gatsby-image/#install) pada `gatsby-config` menggunakan plugin seperti `gatsby-source-filesystem`

#### Petunjuk

1. Pertama, impor `Img`, `graphql`, dan `useStaticQuery` dari `gatsby-image`. 

```jsx
import { useStaticQuery, graphql } from "gatsby" // untuk query data gambar
import Img from "gatsby-image" // untuk mengambil data dari gambar dan me-render-nya
```

2. Tulis sebuah query untuk mengambil data gambar, dan oper data ke dalam komponen `<Img />`:

Pilih salah satu dari (bisa lebih) dari pilihan berikut.

a. satu gambar yang di-query dari berkas tersebut [path](/docs/content-and-data/) (Contoh: `images/corgi.jpg`)

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) { // highlight-line
      childImageSharp {
        fluid {
          base64
          aspectRatio
          src
          srcSet
          sizes
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="Seekor corgi tersenyum bahagia" />
)
```

b. menggunakan [GraphQL fragment](/docs/using-fragments/), untuk query field yang diperlukan lebih singkat

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fluid {
          ...GatsbyImageSharpFluid // highlight-line
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="Seekor corgi tersenyum bahagia" />
)
```

c. beberapa gambar dari sebuah direktori (Contoh: `images/dogs`) [terfilter](/docs/graphql-reference/#filter) dengan `extension` dan field `relativeDirectory`, kemudian di-map ke dalam komponen `Img`.

```jsx
const data = useStaticQuery(graphql`
  query {
    allFile(
      // highlight-start
      filter: {
        extension: { regex: "/(jpg)|(png)|(jpeg)/" }
        relativeDirectory: { eq: "dogs" }
      }
      // highlight-end
    ) {
      edges {
        node {
          base
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
`)

return (
  <div>
    // highlight-start
    {data.allFile.edges.map(image => (
      <Img
        fluid={image.node.childImageSharp.fluid}
        alt={image.node.base.split(".")[0]} // hanya gunakan bagian dari ektensi berkas dengan dibubuhkan nama berkas
      />
    ))}
    // highlight-end
  </div>
)
```

**Catatan**: Metode ini dapat mempersulit untuk mencocokkan gambar dengan teks `alt` untuk hal aksesbilitas. Pada contoh ini menggunakan teks `alt` termasuk berkas nama, seperti `anjing pada topi pesta.jpg`.

d. sebuah gambar dengan gambar yang sudah pasti(fixed) menggunakan field `fixed` dibandingan `fluid`.


```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fixed(width: 250, height: 250) { // highlight-line
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`)
return (
  <Img fixed={data.file.childImageSharp.fixed} alt="Seekor corgi tersenyum bahagia" />
)
```

e. sebuah gambar dengan ukuran pasti dengan `maxWidth`

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fixed(maxWidth: 250) { // highlight-line
          ...GatsbyImageSharpFixed
        }
      }
    }
  }
`)
return (
  <Img fixed={data.file.childImageSharp.fixed} alt="Seekor corgi tersenyum bahagia" /> // highlight-line
)
```

f. sebuah gambar yang mengisi wadah yang fleksbibel (fluid container) dengan max width (dalam pixels) dan kualitas yang lebih tinggi (nilai standarnya ada 50 sampai dengan 50%)

```jsx
const data = useStaticQuery(graphql`
  query {
    file(relativePath: { eq: "corgi.jpg" }) {
      childImageSharp {
        fluid(maxWidth: 800, quality: 75) { // highlight-line
          ...GatsbyImageSharpFluid
        }
      }
    }
  }
`)

return (
  <Img fluid={data.file.childImageSharp.fluid} alt="Seekor corgi tersenyum bahagia" />
)
```

3. (Pilihan) Tambahkan inline style pada `<Img />` seperti pada komponen lainnya

```jsx
<Img
  fluid={data.file.childImageSharp.fluid}
  alt="Seekor corgi tersenyum bahagia"
  style={{ border: "2px solid rebeccapurple", borderRadius: 5, height: 250 }} // highlight-line
/>
```

4. (Pilihan) paksa sebuah gambar terhadap aspek rasio yang diinginkan dengan menimpa filed `aspectRatio` yang dikembalikan oleh query GraphQL sebelum dioper di komponen `<Img />`

```jsx
<Img
  fluid={{
    ...data.file.childImageSharp.fluid,
    aspectRatio: 1.6, // 1280 / 800 = 1.6
  }}
  alt="Seekor corgi tersenyum bahagia"
/>
```

5. Jalankan `gatsby develop` untuk menghasilkan gambar dari berkas dari sistem berkas (jika belum selesai) dan membuat cache dari gambar tersebut

#### Sumber daya tambahan

- [Contoh repo mengilustrasikan contoh-contoh di atas](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipes-gatsby-image)
- [API Gambar Gatsby](/docs/gatsby-image/)
- [Menggunakan Gambar Gatsby](/docs/using-gatsby-image)
- [Lebih lanjut tentang bekerja dengan gambar di Gatsby](/docs/working-with-images/)
- [Video gratis dari egghead.io menjelasakan langkah demi langkah](https://egghead.io/playlists/using-gatsby-image-with-gatsby-ea85129e)

### Optimisasi dan query gambar pada frontmatter post dengan gatsby-image

Pada kasus seperti gambar unggulan pada bos sebuah blog, Anda tetap _dapat_ menggunakan `gatsby-image`. Komponen `Img` memerlukan data gambar yang diproses, yang mana dapat berasal dari berkas lokal (atau remote), termasuk dari URL pada berkas `.md` atau `.mdx` dari frontmatter.

Untuk gambar inline pada markdown (menggunakan sintaks `![]()`), pertimbangkan menggunakan plugin seperti [`gatsby-remark-images`](/packages/
gatsby-remark-images/)

#### Prasyarat

- Paket `gatsby-image`, `gatsby-transformer-sharp`, dan `gatsby-plugin-sharp` terpasang dan ditambahkan pada array plugin pada `gatsby-config`
- [Gambar yang bersumber](/packages/gatsby-image/#install) pada `gatsby-config` Anda menggunakan plugin seperti `gatsby-source-filesystem`
- Berkas markdown yang bersumber pada `gatsby-config` Anda dengan URL gambar pada frontmatter.
- [Halaman yang sudah dibuat](/docs/creating-and-modifying-pages/) dari Markdown menggunakan [`createPages`](https://www.gatsbyjs.org/docs/node-apis/#createPages)

#### Petunjuk

1. Pastikan berkas Markdown memiliki sebuah URL gambar dengan path yang valid pada berkas gambar di proyek Anda

```mdx:title=post.mdx
---
title: Post pertamaku
featuredImage: ./corgi.png // highlight-line
---

Post content...
```

2. Pastikan pada pengidentifikasi unik (sebuah slug pada contoh ini) diarahkan pada context ketika `createPages` dipanggil pada `gatsby-node.js`, yang mana kemudian akan dioper ke query GraphQL pada komponen Tata letak

```js:title=gatsby-node.js
exports.createPages = async ({ graphql, actions }) => {
  const { createPage } = actions

  // query untuk semua markdown

  result.data.allMdx.edges.forEach(({ node }) => {
    createPage({
      path: node.fields.slug,
      component: path.resolve(`./src/components/markdown-layout.js`),
      // highlight-start
      context: {
        slug: node.fields.slug,
      },
      // highlight-end
    })
  })
}
```

3. Sekarang, impor `Img` pada `gatsby-image` dan `graphql` dari `gatsby` ke komponen tata letak, buat sebuah [pageQuery](/docs/page-query/) untuk mendapatkan data gambar berdasarkan yang dioper pada `slug` dan melewati data pada komponen `<Img />`:

```jsx:title=markdown-layout.jsx
import React from "react"
import { graphql } from "gatsby" // highlight-line
import Img from "gatsby-image" // highlight-line

export default ({ children, data }) => (
  <main>
    // highlight-start
    <Img
      fluid={data.markdown.frontmatter.image.childImageSharp.fluid}
      alt="Seekor corgi tersenyum bahagia"
    />
    // highlight-end
    {children}
  </main>
)

// highlight-start
export const pageQuery = graphql`
  query PostQuery($slug: String) {
    markdown: mdx(fields: { slug: { eq: $slug } }) {
      id
      frontmatter {
        image {
          childImageSharp {
            fluid {
              ...GatsbyImageSharpFluid
            }
          }
        }
      }
    }
  }
`
// highlight-end
```

4. Jalankan `gatsby develop` yang akan menghasilkan gambar pada berkas bersumber pada sistem berkas

#### Sumber daya tambahan

- [Contoh repo menggunakan resep ini](https://github.com/gatsbyjs/gatsby/tree/master/examples/recipes-gatsby-image)
- [Gambar unggulan dengan frontmatter](/docs/working-with-images-in-markdown/#featured-images-with-frontmatter-metadata)
- [API Gambar Gatsby](/docs/gatsby-image/)
- [Menggunakan Gambar Gatsby](/docs/using-gatsby-image)
- [Lebih lanjut tentang bekerja dengan gambar di Gatsby](/docs/working-with-images/)

## 8. Transformasi (mengubah bentuk) data

Transformasi data pada Gatsby adalah plugin-driven (berdasarkan plugin). Plugin transformer (pengubah) mengambil data menggunakan plugin sumber, dan memprosesnya menjadi sesuatu yang dapat dipakai.

### Transformasi Markdown ke dalam HTML

Plugin `gatsby-transformer-remark` dapat mengubah bentuk berkas Markdown menjadi HTML.

#### Prasyarat

- Sebuah situs Gatsby dengan `gatsby-config.js` dan sebuah halaman `index.js`
- Sebuah berkas Markdown yang tersimpan pada direktori `src` situs Gatsby Anda
- Sebuah plugin bersumber yang terpasang, contohnya `gatsby-source-filesystem`
- Plugin `gatsby-transformer-remark` terpasang

#### Petunjuk

1. Tambahkan plugin transformer pada `gatsby-config.js` Anda:

```js:title=gatsby-config.js
plugins: [
  // tidak ditampilkan: gatsby-source-filesystem untuk membuat node kemudian ditransformasi
  `gatsby-transformer-remark`
],
```

2. Tambahkan sebuah query GraphQl pada berkas `index.js` situs Gatsby Anda untuk mendapatkan node dari `MarkdownRemark`:

```jsx:title=src/pages/index.js
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

3. Jalankan ulang peladen pengembangan dan buka GraphQL pada `http://localhost:8000/___graphql`. Jelajahi field yang tersedia pada node `MarkdownRemark`.

#### Sumber daya tambahan

- [Tutorial mengubah bentuk Markdown menjadi HTML](/tutorial/part-six/#transformer-plugins) menggunakan `gatsby-transformer-remark`
- Jelajahi plugin transformer yang tersedia pada [pustaka plugin Gatsby](/plugins/?=transformer)

## 9. Deploy situs Anda

Saatnya pertunjukan. Bila Anda sudah merasa cukup dengan situs Anda, Anda sudha siap untuk menjalankannya!

### Mempersiapkan deployment

#### Prasyarat

- Sebuah [Gatsby site](/docs/quick-start)
- [Gatsby CLI](/docs/gatsby-cli) terpasang

#### Petunjuk

1. Memberhentikan peladen pengembangan jika sedang berjalan (`Ctrl + C` pada command line)

2. Untuk path situs yang standar pada direktori root (`/`), jalankan `gatsby build` menggunakan Gatsby CLI pada command line. Berkas yang sudah ter-build akan terletak pada berkas `folder`.

```shell
gatsby build
```

3. Untuk mengikutsertakan path lainnya selain `/` (contohnya `/nama-situs/`), atur sebuah awalan path dengan nembahkan hal berikut pada `gatsby-config.js` Anda mengganntikan `pathprefixanda` dengan awalan (prefix) yang diinginkan:

```js:title=gatsby-config.js
module.exports = {
  pathPrefix: `/pathprefixanda`,
}
```

Ada beberapa alasan untuk melakukan hal ini -- contohnya, hos sebuah blog yang dibuat dengan gatsby pada sebuah domain dengan situs lainnya yang tidak dibuat dengan Gatsby. Situ utama akan diarahkan ke `contoh.com`, dan situs Gatsby akan diarahkan ke path prefix yang terdapat pada `contoh.com/blog`.

4. Dengan path prefix yang diatur pada `gatsby-config.js`, jalankan `gatsby build` dengan flag `--prefix-paths`, maka akan secara otomatis menambahkan prefix (awalan) pada semua URL situs Gatsby dan tag `<Link>`.


```shell
gatsby build --prefix-paths
```

5. Pastikan situs Anda tampil sama persis ketika menjalankan `gatsby build` maupun `gatsby develop`. Dengan `gatsby serve`ketika Anda build situs Anda, Anda dapat menguji (debug kalau diperlukan) produk yang sudah selesai sebelum di-deploy.

```shell
gatsby build && gatsby serve
```

#### Sumber daya tambahan

- Build dan deploy sebuah contoh situs [tutorial bab pertama](/tutorial/part-one/#deploying-a-gatsby-site)
- Belajar mengenai [optimisasi performa](/docs/performance/)
- Baca mengenai [topik yang berhubungan dengan deployment](/docs/preparing-for-deployment/)
- Cek [dokumentasi deployment](/docs/deploying-and-hosting/) untuk hosting platform yang spesifik dan bagaimana deploy pada platform tersebut

### Deploy ke Netlify

Gunakan [`netlify-cli`](https://www.netlify.com/docs/cli/) untuk deploy aplikasi Gatsby Anda tanpa meninggalkan tampilan command line.

#### Prasyarat

- Sebuah [situs Gatsby](/docs/quick-start) dengan satu komponen `index.js`
- Paket [Netlify-cli](https://www.npmjs.com/package/netlify-cli) terpasang
- [Gatsby CLI](/docs/gatsby-cli) terpasang

#### Petunjuk

1. Build aplikasi Gatsby Anda menggunakan `gatsby build`

2. Masuk ke Netlify menggunakan `netlify login`

3. Jalankan perintah `netlify init`. Pilih opsi "Create & configure a new site".

4. Pilih nama situs yang diinginkan dan tekan enter kalau ingin mendapatkan nama yang acak

5. Pilih [tim Anda](https://www.netlify.com/docs/teams/).

6. Ganti path deploy menjadi `public/`.

7. Pastikan semuanya berjalan dengan baik sebelum deploy ke production menggunakan `netlify deploy --prod`

#### Sumber daya tambahan

- [Hosting menggunakan Netlify](/docs/hosting-on-netlify)
- [gatsby-plugin-netlify](/packages/gatsby-plugin-netlify)

### Deploy ke ZEIT Now

Gunakan [Now CLI](https://zeit.co/download) untuk deploy aplikasi Gatsby Anda tanpa meninggalkan tampilan command line.

#### Prasyarat

- Sebuah akun [ZEIT Now](https://zeit.co/signup)
- Sebuah [situs Gatsby](/docs/quick-start) dengan satu komponen `index.js`
- Paket [Netlify-cli](https://www.npmjs.com/package/netlify-cli) terpasang
- [Gatsby CLI](/docs/gatsby-cli) terpasang


#### Petunjuk

1. Masuk ke Now CLI menggunakan `now login`

2. Ganti ke direktori dari aplikasi Gatsby.js Anda pada Terminal jika ANda belum di sana.

3. Jalankan `now` untuk deploy

#### Sumber daya tambahan

- [Deploy ke ZEIT Now](/docs/deploying-to-zeit-now/)

---
title: Pengenalan Styling di Gatsby
typora-copy-images-to: ./
disableTableOfContents: true
---

<!-- Idea: Create a glossary to refer to. A lot of these terms get jumbled -->

<!--
  - Global styles
  - Component css
  - CSS-in-JS
  - CSS Modules

-->

Selamat datang di bagian dua dari tutorial Gatsby!

## Apa yang ada di dalam tutorial ini?

Pada bagian ini, Anda akan menjelajahi pilihan untuk _styling_ situs web Gatsby dan menyelam lebih dalam tentang penggunaan komponen React untuk membangun situs.

## Menggunakan global styles

Setiap situs memiliki semacam _global style_. Ini termasuk hal-hal seperti tipografi dan warna latar belakang. Style ini mengatur keseluruhan nuansa situs — sangat mirip dengan warna dan tekstur dinding yang mengatur nuansa keseluruhan ruangan.

### Membuat global style dengan CSS standar

Salah satu cara yang paling mudah dalam menambahkan _global style_ ke sebuah situs adalah menggunakan global `.css` _stylesheet_.

#### ✋ Membuat situs Gatsby baru

Dimulai dengan membuat situs Gatsby baru. Baiknya (khususnya jika Anda masih awam terhadap _command line_) Anda menutup _terminal windows_ yang digunakan untuk [bagian satu](/tutorial/part-one/) dan memulai sesi _terminal_ baru untuk bagian dua.

Buka _terminal window_ baru, buat sebuah situs gatsby "hello world" baru dan jalankan server pengembangan:

```shell
gatsby new tutorial-part-two https://github.com/gatsbyjs/gatsby-starter-hello-world
cd tutorial-part-two
```

Sekarang Anda memiliki situs Gatsby baru (berdasarkan pada Gatsby "hello world" _starter_) dengan struktur sebagai berikut:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
```

#### ✋ Tambah style pada berkas css

1. Buat berkas `.css` di dalam proyek baru Anda:

```shell
cd src
mkdir styles
cd styles
touch global.css
```

> Catatan : jangan ragu untuk membuat direktori dan berkas menggunakan _code editor_ jika Anda menginginkannya.

Anda sekarang seharusnya memiliki struktur seperti ini:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
```

2. Definisikan beberapa styles di dalam berkas `global.css`:

```css:title=src/styles/global.css
html {
  background-color: lavenderblush;
}
```

> Catatan: penempatan contoh berkas css di dalam diretori `/src/styles/` bersifat acak.

#### ✋ Muat stylesheet ke dalam `gatsby-browser.js`

1. Buat berkas `gatsby-browser.js`

```shell
cd ../..
touch gatsby-browser.js
```

Struktur berkas proyek Anda sekarang seharusnya terlihat seperti ini:

```text
├── package.json
├── src
│   └── pages
│       └── index.js
│   └── styles
│       └── global.css
├── gatsby-browser.js
```

> 💡 Apa itu `gatsby-browser.js`? Jangan terlalu khawatir tentang ini untuk sekarang, pahami saja bahwa `gatsby-browser.js` merupakan salah satu dari beberapa berkas khusus yang Gatsby cari dan gunakan (jika ada). Disini, penamaan berkas **merupakan** sesuatu yang penting. Jika Anda ingin mendalami lebih jauh sekarang, Periksa [dokumentasi](/docs/browser-apis/).

2. Impor stylesheet yang baru saja Anda buat ke dalam berkas `gatsby-browser.js`:

```javascript:title=gatsby-browser.js
import './src/styles/global.css';

// or:
// require('./src/styles/global.css')
```

> Catatan: Baik sintaksis CommonJS (`require`) maupun ES Module (`import`) berfungsi disini. Jika Anda tidak yakin memilih yang mana, Kita kebanyakan menggunakan `import` seiring waktu.

3. Jalankan server pengembangan:

```shell
gatsby develop
```

Jika Anda melihat proyek pada peramban, Anda seharusnya melihat penerapan latar belakang lavender pada "hello world" _starter_:

![Lavender Hello World!](global-css.png)

> Tip: Bagian ini berfokus pada cara tercepat dan termudah untuk memulai styling pada situs Gatsby — impor standar berkas CSS secara langsung menggunakan `gatsby-browser.js`. Pada kebanyakan kasus, cara terbaik menambahkan global styles adalah dengan _shared layout component_. [Telusur dokumentasi](/docs/global-css/) untuk penjelasan lebih tentang pendekatan itu.

## Menggunakan component-scoped CSS

Sejauh ini, kita telah membahas tentang pendekatan yang lebih tradisional tentang penggunaan standar css stylesheet. Sekarang, kita akan membahas beragam metode tentang modularisasi CSS untuk menangani styling berbasis komponen.

### Modul CSS

Mari kita jelajahi **CSS Module**. Dikutip dari
[the CSS Module homepage](https://github.com/css-modules/css-modules):

> **CSS Module** merupakan berkas CSS yang mana semua nama kelas dan nama animasi
> normalnya dicakup secara lokal.

CSS Modules sangat populer karena CSS Modules mengizinkan Anda menulis CSS secara normal namun dengan banyak keamanan. CSS Modules secara otomatis menghasilkan nama kelas dan animasi unik, jadi Anda tidak perlu khawatir tentang penamaan _selector_ yang sama.

Gatsby berfungsi _out of the box_ dengan CSS Modules. Pendekatan ini sangat direkomendasikan untuk mereka yang awam dalam pengembangan menggunakan Gatsby (dan React pada umumnya).

#### ✋ Build a new page using CSS Modules

Pada bagian ini, Anda akan membuat komponen halaman baru dan style yang digunakan halaman komponen menggunakan CSS Module.

Pertama, buat komponen `Container` baru.

1. Buat direktori baru pada `src/components` lalu, dalam direktori tersebut, buat berkas dengan nama `container.js` dan tempel kode berikut:

```javascript:title=src/components/container.js
import React from 'react';
import containerStyles from './container.module.css';

export default ({ children }) => (
  <div className={containerStyles.container}>{children}</div>
);
```

Anda akan melihat Anda mengimpor file modul css bernama `container.module.css`. Mari kita buat file itu sekarang.

2. Pada direkori yang sama (`src/components`), buat sebuah berkas `container.module.css` dan salin/tempel kode berikut:

```css:title=src/components/container.module.css
.container {
  margin: 3rem auto;
  max-width: 600px;
}
```

Anda akan melihat bahwa nama file diakhiri dengan `.module.css` alih-alih`.css` biasa. Ini adalah cara Anda memberi tahu Gatsby bahwa file CSS ini harus diproses sebagai modul CSS daripada CSS biasa.

3. Buat komponen halaman baru dengan cara membuat berkas baru pada
   `src/pages/about-css-modules.js`:

```javascript:title=src/pages/about-css-modules.js
import React from 'react';

import Container from '../components/container';

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
);
```

Sekarang, jika Anda mengunjungi `http://localhost:8000/about-css-modules/`, Halaman Anda seharusnya terlihat seperti ini:

![Halaman dengan CSS module styles](css-modules-basic.png)

#### ✋ Style sebuah komponen menggunakan CSS Modules

Pada bagian ini, Anda akan membuat sebuah daftar orang dengan nama, avatar, dan biografi singkat dalam bahasa Latin. Anda akan membuat sebuah komponen `<User />` dan menerapkan style pada komponen tersebut menggunakan CSS module.

1. Buat berkas untuk CSS pada `src/pages/about-css-modules.module.css`.

2. Tempel kode berikut ke dalam berkas baru:

```css:title=src/pages/about-css-modules.module.css
.user {
  display: flex;
  align-items: center;
  margin: 0 auto 12px auto;
}

.user:last-child {
  margin-bottom: 0;
}

.avatar {
  flex: 0 0 96px;
  width: 96px;
  height: 96px;
  margin: 0;
}

.description {
  flex: 1;
  margin-left: 18px;
  padding: 12px;
}

.username {
  margin: 0 0 12px 0;
  padding: 0;
}

.excerpt {
  margin: 0;
}
```

3. Impor berkas baru `src/pages/about-css-modules.module.css` ke dalam halaman `about-css-modules.js` yang sudah anda buat diawal dengan cara menyunting beberapa baris pertama pada berkas seperti:

```javascript:title=src/pages/about-css-modules.js
import React from 'react';
// highlight-next-line
import styles from './about-css-modules.module.css';
import Container from '../components/container';

// highlight-next-line
console.log(styles);
```

kode `console.log(styles)` akan mencatat hasil impor, jadi Anda dapat melihat hasil proses dari berkas`./about-css-modules.module.css`. Jika Anda membuka _developer console_ (menggunkan misalnya _developer tools_ Firefox atau Chrome) pada peramban Anda, Anda akan melihat:

![Hasil Impor CSS module pada console](css-modules-console.png)

Jika Anda membandingkan dengan berkas CSS Anda, Anda akan melihat bahwa setiap kelas sekarang merupakan sebuah kunci pada obyek yang diimpor merujuk pada sebuah string panjang contohnya `avatar` merujuk pada `src-pages----about-css-modules-module---avatar---2lRF7`. Hal ini merupaka nama kelas yang dihasilkan oleh CSS Modules. Mereka dijamin unik terhadap situs Anda. Dan karena Anda harus mengimpornya untuk menggunakan kelas-kelas yang ada, Tidak pernah ada pertanyaan tentang dimana berberapa CSS tersebut sedang digunakan.

4. Buat sebuah komponen `User`.

Buat komponen `<User />` baru dibarisan dalam komponen halaman `about-css-modules.js`. Ubah `about-css-modules.js` menjadi seperti berikut:

```jsx:title=src/pages/about-css-modules.js
import React from 'react';
import styles from './about-css-modules.module.css';
import Container from '../components/container';

console.log(styles);

// highlight-start
const User = props => (
  <div className={styles.user}>
    <img src={props.avatar} className={styles.avatar} alt="" />
    <div className={styles.description}>
      <h2 className={styles.username}>{props.username}</h2>
      <p className={styles.excerpt}>{props.excerpt}</p>
    </div>
  </div>
);
// highlight-end

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
    {/* highlight-start */}
    <User
      username="Jane Doe"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/adellecharles/128.jpg"
      excerpt="I'm Jane Doe. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    <User
      username="Bob Smith"
      avatar="https://s3.amazonaws.com/uifaces/faces/twitter/vladarbatov/128.jpg"
      excerpt="I'm Bob Smith, a vertically aligned type of guy. Lorem ipsum dolor sit amet, consectetur adipisicing elit."
    />
    {/* highlight-end */}
  </Container>
);
```

> Tip: Umumnya, jika Anda menggunakan komponen pada banyak tempat pada sebuah situs, hal itu seharusnya di dalam berkas modulnya sendiri pada direktori `components`. Tetapi, jika hal tersebut hanya digunakan dalam satu berkas, buat dibaris pada berkas yang ada.

Halaman yang telah selesai seharusnya terlihat seperti:

![Halaman daftar User dengan CSS modules](css-modules-userlist.png)

### CSS-in-JS

CSS-in-JS merupakan pendekatan styling berorientasi komponen. Kebanyakan pada umumnya, Hal itu merupakan pola dimana [CSS dibentuk secara _inline_ menggunakan JavaScript](https://reactjs.org/docs/faq-styling.html#what-is-css-in-js).

#### Menngunakan CSS-in-JS dengan Gatsby

Ada banyak pustaka CSS-in-JS berbeda dan kebanyakan sudah memiliki plugin Gatsby. Kita tidak akan membahas contoh CSS-in-JS pada tutorial awal ini, tapi kita menganjurkan Anda untuk [menjelajahi](/docs/styling/) apa yang ekosistem tawarkan. Ada tutorial mini untuk dua pustaka, khususnya, [Emotion](/docs/emotion/) dan [Styled Components](/docs/styled-components/).

#### Bacaan yang disarankan tentang CSS-in-JS

Jika Anda tertarik bacaan lebih lanjut, telusuri [Christopher "vjeux" Chedeau's 2014 presentation that sparked this movement](https://speakerdeck.com/vjeux/react-css-in-js) dan juga [Mark Dalgleish's more recent post "A Unified Styling Language"](https://medium.com/seek-blog/a-unified-styling-language-d0c208de2660).

### Opsi CSS lainnya

Gatsby mendukung hampir setiap opsi styling (jika belum ada plugin untuk opsi CSS favorit Anda, [silahkan berkontribusi!](/contributing/how-to-contribute/))

- [Typography.js](/packages/gatsby-plugin-typography/)
- [Sass](/packages/gatsby-plugin-sass/)
- [JSS](/packages/gatsby-plugin-jss/)
- [Stylus](/packages/gatsby-plugin-stylus/)
- [PostCSS](/packages/gatsby-plugin-postcss/)

and banyak lagi!

## Apa selanjutnya?

Sekarang lanjutkan ke [tutorial bagian tiga](/tutorial/part-three/), dimana Anda akan belajar tentang plugin Gatsby dan komponen layout.

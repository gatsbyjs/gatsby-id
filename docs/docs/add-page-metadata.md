---
title: Menambahkan *Metadata* Halaman
---

Jika anda menjalankan [audit menggunakan *Lighthouse*](/docs/audit-with-lighthouse/), anda dapat perhatikan skor yang kurang baik dalam kategory "SEO". Mari kita bahas bagaimana anda dapat meningkatkan skor tersebut.

Menambahkan metadata ke halaman (seperti judul atau deskripsi) adalah kunci dalam membantu mesin pencari seperti Google memahami konten anda, 
dan memutuskan kapan akan muncul dalam hasil pencarian.

[React Helmet](https://github.com/nfl/react-helmet) adalah pustaka yang menyediakan atarmuka komponen *React* bagi anda untuk mengelola [dokumen *head*](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head).

[Plugin *react helmet* Gatsby](/packages/gatsby-plugin-react-helmet) menyediakan dukungan *drop-in* untuk data *rendering server* yang ditambahkan dengan *React helmet*. Dengan menggunakan plugin ini, atribut yang anda tambahkan ke *React helmet* akan ditambahkan ke halaman HTML statis yang dibuat dengan Gatsby.

### Cara menggunakan `React Helmet` dan `gatsby-plugin-react-helmet`

1. Instal kedua pustaka:

```shell
npm install --save gatsby-plugin-react-helmet react-helmet
```

2. Tambahkan plugin ke array `plugins` dalam file `gatsby-config.js` anda.

```javascript:title=gatsby-config.js
{
  plugins: [`gatsby-plugin-react-helmet`]
}
```

3. Gunakan `React Helmet` di halaman anda:

```jsx
import React from "react"
import { Helmet } from "react-helmet"

class Application extends React.Component {
  render() {
    return (
      <div className="application">
        {/* highlight-start */}
        <Helmet>
          <meta charSet="utf-8" />
          <title>Judul Saya</title>
          <link rel="canonical" href="http://mysite.com/example" />
        </Helmet>
        {/* highlight-end */}
      </div>
    )
  }
}
```

> 💡 Contoh diatas berasal dari [dokumentasi *React Helmet*](https://github.com/nfl/react-helmet#example). Periksa untuk info lebih banyak!

Anda mungkin juga tertarik untuk melihat dokumen tentang [menambahkan komponen *SEO*](/docs/add-seo-component/).
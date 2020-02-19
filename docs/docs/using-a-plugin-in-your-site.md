---
title: Menggunakan Plugin pada situs Anda
---

Plugin Gatsby adalah paket Node.js, jadi Anda dapat menginstallnya seperti paket lain menggunakan NPM.

<<<<<<< HEAD
Misalnya, `gatsby-transformer-json` adalah paket yang akan menambahkan dukungan untuk file JSON ke lapisan data Gatsby.
=======
For example, `gatsby-transformer-json` is a package that adds support for JSON files to the Gatsby data layer.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

Untuk menginstallnya, di *root* situs Anda jalankan:

```shell
npm install --save gatsby-transformer-json
```

Kemudian di `gatsby-config.js` pada situs Anda, tambahkan `gatsby-transformer-json` ke dalam array seperti:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [`gatsby-transformer-json`],
}
```

Plugin dapat mengambil opsi. Sebagai contoh:

```javascript:title=gatsby-config.js
module.exports = {
  plugins: [
    // Shortcut for adding plugins without options.
    "gatsby-plugin-react-helmet",
    {
      // Standard plugin with options example
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/data/`,
        name: "data",
      },
    },
    {
      resolve: "gatsby-plugin-offline",
      // Blank options, equivalent to string-only plugin
      options: {
        plugins: [],
      },
    },
    {
      resolve: `gatsby-transformer-remark`,
      options: {
        // plugins inside plugins
        plugins: [`gatsby-remark-smartypants`],
      },
    },
  ],
}
```

Perhatikan bahwa opsi plugin akan dirangkai oleh Gatsby, jadi mereka tidak bisa berupa fungsi.

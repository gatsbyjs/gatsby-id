---
title: Glosarium
disableTableOfContents: true
---

import HorizontalNavList from "../../www/src/components/horizontal-nav-list.js"

Saat Anda baru mengenal Gatsby, ada banyak istilah untuk dipelajari. Glosarium ini bertujuan untuk memberi Anda gambaran 10.000 kaki tentang istilah umum serta arti dan maksud istilah tersebut untuk situs-situs Gatsby.

<HorizontalNavList
items={"ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("")}
slug={props.slug}
/>

## A

### AST

_Abstract Syntax Tree_ atau Pohon Sintaksis Abstrak: Pohon representasi dari kode sumber yang terdapat pada proses [kompilasi](#compiler) antar dua bahasa. Sebagai contoh, [gatsby-transformer-remark](/packages/gatsby-transformer-remark/) akan membuat AST dari [Markdown](#markdown) untuk mendeskripsikan dokumen Markdown dalam sebuah struktur pohon menggunakan _parser_ [Remark](#remark).

### API

_Application Programming Interface_ atau Antarmuka Pemrograman Aplikasi: Metode bagi sebuah aplikasi untuk berkomunikasi dengan aplikasi lainnya. Sebagai contoh, sebuah [_source plugin_](#source-plugin) akan sering menggunakan API untuk mendapatkan data yang diperlukan.

### Aksesibilitas

Penerapan secara inklusif untuk menghilangkan hambatan yang mencegah interaksi dengan, atau akses ke situs web oleh para penyandang cacat. Ketika situs dirancang, dikembangkan dan disunting dengan benar untuk aksesibilitas, umumnya semua pengguna memiliki akses yang sama terhadap informasi dan fungsionalitas. Baca tentang [Komitmen Gatsby untuk Aksesibilitas](/blog/2019-04-18-gatsby-commitment-to-accessibility/).

## B

### Babel

Sebuah alat yang memungkinkan Anda menulis [JavaScript](#javascript) termutakhir, dan ketika proses [_build_](#build) akan [dikompilasi](#compiler) menjadi kode yang dipahami hampir semua peramban web.

### Backend

Belakang layar yang tidak terlihat oleh [publik](#public). Hal ini sering merujuk pada bagian kontrol [CMS](#cms) Anda. _Backend_ biasanya didukung oleh bahasa pemrograman _server-side_ seperti Node.js, PHP, Go, ASP.net, Ruby, atau Java.

### Build

Bagi Gatsby, ini adalah proses mengolah kode dan konten Anda lalu mengemasnya menjadi situs web yang dapat disajikan dan diakses. Umumnya proses ini disebut _build time_. Lihat juga: [_backend_](#backend) dan [_server-side_](#server-side).

## C

### Cache

Penyimpanan lokal informasi yang dapat digunakan kembali, sehingga perhitungan dan pencarian dapat diambil lebih cepat dari satu tempat. Gatsby menggunakan _cache_ untuk menyimpan informasi sehingga dapat membangun situs Anda lebih cepat ketika Anda mengembangkan situs Anda tanpa perlu melakukan pekerjaan yang sama dua kali.

### CLI

_Command Line Interface_ atau Antarmuka Baris Perintah: Aplikasi yang berjalan pada komputer Anda melalui [baris perintah](#command-line) dan berinteraksi dengan papan ketik Anda.

Gatsby memiliki dua antarmuka baris perintah. Yang pertama adalah [`gatsby`](/docs/gatsby-cli/), untuk pengembangan sehari-hari dengan Gatsby dan satu lagi yaitu [`gatsby-dev`](/contributing/setting-up-your-local-dev-environment/#gatsby-repo-install-instructions), untuk mereka yang berkontribusi pada proyek Gatsby.

### Client-side

_Client-side_ merujuk pada operasi yang dilakukan oleh peramban web pengguna pada [hubungan klien–server](https://en.wikipedia.org/wiki/Client%E2%80%93server_model) di dalam jaringan komputer. Pada Gatsby, hal ini penting ketika [bekerja dengan _package_](/docs/using-client-side-only-packages/) yang bergantung pada objek di dalam [DOM peramban web](#dom), seperti `window` atau `navigator`. Lihat juga: [_server-side_](#server-side), [_frontend_](#frontend), dan [_backend_](#backend).

### CMS

_Content Management System_ atau Sistem Manajemen Konten: aplikasi yang memungkinkan Anda mengelola konten Anda dan menyimpannya pada basis data atau file untuk diakses nanti. Beberapa contoh Sistem Manajemen Konten yaitu WordPress, Drupal, Contentful, dan Netlify CMS.

### Command Line

Antarmuka teks untuk menjalankan perintah pada komputer Anda. Aplikasi baris perintah bawaan untuk Mac dan Windows adalah `Terminal` dan `Command Prompt`.

### Compiler

_Compiler_ atau kompilator adalah program yang menerjemahkan kode yang Anda tulis dalam satu bahasa ke bahasa lain. Sebagai contoh [Gatsby](#gatsby) dapat mengkompilasi aplikasi [React](#react) menjadi file [HTML](#html) statis.

### Component

Komponen adalah potongan kode yang independen dan dapat digunakan kembali yang diberdayakan oleh [React](#react) yang, ketika digabungkan, akan menjadi situs web atau aplikasi Anda.

Sebuah komponen dapat terdiri dari beberapa komponen yang berbeda. Bahkan [halaman](#page) dan [_template_](#template) adalah contoh dari komponen.

### Config

File konfigurasi, `gatsby-config.js` memberi tahu Gatsby informasi tentang situs web Anda. Pilihan umum yang diatur dalam konfigurasi adalah _metadata_ situs Anda yang dapat mendukung _SEO meta tag_ Anda.

### [Continuous Deployment](/docs/glossary/continuous-deployment)

_Continuous deployment_ (CD) mengotomatiskan proses merilis pembaruan pada proyek Anda. Alur kerja _continuous deployment_ secara otomatis membangun dan menguji proyek Anda, dan menerbitkan pembaruan Anda hanya ketika pembaruan tersebut lulus tes yang diperlukan.

### CSS

[CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) adalah singkatan dari Cascading Style Sheets dan merupakan bagian utama dari Platform Web bersama dengan [HTML](#html) dan [JavaScript](#javascript). CSS adalah bahasa untuk menata halaman web yang dirancang agar _backwards-compatible_. Saat fitur baru diluncurkan ke pengguna, [parser CSS](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/#CSS_parsing) dapat dengan aman mengabaikan fitur yang tidak didukung serta meningkatkan fitur yang didukung. CSS dapat melakukan hal ini karena didukung dengan desain _cascading_, yang sangat penting untuk penataan halaman web dengan teknik baru seperti [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/CSS_Grid_and_Progressive_Enhancement) sembari memberi alternatif untuk peramban web lama. Gatsby mendukung berbagai [cara penataan](/docs/styling/), termasuk file CSS biasa, CSS modules, dan CSS-in-JS.

## D

### Data Source

Sumber asal konten dan data, biasanya terintegrasi dengan Gatsby melalui [_plugin source_](#source-plugin). Sumber data sering kali adalah [_Headless CMS_](#headless-cms), namun bisa juga mencakup file Markdown, JSON, atau YAML.

### Database

Database adalah kumpulan data atau konten yang terstruktur. Seringkali [CMS](#cms) akan menyimpan ke database menggunakan [teknologi backend](#backend). Database biasa diakses pada proyek Gatsby menggunakan [source plugin](#source-plugin).

### Decoupled

_Decoupling_ menggambarkan pemisahan masalah yang berbeda. Bagi [Gatsby](#gatsby), ini umumnya adalah memisahkan [frontend](#frontend) dari [backend](#backend), seperti dengan [Decoupled Drupal](https://dri.es/how-to-decouple-drupal-in-2019) atau [Headless WordPress](https://www.smashingmagazine.com/2018/10/headless-wordpress-decoupled/).

### [Decoupled Drupal](/docs/glossary/decoupled-drupal)

_Decoupling_ mengacu pada praktik menggunakan Drupal sebagai [_headless CMS_](#headless-cms). Decoupled Drupal berfungsi sebagai API konten yang mengembalikan JSON untuk dikonsumsi [frontend](#frontend) Anda.

### Deploy

Proses [membangun](#build) situs web atau aplikasi Anda dan mengunggahnya ke [penyedia layanan hosting](#hosting).

### Development Environment

[Lingkungan](#environment) tempat Anda mengembangkan kode Anda. Dapat diakses melalui [CLI](#cli) menggunakan perintah `gatsby develop`, yang akan memberikan laporan kesalahan tambahan dan hal-hal untuk membantu Anda melakukan _debug_ sebelum membangun untuk lingkungan [produksi](#production-environment).

### DOM

The Document Object Model, commonly referred to as "the DOM", is a standard browser API that connects web pages to scripts or programming languages by representing the structure of an HTML document in memory. Developers commonly interact with the DOM through [HTML](#html) markup (written in [JSX](#jsx) in Gatsby), as well as both [React](https://reactjs.org/docs/react-dom.html) and [vanilla JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction#DOM_and_JavaScript) code. Another important aspect of utilizing the DOM to its full potential is writing [accessible](#accessibility) HTML markup to expose a page's structure to assistive technology.

## E

### ECMAScript

ECMAScript (sering disebut sebagai ES) adalah spesifikasi bahasa pemrograman. [JavaScript](#javascript) adalah implementasi dari ECMAScript. Seringkali pengembang menggunakan [Babel](#babel) untuk [mengkompilasi](#compiler) kode ECMAScript terbaru menjadi JavaScript yang didukung lebih luas.

### Environment

Lingkungan tempat Gatsby bekerja. Misalnya saat Anda menulis kode, Anda mungkin ingin melakukan _debug_ sebanyak mungkin, tetapi tidak untuk situs web atau aplikasi yang telah tersaji. Oleh karena itu Gatsby dapat menyesuaikan dengan lingkungan kerjanya.

Gatsby memiliki dua lingkungan bawaan, yaitu [lingkungan pengembangan](#development-environment) dan [lingkungan produksi](#production-environment).

### Environment Variables

[Environment Variables](/docs/environment-variables/) allow you to customize the behavior of your app depending on its [environment](#environment). For instance, you may wish to get content from a staging CMS during development and connect to your production CMS when you [build](#build) your site. With environment variables you can set a different URL for each environment.

## F

### Filesystem

Cara penataan file. Bagi Gatsby, ini berarti file berada di tempat yang sama dengan kode situs web atau aplikasi Anda alih-alih menarik data dari [sumber](#data-source) eksternal. Penggunaan _filesystem_ yang umum untuk Gatsby termasuk konten Markdown, gambar, file data, dan aset lainnya.

### Frontend

Antarmuka untuk [khalayak umum](#public) dari situs web atau aplikasi Anda, disampaikan menggunakan teknologi web: HTML, CSS, dan JavaScript. Untuk wawasan lebih lanjut mengenai bagaimana Platform Web menyatukan teknologi-teknologi ini, Anda bisa melihat artikel tentang [Cara Kerja Peramban](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/).

## G

### Gatsby

Gatsby adalah _framework_ situs web modern yang meningkatkan kinerja setiap situs web atau aplikasi dengan memanfaatkan teknologi web terbaru seperti [React](#react), [GraphQL](#graphql), dan [JavaScript](#javascript) modern. Gatsby memudahkan Anda dalam membuat pengalaman web yang cepat dan menarik tanpa perlu menjadi ahli kinerja situs web.

### [GraphQL](/docs/glossary/graphql)

Bahasa [query](#query) yang memungkinkan Anda menarik data menuju situs web atau aplikasi Anda. GraphQL adalah [antarmuka yang digunakan Gatsby](/docs/graphql/) untuk mengelola data situs.

## H

### HTML

Bahasa markup yang dipahami oleh setiap peramban web. HTML adalah singkatan dari _Hypertext Markup Language_. [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) memberi konten web Anda struktur informasi universal, mendefinisikan hal-hal seperti judul, paragraf, dan banyak lagi. HTML juga merupakan kunci untuk menyediakan situs web yang dapat diakses.

### [Headless CMS](/docs/glossary/headless-cms)

[CMS](#cms) yang hanya menangani manajemen konten [_backend_](#backend) alih-alih menangani _backend_ dan [_frontend_](#frontend). Jenis pengaturan ini juga disebut sebagai [_Decoupled_](#decoupled).

### [Headless WordPress](/docs/glossary/headless-wordpress)

Praktek penggunaan JSON yang dihasilkan dari WordPress REST API sebagai [_headless CMS_](#headless-cms). Hal ini memungkinkan Anda menggunakan WordPress untuk menulis dan mengubah konten yang akan dikonsumsi oleh klien mana pun yang mampu menerima JSON.

### Hosting

Penyedia layanan hosting menyimpan salinan situs web atau aplikasi Anda dan membuatnya dapat diakses oleh [publik](#public). [Penyedia layanan hosting yang umum untuk proyek Gatsby](/docs/deploying-and-hosting/) termasuk Netlify, AWS, S3, Surge, Heroku, dan banyak lagi.

### Hot module replacement

Fitur yang digunakan ketika Anda menjalankan `gatsby develop` yang akan memperbarui situs Anda secara langsung ketika Anda menyimpan kode dari _text editor_ dengan secara otomatis mengganti modul, atau potongan kode, di dalam jendela peramban web.

### Hydration

Setelah situs [dibangun](#build) oleh Gatsby dan dimuat di peramban web, file-file JavaScript untuk [_client-side_](#client-side) akan mengunduh dan mengubah situs tersebut menjadi aplikasi React yang mampu memanipulasi [DOM](#dom). Proses ini disebut dengan _re-hydration_ karena proses ini menjalankan kode JavaScript yang digunakan untuk menghasilkan halaman Gatsby, tetapi kali ini dengan API DOM peramban web seperti `window` telah tersedia.

## I

### Inference

As part of its data layer and [build](#build) process, Gatsby will automatically **infer** a [schema](#schema), or type-based structure, based on available data sources (e.g. Markdown file nodes, WordPress posts, etc.). More control can be gained over this structure by using Gatsby's [Schema Customization API](/docs/schema-customization/).

## J

### [JAMStack](/docs/glossary/jamstack)

JAMStack merujuk pada arsitektur web modern menggunakan [JavaScript](#javascript), [API](#api), and _markup_ ([HTML](#html)). Dikutip dari [JAMStack.org](https://jamstack.org): "Ini adalah cara baru dalam membangun situs web dan aplikasi yang memberikan kinerja yang lebih baik, keamanan yang lebih tinggi, biaya penskalaan yang lebih rendah, dan pengalaman pengembang yang lebih baik."

### JavaScript

Bahasa pemrograman yang membantu kita menciptakan halaman web yang dinamis dan interaktif. [JavaScript](https://developer.mozilla.org/en-US/docs/Web/Javascript) adalah teknologi pada peramban web yang banyak digunakan. JavaScript juga digunakan pada aplikasi _server-side_ dengan [Node.js](#node). JavaScript adalah implementasi dari spesifikasi [ECMAScript](#ECMAScript).

### JSX

JSX adalah ekstensi JavaScript yang memungkinkan pengembang menulis HTML dan komponen dalam bagian kode yang sama. [Tim React merekomendasikan](https://reactjs.org/docs/introducing-jsx.html) penggunaannya untuk mendeskripsikan seperti apa tampilan pada [UI](#UI). JSX mungkin mengingatkan Anda pada bahasa _template_, tetapi dilengkapi dengan kekuatan JavaScript. Beberapa perincian penting yang perlu diperhatikan karena JSX menggunakan JavaScript, yaitu beberapa atribut HTML di markup Anda harus diganti untuk menghindari _keyword_ JavaScript (seperti `htmlFor` dan `className`).

## K

## L

### Linting

_Linting_ adalah proses menjalankan program yang akan menganalisis kode untuk mencari kesalahan potensial. Proyek Gatsby menggunakan [prettier](https://prettier.io/) untuk mengidentifikasi dan memperbaiki masalah umum penataan kode sumber. Contoh lain dari _linter_ yang biasa digunakan dalam proyek React adalah [eslint-jsx-plugin-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y), yang memeriksa masalah [aksesibilitas](#accessibility) umum dalam pengembangan.

## M

### MDX

Memperluas [Markdown](#markdown) untuk mendukung [komponen](#component) [React](#react) dalam konten Anda.

### Markdown

Cara menulis konten HTML dengan teks biasa, menggunakan karakter spesial untuk menunjukkan tipe konten seperti simbol hash untuk [judul](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements), dan garis bawah dan tanda bintang untuk penekanan teks.

## N

### NPM

[Node](#node) [Package](#package) Manager. Memungkinkan Anda memasang dan memperbarui _package_ lain yang diperlukan oleh proyek Anda. [Gatsby](#gatsby) dan [React](#react) adalah beberapa contoh dependensi proyek Anda. Lihat juga: [Yarn](#yarn).

### Node

Gatsby menggunakan [_node_ data](/docs/node-interface/) untuk mewakili suatu bagian dari data. Sebuah [sumber data](#data-source) akan menciptakan beberapa _node_.

### [Node.js](/docs/glossary/node)

Program yang memungkinkan Anda menjalankan [JavaScript](#javascript) pada komputer Anda. Gatsby didukung oleh Node.

## O

## P

### Package

_Package_ biasanya mengacu pada program [JavaScript](#javascript) yang memiliki informasi tambahan tentang bagaimana seharusnya didistribusikan dan digunakan, seperti nomor versi. [NPM](#npm) dan [Yarn](#yarn) mengelola dan memasang _package_ yang digunakan proyek Anda. [Gatsby](#gatsby) sendiri adalah sebuah _package_.

### Page

Sebuah halaman [HTML](#html).

Hal ini sering juga merujuk pada [komponen](#component) yang berada di `/src/pages/` dan diolah menjadi halaman oleh [Gatsby](#gatsby), serta [halaman yang dibuat secara dinamis](/docs/creating-and-modifying-pages/#creating-pages-in-gatsby-nodejs) pada file `gatsby-node.js`.

### Plugin

Kode untuk menambahkan fungsionalitas yang belum termasuk pada Gatsby. [_Plugin_ Gatsby](/plugins/) yang umum digunakan meliputi _plugin_ [_source_](#source-plugins) dan [_transformer_](#transformer) untuk menarik dan memanipulasi data.

### Production Environment

[Lingkungan](#environment) untuk situs web atau aplikasi yang [dibangun](#build) yang akan digunakan pengguna ketika akan [_deploy_](#deploy). Dapat diakses melalui [CLI](#cli) menggunakan `gatsby build` atau `gatsby serve`.

### Programmatically

Sesuatu yang terjadi secara otomatis berdasarkan kode dan pengaturan Anda. Misalnya, Anda dapat [mengkonfigurasi](#config) proyek Anda untuk membuat [halaman](#page) untuk setiap posting blog yang ditulis, atau membaca serta menampilkan tahun sebagai bagian dari pernyataan hak cipta pada _footer_ situs Anda.

### Progressive enhancement

Progressive enhancement is a strategy for the web that emphasizes core page content is loaded from a server before anything else, without [JavaScript](#javascript) as a requirement to load. This strategy then progressively adds more complex layers of presentation and features on top of the content as the end user's browser/network connection allow. Gatsby's default approach to [building](#build) pages ahead-of-time means content will load first and enhance as scripts download and execute.

### Public

Biasanya merujuk pada khalayak umum (bukan anggota tim Anda) atau folder `/public` di mana situs web atau aplikasi Anda yang telah [dibangun](#build) tersimpan.

## Q

### Query

Proses meminta data tertentu dari suatu tempat. Dengan Gatsby Anda umumnya meminta data dengan [GraphQL](#graphql).

## R

### [React](/docs/glossary/react)

_Library_ kode (ditulis menggunakan [JavaScript](#javascript)) untuk membangun antarmuka pengguna. Ini adalah _framework_ yang digunakan [Gatsby](#gatsby) untuk membuat halaman dan struktur konten.

### Remark

Sebuah _parser_ untuk menerjemahkan [Markdown](#markdown) menjadi format lain seperti [HTML](#html) atau kode [React](#react).

### Runtime

Runtime is when a program is running (or being executable); it can refer to a few things. [Node.js](#nodejs) is a [server-side](#server-side) runtime that executes JavaScript code. [Client-side JavaScript](#client-side), on the other hand, refers to the browser runtime where traditional JavaScript code executes. Gatsby compiles your site at [build time](#build) and [rehydrates with a React runtime](#hydration) to provide a fast, interactive, and dynamic user experience.

### Routing

_Routing_ adalah mekanisme untuk memuat konten yang diinginkan pada situs atau aplikasi web sesuai permintaan jaringan - biasanya melalui URL. Misalnya, ketika ingin melakukan _routing_ URL seperti `/about-us` menuju [halaman](#page), [template](#template), atau [komponen](#component) yang sesuai.

## S

### Schema

Gambaran bagaimana data tersimpan dalam sebuah sistem, seperti tabel dan kolom pada database atau struktur file JSON. Pada Gatsby, skema GraphQL menggambarkan semua data atau data yang dapat diminta oleh komponen sebagai lapisan data Gatsby.

### Server-side

The server-side part of the [client-server relationship](https://en.wikipedia.org/wiki/Client%E2%80%93server_model) refers to operations performed by a computer program which manages access to a centralized resource or service in a computer network. Gatsby uses the server-side technology [Node.js](#nodejs) to compile pages at build time, as opposed to serving them at [browser runtime](#runtime) with [client-side](#client-side) JavaScript. See also: [frontend](#frontend) and [backend](#backend).

### Source Code

Kode sumber adalah kode yang berada di folder `/src/` dan menjadi aspek unik dari situs web atau aplikasi Anda. Terdiri dari [JavaScript](#javascript) dan terkadang [CSS](#css) dan file lainnya.

Kode sumber tersebut [diolah](#build) menjadi situs yang akan dilihat oleh [publik](#public).

### Source Plugin

[Plugin](#plugin) yang memberikan tambahan [sumber data](#data-source) untuk Gatsby yang kemudian dapat [diminta](#query) oleh [halaman](#page) dan [komponen](#component) Anda.

### Starter

Proyek Gatsby yang telah dikonfigurasi sebelumnya dan dapat digunakan sebagai titik awal untuk proyek Anda. Mereka dapat ditemukan menggunakan [Gatsby Starter Library](/starters/) dan dipasang menggunakan [Gatsby CLI](/docs/starters/).

### Static

Gatsby [membangun](#build) versi statis halaman Anda yang dapat Anda [hosting](#hosting). Berbeda dengan sistem dinamis di mana setiap halaman dibuat ketika dibutuhkan. Situs statis dapat meningkatkan kinerja karena pekerjaan hanya perlu dilakukan sekali untuk setiap konten atau ketika konten berubah.

Hal ini juga merujuk pada folder `/static` yang secara otomatis disalin ke folder `/public` pada setiap [build](#build) untuk file yang tidak perlu diproses oleh Gatsby tetapi perlu berada di [public](#public).

### [Static Site Generator](/docs/glossary/static-site-generator)

A software application that creates HTML pages from templates or [components](#component) and a given content source.

## T

### Template

[Komponen](#component) yang secara [terprogram](#programmatically) diolah menjadi halaman oleh Gatsby.

### Theme

Tema Gatsby seperti tema WordPress yang dapat disusun (dengan tema lain), dapat diperluas (dengan tambahan logika), dan dapat diganti ([dibayangi](/blog/2019-04-29-component-shadowing/)). Tema Gatsby dapat memiliki sisi mana pun dari aplikasi Gatsby yang dikemas di dalamnya, dan juga dapat menawarkan sejumlah fitur yang dapat dihidupkan atau dimatikan.

### Transformer

[_Plugin_](#plugin) yang mengubah satu jenis data menjadi jenis yang lain. Misalnya, Anda dapat mengubah _spreadsheet_ menjadi _array_ [JavaScript](#javascript).

## U

### UI

_UI_ mengacu pada Antarmuka Pengguna. Pada bidang interaksi manusia-komputer, _UI_ adalah ruang di mana interaksi antara manusia dan mesin terjadi. Tujuan dari interaksi ini adalah untuk memungkinkan operasi dan kontrol mesin yang efektif bagi manusia, sementara mesin secara serentak memberi umpan balik informasi yang membantu proses pengambilan keputusan bagi pegguna (seperti pesan kesalahan atau pemberitahuan).

## V

## W

### [webpack](/docs/glossary/webpack)

Aplikasi [JavaScript](#javascript) yang digunakan Gatsby untuk mem-_bundle_ kode sumber situs web Anda. Hal ini terjadi secara otomatis ketika proses [_build_](#build).

## X

## Y

### Yarn

_[Package](#package) manager_ yang lebih disukai beberapa orang daripada [NPM](#npm). Hal ini juga diperlukan untuk [mengembangkan Gatsby](/contributing/setting-up-your-local-dev-environment/#using-yarn).

## Z

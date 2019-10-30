---
title: Menyiapkan Lingkungan Pengembangan Anda
typora-copy-images-to: ./
disableTableOfContents: true
---

Sebelum memulai membangun situs Gatsby pertama Anda, Anda harus membiasakan diri dengan beberapa teknologi inti pada web dan memastikan bahwa Anda telah menginstal semua perangkat lunak yang diperlukan.

## Biasakan diri Anda dengan baris perintah

Baris perintah adalah sebuah antarmuka berbasis teks yang digunakan untuk menjalankan perintah di komputer Anda. Baris perintah juga sering kita ketahui sebagai terminal. Dalam tutorial ini, kita akan menggunakan keduanya secara bergantian. Baris perintah ini sangat mirip seperti kita menggunakan Finder di Mac atau Explorer di Windows. Finder dan Explorer adalah contoh antarmuka pengguna grafis (GUI). Baris perintah adalah cara yang ampuh untuk berinteraksi dengan komputer Anda dengan berbasis teks.

Luangkan waktu sejenak untuk mencari dan membuka antarmuka baris perintah (CLI) untuk komputer Anda. Tergantung pada sistem operasi yang Anda gunakan, lihat [**petunjuk untuk Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**petunjuk untuk Windows**](https://www.quora.com/How-do-I-open-terminal-in-windows) atau [**petunjuk untuk Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

## Instal Homebrew untuk Node.js

Untuk menginstal Gatsby dan Node.js, disarankan untuk menggunakan [Homebrew](https://brew.sh/). Sedikit pengaturan di awal dapat menghindarkan Anda dari permasalahan nantinya!

Cara menginstal atau memverifikasi Homebrew di komputer Anda:

1. Buka Terminal Anda.
2. Lihat apakah Homebrew telah diinstal dengan menjalankan `brew -v`. Anda akan melihat "Homebrew" dan nomor versinya.
3. Jika tidak, unduh dan instal [Homebrew dengan petunjuknya](https://docs.brew.sh/Installation) untuk sistem operasi Anda (Mac, Linux atau Windows).
4. Setelah Anda menginstal Homebrew, ulangi langkah ke-2 untuk memverifikasi.

### Pengguna Mac: instal Baris Perintah Xcode

1. Buka Terminal Anda.
2. Pada Mac, instal baris perintah Xcode dengan menjalankan `xcode-select --install`.
   1. Jika gagal, unduh [langsung dari situs Apple](https://developer.apple.com/download/more/), setelah masuk dengan akun pengembang Apple
3. Setelah diminta untuk memulai proses instalasi, Anda akan diminta untuk menerima lisensi perangkat lunak untuk dapat diunduh.

## ⌚ Instal Node.js dan npm

Node.js adalah sebuah lingkungan yang dapat menjalankan kode JavaScript di luar browser web. Gatsby dibangun dengan Node.js. Untuk memulai dan menjalankan Gatsby, Anda harus memiliki Node.js versi terbaru yang diinstal di komputer Anda.

_Catatan: Versi minimum Node.js yang didukung oleh Gatsby adalah Node 8, akan tetapi jangan ragu untuk menggunakan versi yang lebih baru._

1. Buka Terminal Anda.
2. Jalankan `brew update` untuk memastikan Anda memiliki Homebrew versi terbaru.
3. Jalankan perintah ini untuk menginstal Node dan npm sekaligus: `brew install node`

Setelah Anda mengikuti langkah-langkah instalasi, pastikan semuanya telah diinstal dengan benar:

### Periksa instalasi Node.js Anda

1. Buka Terminal Anda.
2. Jalankan `node --version`. (Jika Anda baru dalam menggunakan baris perintah, “jalankan `command`” berarti “ketik `node --version` di *command prompt*, dan tekan tombol *Enter*”. Dari sini, inilah yang kami maksud dengan “jalankan `command`”).
3. Jalankan `npm --version`.

*Output* dari masing-masing perintah tersebut harus berupa nomor versi. Versi Anda mungkin tidak sama dengan yang ditunjukkan di bawah ini! Jika pada saat Anda memasukkan perintah-perintah tersebut tidak menunjukkan nomor versi Anda, kembali lagi dan pastikan Anda telah menginstal Node.js.

![Periksa versi node dan npm di terminal](01-node-npm-versions.png)

## Instal Git

Git adalah sistem pengelola perubahan yang terdistribusi secara terbuka dan gratis yang dirancang untuk menangani segala sesuatu mulai dari proyek kecil hingga proyek yang sangat besar dengan cepat dan efisien. Saat Anda memasang situs Gatsby "starter", Gatsby menggunakan Git di belakang layar untuk mengunduh dan menginstal file yang diperlukan untuk starter Anda. Anda perlu menginstal Git untuk menyiapkan situs Gatsby pertama Anda.

Langkah-langkah untuk mengunduh dan menginstal Git tergantung pada sistem operasi Anda. Ikuti panduan untuk sistem Anda:

- [Instal Git untuk macOS](https://www.atlassian.com/git/tutorials/install-git#mac-os-x)
- [Instal Git untuk Windows](https://www.atlassian.com/git/tutorials/install-git#windows)
- [Instal Git untuk Linux](https://www.atlassian.com/git/tutorials/install-git#linux)

## Menggunakan Gatsby CLI

Gatsby CLI memungkinkan Anda untuk membuat situs yang didukung oleh Gatsby dengan cepat dan dapat menjalankan perintah-perintah untuk membangun situs Gatsby. Gatsby CLI merupakan sebuah paket yang diterbitkan di npm .

Gatsby CLI tersedia melalui npm dan harus diinstal secara global dengan menjalankan `npm install -g gatsby-cli`.

_**Catatan**: ketika Anda menginstal Gatsby dan dijalankan untuk pertama kalinya, Anda akan melihat pesan singkat yang memberi tahu Anda tentang data penggunaan yang tidak dikenal dimana data tersebut dikumpulkan untuk perintah-perintah Gatsby, Anda dapat membaca lebih lanjut tentang bagaimana data itu diambil dan digunakan dalam [dokumen telemetri](/docs/telemetry)._

Untuk melihat perintah-perintah yang tersedia, jalankan `gatsby --help`.

![Periksa perintah gatsby di terminal](05-gatsby-help.png)

> 💡 Jika Anda tidak berhasil menjalankan Gatsby CLI karena masalah perizinan, Anda mungkin ingin membaca [dokumen npm dalam memperbaiki perizinan](https://docs.npmjs.com/getting-started/fixing-npm-permissions), atau [panduan ini](https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md).

## Membuat situs Gatsby

Sekarang Anda siap menggunakan Gatsby CLI untuk membuat situs Gatsby pertama Anda. Dengan menggunakan Gatsby CLI, Anda dapat mengunduh "starters" (situs yang dibangun dengan beberapa konfigurasi bawaan) untuk membantu Anda bekerja lebih cepat dalam membuat situs dengan jenis tertentu. Starter "Hello World" yang akan Anda gunakan di sini adalah starter yang sudah termasuk konfigurasi penting yang dibutuhkan dalam membuat situs Gatsby.

1. Buka terminal Anda.
2. Jalankan `gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world`. (_Catatan: Tergantung pada kecepatan unduhan Anda, jumlah waktu yang dibutuhkan akan bervariasi. Untuk mempersingkat, gif di bawah ini ditunda selama proses install_).
3. Jalankan `cd hello-world`.
4. Jalankan `gatsby develop`.

<video controls="controls" autoplay="true" loop="true">
  <source type="video/mp4" src="./03-create-site.mp4" />
  <p>Sorry! You browser doesn't support this video.</p>
</video>

Apa yang baru saja terjadi?

```shell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world
```

- `new` adalah perintah gatsby untuk membuat proyek Gatsby yang baru.
- Disini, `hello-world` adalah judul acak - Anda bisa memilih apa saja. CLI akan menempatkan kode untuk situs baru Anda pada folder baru yang disebut “hello-world”.
- Terakhir, GitHub URL akan menentukan poin ke repositori yang berisi kode starter yang akan Anda gunakan.

```shell
cd hello-world
```

- Ini dapat diartikan juga sebagai 'Saya ingin mengubah direktori (`cd`) menjadi *subfolder* “hello-world”'. Kapan pun Anda ingin menjalankan perintah untuk situs Anda, Anda harus berada dalam direktori situs tersebut (alias, terminal Anda perlu diarahkan ke direktori tempat kode situs Anda berada).

```shell
gatsby develop
```

- Perintah ini akan memulai *server* pengembangan. Anda akan dapat melihat dan berinteraksi dengan situs baru Anda di lingkungan pengembangan - lokal (di komputer Anda, tidak dipublikasikan ke internet).

### Lihat situs Anda secara lokal

Buka tab baru di browser Anda dan arahkan ke [**http://localhost:8000**](http://localhost:8000/).

![Periksa beranda](04-home-page.png)

Selamat! Ini merupakan awal dari situs Gatsby pertama Anda! 🎉

Anda dapat mengunjungi situs secara lokal di [**_http://localhost:8000_**](http://localhost:8000/) selama *server* pengembangan Anda berjalan. Itulah proses yang Anda mulai dengan menjalankan perintah `gatsby develop`. Untuk berhenti menjalankan proses tersebut (atau untuk "berhenti menjalankan *server* pengembangan"), kembali ke jendela terminal Anda, tahan tombol "control", dan kemudian tekan "c" (ctrl-c). Untuk memulainya lagi, jalankan `gatsby develop` lagi!

**Catatan:** Jika Anda menggunakan pengaturan VM seperti `vagrant` dan atau ingin terhubung pada alamat IP lokal Anda, jalankan `gatsby develop -- --host=0.0.0.0`. Sekarang, *server* pengembangan terhubung ke 'localhost' dan IP lokal Anda.

## Menyiapkan *code editor*

*Code editor* adalah program yang dirancang khusus untuk mengedit kode. Ada banyak *Code editor* yang bagus di luar sana.

### Unduh VS Code

Dokumentasi Gatsby terkadang menyertakan *screenshots* yang diambil dalam VS Code, jadi jika Anda belum memiliki *Code editor* pilihan, dengan menggunakan VS Code akan dipastikan bahwa layar Anda akan terlihat sama seperti *screenshots* dalam tutorial dan dokumen. Jika Anda memilih untuk menggunakan VS Code, kunjungi [Situs VS Code](https://code.visualstudio.com/#alt-downloads) dan unduh versi yang sesuai untuk *platform* Anda.

### Instal *plugin* Prettier

Kami juga merekomendasikan menggunakan [Prettier](https://github.com/prettier/prettier), sebuat alat yang membantu memformat kode Anda untuk menghindari kesalahan.

Anda dapat menggunakan Prettier secara langsung di *editor* Anda menggunakan [Prettier VS Code plugin](https://github.com/prettier/prettier-vscode):

1. Buka tampilan ekstensi pada VS Code (View => Extensions).
2. Cari "Prettier - Code formatter".
3. Klik "Install". (Setelah instalasi, Anda akan diminta untuk me-*restart* VS Code untuk mengaktifkan ekstensi. Untuk VS Code versi terbaru, VS Code akan secara otomatis mengaktifkan ekstensi setelah diunduh.)

> 💡 Jika Anda tidak menggunakan VS Code, periksa dokumen Prettier untuk [instruksi instalasi](https://prettier.io/docs/en/install.html) atau [integrasi editor lainnya](https://prettier.io/docs/en/editors.html).

## ➡️ Apa berikutnya?

Sebagai rangkuman, pada bagian ini Anda:

- Mempelajari tentang baris perintah dan cara menggunakannya
- Menginstal dan mempelajari tentang Node.js dan npm CLI, sistem pengelola perubahan Git, dan Gatsby CLI
- Menghasilkan situs Gatsby baru dengan menggunakan Gatsby CLI
- Menjalankan *server* pengembangan Gatsby dan mengunjungi situs Anda secara lokal
- Mengunduh *code editor*
- Menginstal pemformat kode yang disebut Prettier

Sekarang, lanjut ke [**mengenal *building blocks* pada Gatsby**](/tutorial/part-one/).

## Referensi

### Gambaran tentang teknologi inti

Tidak perlu menjadi seseorang yang ahli dengan hal ini - jika Anda tidak, jangan khawatir! Anda akan mendapatkan banyak hal melalui seri tutorial ini. Ini adalah beberapa teknologi inti pada web yang akan Anda gunakan saat membangun situs Gatsby:

- **HTML**: Bahasa *markup* yang dapat dipahami oleh setiap browser web. HTML adalah singkatan dari *HyperText Markup Language*. HTML memberikan konten web Anda sebuah struktur informasi yang universal, mendefinisikan hal-hal seperti judul utama, paragraf, dan banyak lagi.
- **CSS**: Bahasa presentasi yang digunakan untuk menata tampilan konten web Anda (font, warna, tata letak, dll). CSS singkatan dari *Cascading Style Sheets*.
- **JavaScript**: Bahasa pemrograman yang membantu kita dalam membuat web menjadi dinamis dan interaktif.
- **React**: Sebuah *library* (dibangun dengan JavaScript) untuk membangun antarmuka pengguna. Ini adalah *framework* yang digunakan Gatsby untuk membangun halaman dan menyusun konten.
- **GraphQL**: Bahasa *query* yang memungkinkan Anda untuk menarik data ke situs web Anda. Ini adalah antarmuka yang digunakan Gatsby untuk mengelola data pada situs.

### Apa itu situs web?

Untuk pengenalan yang komprehensif tentang apa itu situs web - termasuk pengantar ke HTML dan CSS - lihat “[**Membangun halaman web pertama Anda**](https://learn.shayhowe.com/html-css/building-your-first-web-page/)”. Ini adalah tempat yang tepat untuk memulai pembelajaran tentang web. Untuk pengenalan langsung [**HTML**](https://www.codecademy.com/learn/learn-html), [**CSS**](https://www.codecademy.com/learn/learn-css), dan [**JavaScript**](https://www.codecademy.com/learn/introduction-to-javascript), lihat tutorial dari Codecademy. [**React**](https://reactjs.org/tutorial/tutorial.html) dan [**GraphQL**](http://graphql.org/graphql-js/) juga memiliki tutorial pengantar mereka sendiri.

### Pelajari lebih lanjut tentang baris perintah

Tutorial ini sangat bagus untuk Anda yang masih baru dalam menggunakan baris perintah, lihat [**tutorial Baris Perintah oleh Codecademy**](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) untuk pengguna Mac dan Linux, dan [**tutorial ini**](https://www.computerhope.com/issues/chusedos.htm) untuk pengguna Windows. Meskipun Anda pengguna Windows, halaman pertama pada tutorial dari Codecademy sangat layak untuk Anda baca. Tutorial tersebut menjelaskan tentang apa itu baris perintah, bukan hanya bagaimana berinteraksi dengannya.

### Pelajari lebih lanjut tentang npm

npm adalah pengelola paket JavaScript. Paket adalah sebuah modul kode yang dapat Anda pilih untuk dimasukkan ke dalam proyek Anda. Jika Anda baru saja mengunduh dan menginstal Node.js, npm sudah terinstal dengannya!

npm memiliki tiga komponen berbeda: situs web npm, registri npm, dan antarmuka baris perintah (CLI).

- Pada situs web npm, Anda dapat mencari paket JavaScript apa yang tersedia di registri npm.
- Registri npm adalah sebuah database informasi besar tentang paket-paket JavaScript yang tersedia di npm.
- Setelah Anda mengidentifikasi paket yang Anda inginkan, Anda dapat menggunakan npm CLI untuk menginstalnya di proyek Anda atau secara global (seperti CLI lainnya). CLI npm yang akan berinteraksi ke registri - Anda biasanya hanya akan berinteraksi dengan situs web npm atau CLI npm.

> 💡 Lihat pengenalan tentang npm, “[**Apa itu npm?**](https://docs.npmjs.com/getting-started/what-is-npm)”.

### Pelajari lebih lanjut tentang Git

Anda tidak perlu tahu Git untuk menyelesaikan tutorial ini, tetapi Git akan sangat berguna. Jika Anda tertarik untuk mempelajari lebih lanjut tentang pengelola perubahan, Git, dan GitHub, lihat [Pedoman GitHub](https://guides.github.com/introduction/git-handbook/) Github.

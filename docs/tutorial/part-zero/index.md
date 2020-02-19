---
title: Menyiapkan Lingkungan Pengembangan Anda
typora-copy-images-to: ./
disableTableOfContents: true
---

Sebelum memulai membangun situs Gatsby pertama Anda, Anda harus membiasakan diri dengan beberapa teknologi inti pada web dan memastikan bahwa Anda telah menginstal semua perangkat lunak yang diperlukan.

## Biasakan diri Anda dengan *command line*

*Command line* adalah sebuah antarmuka berbasis teks yang digunakan untuk menjalankan perintah di komputer Anda. *Command line* juga sering kita ketahui sebagai terminal. Dalam tutorial ini, kita akan menggunakan keduanya secara bergantian. *Command line* ini sangat mirip seperti kita menggunakan Finder di Mac atau Explorer di Windows. Finder dan Explorer adalah contoh antarmuka pengguna grafis (GUI). *Command line* adalah cara yang ampuh untuk berinteraksi dengan komputer Anda dengan berbasis teks.

<<<<<<< HEAD
Luangkan waktu sejenak untuk mencari dan membuka *command line interface* (CLI) untuk komputer Anda. Tergantung pada sistem operasi yang Anda gunakan, lihat [**petunjuk untuk Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**petunjuk untuk Windows**](https://www.quora.com/How-do-I-open-terminal-in-windows) atau [**petunjuk untuk Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

## Instal Homebrew untuk Node.js

Untuk menginstal Gatsby dan Node.js, disarankan untuk menggunakan [Homebrew](https://brew.sh/). Sedikit pengaturan di awal dapat menghindarkan Anda dari permasalahan nantinya!

Cara menginstal atau memverifikasi Homebrew di komputer Anda:

1. Buka Terminal Anda.
2. Lihat apakah Homebrew telah diinstal dengan menjalankan `brew -v`. Anda akan melihat "Homebrew" dan nomor versinya.
3. Jika tidak, unduh dan instal [Homebrew dengan petunjuknya](https://docs.brew.sh/Installation) untuk sistem operasi Anda (Mac, Linux atau Windows).
4. Setelah Anda menginstal Homebrew, ulangi langkah ke-2 untuk memverifikasi.

### Pengguna Mac: instal Xcode Command Line

1. Buka Terminal Anda.
2. Pada Mac, instal Xcode Command Line dengan menjalankan `xcode-select --install`.
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
2. Jalankan `node --version`. (Jika Anda baru dalam menggunakan *command line*, “jalankan `command`” berarti “ketik `node --version` di *command prompt*, dan tekan tombol *Enter*”. Dari sini, inilah yang kami maksud dengan “jalankan `command`”).
3. Jalankan `npm --version`.

*Output* dari masing-masing perintah tersebut harus berupa nomor versi. Versi Anda mungkin tidak sama dengan yang ditunjukkan di bawah ini! Jika pada saat Anda memasukkan perintah-perintah tersebut tidak menunjukkan nomor versi Anda, kembali lagi dan pastikan Anda telah menginstal Node.js.
=======
Take a moment to locate and open up the command line interface (CLI) for your computer. Depending on which operating system you are using, see [**instructions for Mac**](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/), [**instructions for Windows**](https://www.lifewire.com/how-to-open-command-prompt-2618089) or [**instructions for Linux**](https://www.howtogeek.com/140679/beginner-geek-how-to-start-using-the-linux-terminal/).

_Note: If you’re new to the command line, "running" a command, means "writing a given set of instructions in your command prompt, and hitting the Enter key". Commands will be shown in a highlighted box, something like `node --version`, but not every highlighted box is a command! If something is a command it will be mentioned as something you have to run/execute._

## Install Node.js for your appropriate operating system

Node.js is an environment that can run JavaScript code outside of a web browser. Gatsby is built with Node.js. To get up and running with Gatsby, you’ll need to have a recent version installed on your computer. npm comes bundled with Node.js so if you don't have npm, chances are that you don't have Node.js either.

### Mac instructions

To install Gatsby and Node.js on a Mac, it is recommended to use [Homebrew](https://brew.sh/). A little set-up in the beginning can save you from some headaches later on!

#### How to install or verify Homebrew on your computer:

1. Open your Terminal.
2. See if Homebrew is installed by running `brew -v`. You should see "Homebrew" and a version number.
3. If not, download and install [Homebrew with the instructions](https://docs.brew.sh/Installation).
4. Once you've installed Homebrew, repeat step 2 to verify.

#### Install Xcode Command Line Tools:

1. Open your Terminal.
2. Install Xcode Command line tools by running `xcode-select --install`.
   - If that fails, download it [directly from Apple's site](https://developer.apple.com/download/more/), after signing-in with an Apple developer account
3. After being prompted to start the installation, you'll be prompted again to accept a software license for the tools to download.

#### Install Node

1. Open your Terminal
2. Run `brew install node`
   - If you don't want to install it through Homebrew, download the latest Node.js version from [the official Node.js website](https://nodejs.org/en/), double click on the downloaded file and go through the installation process.

### Windows Instructions

- Download and install the latest Node.js version from [the official Node.js website](https://nodejs.org/en/)

### Linux Instructions

Install nvm (Node Version Manager) and needed dependencies. nvm is used to manage Node.js and all its associated versions.

_💡 If when installing a package, it asks for confirmation, type `y` and press enter._

#### Ubuntu, Debian, and other `apt` based distros:

1. Run `sudo apt update` and then `sudo apt -y upgrade` to make sure your Linux distribution is ready to go.
2. Run `sudo apt-get install curl` to install curl which allows you to transfer data and download additional dependencies.
3. After it finishes installing, run `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash` to download the latest nvm version.
4. To confirm this has worked, use the following command. `nvm --version`. The output should be a version number.
5. [Set default Node.js version](#set-default-nodejs-version)

#### Arch, Manjaro and other `pacman` based distros:

1. Run `sudo pacman -Sy` to make sure your distribution is ready to go.
2. These distros come installed with curl, so you can use that to download nvm.
   `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash`
3. Before using nvm, you need to install additional dependencies by running `sudo pacman -S grep awk tar`.
4. To confirm this has worked, use the following command. `nvm --version`. The output should be a version number.
5. [Set default Node.js version](#set-default-nodejs-version)

#### Fedora, RedHat, and other `dnf` based distros:

1. These distros come installed with curl, so you can use that to download nvm.
   `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash`
2. To confirm this has worked, use the following command. `nvm --version`. The output should be a version number.
3. [Set default Node.js version](#set-default-nodejs-version)

If the Linux distribution you are using is not listed here, please find instructions on the web.

#### Set default Node.js version

When nvm is installed, it does not default to a particular node version. You’ll need to install the version you want and give nvm instructions to use it. This example uses the latest release of version 10, but more recent version numbers can be used instead.

```shell
nvm install 10
nvm use 10
```

To confirm that this worked, you can run `npm --version` and `node --version`. The output should look similar to the screenshot below, showing version numbers in response to the commands.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

![Periksa versi node dan npm di terminal](01-node-npm-versions.png)

<<<<<<< HEAD
## Instal Git
=======
Once you have followed the installation steps and you have checked everything is installed properly, you can continue to the next step.

## Install Git
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

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
  <p>Sorry! Your browser doesn't support this video.</p>
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

- Perintah ini akan memulai *development server*. Anda akan dapat melihat dan berinteraksi dengan situs baru Anda di lingkungan pengembangan - lokal (di komputer Anda, tidak dipublikasikan ke internet).

### Lihat situs Anda secara lokal

<<<<<<< HEAD
Buka tab baru di browser Anda dan arahkan ke [**http://localhost:8000**](http://localhost:8000/).
=======
Open up a new tab in your browser and navigate to `http://localhost:8000/`
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

![Periksa beranda](04-home-page.png)

Selamat! Ini merupakan awal dari situs Gatsby pertama Anda! 🎉

<<<<<<< HEAD
Anda dapat mengunjungi situs secara lokal di [**_http://localhost:8000_**](http://localhost:8000/) selama *development server* Anda berjalan. Itulah proses yang Anda mulai dengan menjalankan perintah `gatsby develop`. Untuk berhenti menjalankan proses tersebut (atau untuk "berhenti menjalankan *development server*"), kembali ke jendela terminal Anda, tahan tombol "control", dan kemudian tekan "c" (ctrl-c). Untuk memulainya lagi, jalankan `gatsby develop` lagi!

**Catatan:** Jika Anda menggunakan pengaturan VM seperti `vagrant` dan atau ingin terhubung pada alamat IP lokal Anda, jalankan `gatsby develop -- --host=0.0.0.0`. Sekarang, *development server* terhubung ke 'localhost' dan IP lokal Anda.
=======
You’ll be able to visit the site locally at `http://localhost:8000/` for as long as your development server is running. That’s the process you started by running the `gatsby develop` command. To stop running that process (or to “stop running the development server”), go back to your terminal window, hold down the “control” key, and then hit “c” (ctrl-c). To start it again, run `gatsby develop` again!

**Note:** If you are using VM setup like `vagrant` and/or would like to listen on your local IP address, run `gatsby develop --host=0.0.0.0`. Now, the development server listens on both `http://localhost` and your local IP.
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

## Menyiapkan *code editor*

*Code editor* adalah program yang dirancang khusus untuk mengedit kode. Ada banyak *Code editor* yang bagus di luar sana.

### Unduh VS Code

Dokumentasi Gatsby terkadang menyertakan *screenshots* yang diambil dalam VS Code, jadi jika Anda belum memiliki *Code editor* pilihan, dengan menggunakan VS Code akan dipastikan bahwa layar Anda akan terlihat sama seperti *screenshots* dalam tutorial dan dokumen. Jika Anda memilih untuk menggunakan VS Code, kunjungi [Situs VS Code](https://code.visualstudio.com/#alt-downloads) dan unduh versi yang sesuai untuk *platform* Anda.

### Instal *plugin* Prettier

Kami juga merekomendasikan menggunakan [Prettier](https://github.com/prettier/prettier), sebuat alat yang membantu memformat kode Anda untuk menghindari kesalahan.

Anda dapat menggunakan Prettier secara langsung di *editor* Anda menggunakan [Prettier VS Code plugin](https://github.com/prettier/prettier-vscode):

<<<<<<< HEAD
1. Buka tampilan ekstensi pada VS Code (View => Extensions).
2. Cari "Prettier - Code formatter".
3. Klik "Install". (Setelah instalasi, Anda akan diminta untuk me-*restart* VS Code untuk mengaktifkan ekstensi. Untuk VS Code versi terbaru, VS Code akan secara otomatis mengaktifkan ekstensi setelah diunduh.)
=======
1.  Open the extensions view on VS Code (View => Extensions).
2.  Search for "Prettier - Code formatter".
3.  Click "Install". (After installation, you'll be prompted to restart VS Code to enable the extension. Newer versions of VS Code will automatically enable the extension after download.)
>>>>>>> 90932a06db2e297cf416552b84e48b4b82e56fbc

> 💡 Jika Anda tidak menggunakan VS Code, periksa dokumen Prettier untuk [instruksi instalasi](https://prettier.io/docs/en/install.html) atau [integrasi editor lainnya](https://prettier.io/docs/en/editors.html).

## ➡️ Apa berikutnya?

Sebagai rangkuman, pada bagian ini Anda:

- Mempelajari tentang *command line* dan cara menggunakannya
- Menginstal dan mempelajari tentang Node.js dan npm CLI, sistem pengelola perubahan Git, dan Gatsby CLI
- Menghasilkan situs Gatsby baru dengan menggunakan Gatsby CLI
- Menjalankan *development server* Gatsby dan mengunjungi situs Anda secara lokal
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

### Pelajari lebih lanjut tentang *command line*

Tutorial ini sangat bagus untuk Anda yang masih baru dalam menggunakan *command line*, lihat [**tutorial *Command Line* oleh Codecademy**](https://www.codecademy.com/courses/learn-the-command-line/lessons/navigation/exercises/your-first-command) untuk pengguna Mac dan Linux, dan [**tutorial ini**](https://www.computerhope.com/issues/chusedos.htm) untuk pengguna Windows. Meskipun Anda pengguna Windows, halaman pertama pada tutorial dari Codecademy sangat layak untuk Anda baca. Tutorial tersebut menjelaskan tentang apa itu *command line*, bukan hanya bagaimana berinteraksi dengannya.

### Pelajari lebih lanjut tentang npm

npm adalah pengelola paket JavaScript. Paket adalah sebuah modul kode yang dapat Anda pilih untuk dimasukkan ke dalam proyek Anda. Jika Anda baru saja mengunduh dan menginstal Node.js, npm sudah terinstal dengannya!

npm memiliki tiga komponen berbeda: situs web npm, registri npm, dan *command line interface* (CLI).

- Pada situs web npm, Anda dapat mencari paket JavaScript apa yang tersedia di registri npm.
- Registri npm adalah sebuah database informasi besar tentang paket-paket JavaScript yang tersedia di npm.
- Setelah Anda mengidentifikasi paket yang Anda inginkan, Anda dapat menggunakan npm CLI untuk menginstalnya di proyek Anda atau secara global (seperti CLI lainnya). CLI npm yang akan berinteraksi ke registri - Anda biasanya hanya akan berinteraksi dengan situs web npm atau CLI npm.

> 💡 Lihat pengenalan tentang npm, “[**Apa itu npm?**](https://docs.npmjs.com/getting-started/what-is-npm)”.

### Pelajari lebih lanjut tentang Git

Anda tidak perlu tahu Git untuk menyelesaikan tutorial ini, tetapi Git akan sangat berguna. Jika Anda tertarik untuk mempelajari lebih lanjut tentang pengelola perubahan, Git, dan GitHub, lihat [Pedoman GitHub](https://guides.github.com/introduction/git-handbook/) Github.

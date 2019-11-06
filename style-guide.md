# Panduan Penulisan

Gunakan file ini sebagai panduan penulisan dalam penerjemahan.

## Aturan

### Teks di dalam Kode

Jangan menerjemahkan teks yang ada di dalam kode kecuali teks untuk komentar. Kamu juga bisa menerjemakan teks yang tipenya adalah [string](https://id.wikipedia.org/wiki/String), tapi tetap harus hati - hati jangan menerjemahkan string yang merujuk pada kode!

Contoh:

```js
// Example
import React from "react"
export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
)
```

✅ BOLEH:

```js
// Contoh
import React from "react"
export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Hello Gatsby!</div>
)
```

✅ BOLEH JUGA:

```js
// Contoh
import React from "react"
export default () => (
  <div style={{ color: `purple`, fontSize: `72px` }}>Halo Gatsby!</div>
)
```

❌ JANGAN:

```js
// Contoh
import React from "react"
export default () => (
  // 'purple' adalah sebuag nama yang digunakan dalam CSS
  <div style={{ color: `ungu`, fontSize: `72px` }}>Halo Gatsby!</div>
)
```

❌ JANGAN PERNAH LAKUKAN:

```js
impor Aksi dari "aksi"
expor standar () => (
   <div style= {{color: `ungu`, fontSize:` 72px`}}> Halo Gatsby! </div>
)
```

### Tautan dari luar

Jika ada tautan dari luar yang berhubungan dengan referensi dalam artikel seperti pada [MDN] atau [Wikipedia], dan artikel tersebut berbahasa Indonesia yang kualitasnya terjamin, maka lebih baik menautkan pada kata tersebut.

[mdn]: https://developer.mozilla.org/en-US/
[wikipedia]: https://en.wikipedia.org/wiki/Main_Page

Contoh:

```md
React elements are [immutable](https://en.wikipedia.org/wiki/Immutable_object).
```

✅ OK:

```md
Elemen - elemen pada React adalah [inmutables](https://es.wikipedia.org/wiki/Objeto_inmutable).
```

Untuk tautan - tautan yang tidak mempunyai padankata (Stack Overflow, video - video YouTube, dan lainnya), maka gunakanlah tautan berbahasa Inggris.

## Glosarium

Gunakan bagian ini untuk mendaftar tentang bagaimana cara terminologi teknis seharusnya diterjemahkan.

| Istilah   | Terjemahan  |
| --------- | ----------- |
| Plugin    | ??          |
| Theme     | ??          |
| Query     | ??          |

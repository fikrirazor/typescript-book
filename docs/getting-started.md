* [Memulai dengan TypeScript](#memulai-dengan-typescript)
* [Versi TypeScript](#versi-typescript)

# Memulai dengan TypeScript

TypeScript mengkompilasi ke dalam JavaScript. Javascript adalah yang sering Anda jalankan didalam browser atau server. Untuk menjalankan TypeScript Anda membutuhkan :

* TypeScript compiler (OSS available [in source](https://github.com/Microsoft/TypeScript/) dan [NPM](https://www.npmjs.com/package/typescript))
* TypeScript editor (Anda dapat menggunakan notepad jika Anda mau tetapi Saya menggunakan[vscode 🌹](https://code.visualstudio.com/) dengan [extension yang Saya tulis](https://marketplace.visualstudio.com/items?itemName=basarat.god). Juga [Banyak IDE yang telah mensuport TypeScript]( https://github.com/Microsoft/TypeScript/wiki/TypeScript-Editor-Support))


## Versi TypeScript

Alih-alih menggunakan kompiler TypeScript yang stabil, kami akan menghadirkan banyak hal baru dalam buku ini yang mungkin belum dikaitkan dengan nomor versi. Saya biasanya merekomendasikan orang untuk menggunakan versi nightly karena **test suite kompiler hanya menangkap lebih banyak bug dari waktu ke waktu**.

Anda dapat menginstall TypeScript dengan perintah berikut:

```
npm install -g typescript@next
```

Dan sekarang perintah `tsc` akan menjadi sering dipakai. Beberapa dari banyak IDE telah mensupport perintah tersebut.

* Anda dapat meminta vscode untuk menggunakan versi ini dengan membuat  `.vscode/settings.json` dengan konten berikut:

```json
{
  "typescript.tsdk": "./node_modules/typescript/lib"
}
```

## Mendapatkan Kode Sumber
Sumber untuk buku ini tersedia di repositori github https://github.com/basarat/typescript-book/tree/master/code banyak contoh kode yang Anda dapat salin ke vscode dan Anda dapat bermain dengan mereka. Untuk contoh kode yang membutuhkan pengaturan tambahan (mis. npm modules), kami akan menautkan Anda ke sampel kode sebelum menyajikan kode. misalnya

`this/will/be/the/link/to/the/code.ts`
```ts
// This will be the code under discussion
```

Dengan pengaturan pengembangan, mari kita beralih ke sintaks TypeScript.

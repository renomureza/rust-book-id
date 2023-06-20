## Komentar

Semua pemrogram berusaha keras untuk membuat kode mereka mudah dipahami, tetapi terkadang diperlukan penjelasan tambahan. Dalam kasus ini, pemrogram meninggalkan _komentar_ dalam kode sumber mereka yang akan diabaikan oleh kompiler tetapi orang yang membaca kode sumber mungkin berguna.

Berikut komentar sederhana:

```rust
// hello, world
```

Di Rust, gaya komentar idiomatis memulai komentar dengan dua garis miring, dan komentar berlanjut hingga akhir baris. Untuk komentar yang membutuhkan lebih dari satu baris, Anda harus menyertakannya `//` di setiap baris, seperti ini:

```rust
// So we’re doing something complicated here, long enough that we need
// multiple lines of comments to do it! Whew! Hopefully, this comment will
// explain what’s going on.
```

Komentar juga dapat ditempatkan di akhir baris yang berisi kode:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-24-comments-end-of-line/src/main.rs}}
```

Namun Anda akan lebih sering melihatnya digunakan dalam format ini, dengan komentar pada baris terpisah di atas kode yang diberi anotasi:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-25-comments-above-line/src/main.rs}}
```

Rust juga memiliki jenis komentar lain, komentar dokumentasi, yang akan kita diskusikan di bagian [“Menerbitkan Crate ke Crates.io”][publishing] di Bab 14.

[publishing]: ch14-02-publishing-to-crates-io.html

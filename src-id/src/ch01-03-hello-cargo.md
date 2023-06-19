## Hello, Cargo!

Cargo adalah _build system_ dan _package manager_ Rust. Sebagian besar Rustacean menggunakan alat ini untuk mengelola proyek Rust mereka karena Cargo menangani banyak tugas untuk Anda, seperti membangun kode, mengunduh _library_ dimana kode Anda bergantung padanya, dan membangun _library_ tersebut. (Kami memanggil _library_ yang yang diperlukan dependensi kode Anda.)

Program Rust yang paling sederhana, seperti yang telah kami tulis sejauh ini, tidak memiliki ketergantungan apa pun. Jika kita telah membangun proyek "Hello, world!" dengan Cargo, itu hanya akan menggunakan bagian dari Cargo yang menangani pembuatan kode Anda. Saat Anda menulis program Rust yang lebih kompleks, Anda akan menambahkan dependensi, dan jika Anda memulai proyek menggunakan Cargo, menambahkan dependensi akan lebih mudah dilakukan.

Karena sebagian besar proyek Rust menggunakan Cargo, sisa buku ini mengasumsikan bahwa Anda juga menggunakan Cargo. Cargo dilengkapi dengan Rust jika Anda menggunakan penginstal resmi yang dibahas di bagian [“Instalasi”][installation]. Jika Anda menginstal Rust melalui cara lain, periksa apakah Cargo diinstal dengan memasukkan perintah berikut di terminal Anda:

```console
$ cargo --version
```

Jika Anda melihat nomor versi, Anda memilikinya! Jika Anda melihat kesalahan, seperti `command not found`, lihat dokumentasi metode pemasangan Anda untuk menentukan cara memasang Cargo secara terpisah.

### Membuat Proyek dengan Kargo

Mari buat proyek baru menggunakan Cargo dan lihat perbedaannya dari proyek "Hello, world!". Arahkan kembali ke direktori _projects_ Anda (atau di mana pun Anda memutuskan untuk menyimpan kode Anda). Kemudian, pada sistem operasi apa pun, jalankan perintah berikut:

```console
$ cargo new hello_cargo
$ cd hello_cargo
```

Perintah pertama membuat direktori dan proyek baru bernama _hello_cargo_. Kami menamai proyek kami _hello_cargo_, dan Cargo membuat file-filenya di direktori dengan nama yang sama.

Masuk ke direktori _hello_cargo_ dan lihat file-filenya. Anda akan melihat bahwa Cargo telah menghasilkan dua file dan satu direktori untuk kita: file _Cargo.toml_ dan direktori _src_ dengan file _main.rs_ di dalamnya.

Itu juga menginisialisasi repositori Git baru bersama dengan file _.gitignore_. File Git tidak akan dibuat jika Anda menjalankannya `cargo new` di dalam repositori yang sudah memiliki Git; Anda dapat mengganti perilaku ini dengan menggunakan `cargo new --vcs=git`.

> Catatan: Git adalah sistem kontrol versi yang umum. Anda dapat mengubah `cargo new` untuk menggunakan sistem kontrol versi yang berbeda atau tanpa sistem kontrol versi dengan menggunakan bendera `--vcs`. Jalankan `cargo new --help` untuk melihat opsi yang tersedia.

Buka _Cargo.toml_ di editor teks pilihan Anda. Seharusnya terlihat mirip dengan kode di Daftar 1-2.

<span class="filename">Nama file: Cargo.toml</span>

```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

<span class="caption">Daftar 1-2: Konten _Cargo.toml_ yang dihasilkan `cargo
new`</span>

File ini dalam format [_TOML_][toml]<!-- ignore --> (_Tom's Obvious, Minimal Language_), yang merupakan format konfigurasi Cargo.

Baris pertama, `[package]`, adalah judul bagian yang menunjukkan bahwa pernyataan berikut sedang mengonfigurasi sebuah paket. Saat kami menambahkan lebih banyak informasi ke file ini, kami akan menambahkan bagian lain.

Tiga baris berikutnya menetapkan informasi konfigurasi yang diperlukan Cargo untuk mengompilasi program Anda: nama, versi, dan edisi Rust yang akan digunakan. Kami akan berbicara tentang `edition` di [Lampiran E][appendix-e].

Baris terakhir, `[dependencies]`, adalah awal dari bagian untuk Anda membuat daftar dependensi proyek Anda. Di Rust, paket kode disebut sebagai _crates_. Kita tidak memerlukan crates lain untuk proyek ini, tetapi kita akan membutuhkannya di proyek pertama di Bab 2, jadi kita akan menggunakan bagian dependensi ini nanti.

Sekarang buka _src/main.rs_ dan lihat:

<span class="filename">Nama file: src/main.rs</span>

```rust
fn main() {
    println!("Hello, world!");
}
```

Cargo telah menghasilkan program "Hello, world!" untuk Anda, seperti yang kami tulis di Daftar 1-1! Sejauh ini, perbedaan antara proyek kami dan proyek yang dihasilkan Cargo adalah Cargo menempatkan kode di direktori _src_ dan kami memiliki file konfigurasi _Cargo.toml_ di direktori teratas.

Cargo mengharapkan file sumber Anda berada di dalam direktori _src_. Direktori proyek tingkat atas hanya untuk file README, informasi lisensi, file konfigurasi, dan hal lain yang tidak terkait dengan kode Anda. Menggunakan Cargo membantu Anda mengatur proyek Anda. Ada tempat untuk segalanya, dan semuanya ada di tempatnya.

Jika Anda memulai proyek yang tidak menggunakan Cargo, seperti yang kami lakukan dengan proyek "Hello, world!", Anda dapat mengonversinya menjadi proyek yang menggunakan Cargo. Pindahkan kode proyek ke direktori _src_ dan buat file _Cargo.toml_ yang sesuai .

### Membangun dan Menjalankan Proyek Cargo

Sekarang mari kita lihat apa yang berbeda saat kita membangun dan menjalankan program "Hello, world!" dengan Cargo! Dari direktori _hello_cargo_ Anda, bangun proyek Anda dengan memasukkan perintah berikut:

```console
$ cargo build
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```

Perintah ini membuat file yang dapat dieksekusi di _target/debug/hello_cargo_ (atau _target\debug\hello_cargo.exe_ untuk Windows) alih-alih di direktori Anda saat ini. Karena build default adalah build debug, Cargo menempatkan biner di direktori bernama debug. Anda dapat menjalankan file _executable_ dengan perintah ini:

```console
$ ./target/debug/hello_cargo # atau .\target\debug\hello_cargo.exe untuk Windows
Hello, world!
```

Jika semuanya berjalan dengan baik, `Hello, world!` harus dicetak ke terminal. Menjalankan `cargo build` untuk pertama kali juga menyebabkan Cargo membuat file baru di tingkat teratas: _Cargo.lock_. File ini melacak versi dependensi yang tepat dalam proyek Anda. Proyek ini tidak memiliki dependensi, jadi filenya agak jarang. Anda tidak perlu mengubah file ini secara manual; Cargo mengelola isinya untuk Anda.

Kami baru saja membangun sebuah proyek dengan `cargo build` dan menjalankannya dengan `./target/debug/hello_cargo`, tetapi kami juga dapat menggunakan `cargo run` untuk mengkompilasi kode dan kemudian menjalankan file yang dapat dieksekusi dalam satu perintah:

```console
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/hello_cargo`
Hello, world!
```

Menggunakan `cargo run` lebih nyaman daripada harus mengingat untuk menjalankan `cargo build` dan kemudian menggunakan seluruh jalur ke biner, oleh karena itu sebagian besar pengembang menggunakan `cargo run`.

Perhatikan bahwa kali ini kami tidak melihat _output_ yang menunjukkan bahwa Cargo sedang mengkompilasi _hello_cargo_. Cargo mengetahui bahwa file-file tersebut tidak berubah, sehingga tidak dibangun kembali tetapi hanya menjalankan biner. Jika Anda telah memodifikasi kode sumber Anda, Cargo akan membuat ulang proyek sebelum menjalankannya, dan Anda akan melihat _output_ ini:

```console
$ cargo run
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.33 secs
     Running `target/debug/hello_cargo`
Hello, world!
```

Cargo juga menyediakan perintah yang disebut `cargo check`. Perintah ini memeriksa kode Anda dengan cepat untuk memastikan kompilasi tetapi tidak menghasilkan file yang dapat dieksekusi:

```console
$ cargo check
   Checking hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.32 secs
```

Mengapa Anda tidak menginginkan file yang dapat dieksekusi? Seringkali, `cargo check` jauh lebih cepat daripada `cargo build` karena melewatkan langkah yang menghasilkan _executable_. Jika Anda terus-menerus memeriksa pekerjaan Anda saat menulis kode, penggunaan `cargo check` akan mempercepat proses memberi tahu Anda jika proyek Anda masih dikompilasi! Dengan demikian, banyak Rustacean menjalankan `cargo check` secara berkala saat mereka menulis program mereka untuk memastikan bahwa itu dapat dikompilasi. Kemudian mereka menjalankan `cargo build` ketika mereka siap menjalankan file yang dapat dieksekusi.

Mari rekap apa yang telah kita pelajari sejauh ini tentang Cargo:

- Kita dapat membuat proyek menggunakan `cargo new`.
- Kita dapat membangun proyek menggunakan `cargo build`.
- Kita dapat membangun dan menjalankan proyek dalam satu langkah menggunakan `cargo run`.
- Kita dapat membangun proyek tanpa menghasilkan biner untuk memeriksa kesalahan menggunakan
  `cargo check`.
- Alih-alih menyimpan hasil build di direktori yang sama dengan kode kita, Cargo menyimpannya di direktori _target/debug_.

Keuntungan tambahan menggunakan Cargo adalah bahwa perintahnya sama, apa pun sistem operasi yang Anda gunakan. Jadi, saat ini, kami tidak akan lagi memberikan petunjuk khusus untuk Linux dan macOS versus Windows.

### Membangun untuk Rilis

Ketika proyek Anda akhirnya siap untuk dirilis, Anda dapat menggunakannya `cargo build --release` untuk mengompilasi dengan pengoptimalan. Perintah ini akan membuat executable di _target/release_ bukan _target/debug_. Pengoptimalan membuat kode Rust Anda berjalan lebih cepat, tetapi mengaktifkannya akan memperpanjang waktu yang diperlukan untuk mengompilasi program Anda. Inilah mengapa ada dua profil yang berbeda: satu untuk pengembangan, ketika Anda ingin membangun kembali dengan cepat dan sering, dan satu lagi untuk membangun program final yang akan Anda berikan kepada pengguna yang tidak akan dibangun kembali berulang kali dan akan berjalan secepat mungkin. Jika Anda membandingkan waktu berjalan kode Anda, pastikan untuk menjalankan `cargo build --release` dan melakukan _benchmark_ dengan executable di _target/release_.

### Cargo sebagai Konvensi

Dengan proyek-proyek sederhana, Cargo tidak memberikan banyak nilai daripada menggunakan `rustc`, tetapi akan membuktikan nilainya saat program Anda menjadi lebih rumit. Setelah program berkembang menjadi banyak file atau memerlukan ketergantungan, akan lebih mudah untuk membiarkan Cargo mengoordinasikan pembangunan.

Meskipun proyeknya `hello_cargo` sederhana, proyek ini sekarang menggunakan banyak perkakas asli yang akan Anda gunakan di sisa karier Rust Anda. Bahkan, untuk bekerja pada proyek yang sudah ada, Anda dapat menggunakan perintah berikut untuk memeriksa kode menggunakan Git, mengubah ke direktori proyek tersebut, dan membangun:

```console
$ git clone example.org/someproject
$ cd someproject
$ cargo build
```

Untuk informasi lebih lanjut tentang Cargo, [lihat dokumentasinya][cargo].

## Ringkasan

Anda sudah memulai awal yang baik dalam perjalanan Rust Anda! Dalam bab ini, Anda telah mempelajari cara:

- Menginstal Rust versi stabil terbaru menggunakan `rustup`
- Memperbarui Rust ke versi yang lebih baru
- Buka dokumentasi yang diinstal secara lokal
- Tulis dan jalankan "Hello, world!" menggunakan program `rustc` secara langsung
- Buat dan jalankan proyek baru menggunakan konvensi Cargo

Ini adalah waktu yang tepat untuk membuat program yang lebih substansial agar terbiasa membaca dan menulis kode Rust. Jadi, di Bab 2, kita akan membuat program permainan tebak-tebakan. Jika Anda lebih suka memulai dengan mempelajari cara kerja konsep pemrograman umum di Rust, lihat Bab 3 lalu kembali ke Bab 2.

[installation]: ch01-01-installation.html#installation
[toml]: https://toml.io
[appendix-e]: appendix-05-editions.html
[cargo]: https://doc.rust-lang.org/cargo/

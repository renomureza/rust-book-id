# Bahasa Pemrograman Rust

[Bahasa Pemrograman Rust](title-page.md)
[Kata Pengantar](foreword.md)
[Perkenalan](ch00-00-introduction.md)

## Memulai

- [Memulai](ch01-00-getting-started.md)

  - [Instalasi](ch01-01-installation.md)
  - [Hello, World!](ch01-02-hello-world.md)
  - [Hello, Cargo!](ch01-03-hello-cargo.md)

- [Pemrograman Game Menebak](ch02-00-guessing-game-tutorial.md)

- [Konsep Pemrograman Umum](ch03-00-common-programming-concepts.md)

  - [Variabel dan Mutabilitas](ch03-01-variables-and-mutability.md)
  - [Tipe Data](ch03-02-data-types.md)
  - [Funsi](ch03-03-how-functions-work.md)
  - [Komentar](ch03-04-comments.md)
  - [Aliran Kontrol](ch03-05-control-flow.md)

- [Memahami Ownership](ch04-00-understanding-ownership.md)

  - [Apa itu Ownership?](ch04-01-what-is-ownership.md)
  - [Reference dan Borrowing](ch04-02-references-and-borrowing.md)
  - [Tipe Slice](ch04-03-slices.md)

- [Menggunakan Struct untuk Menyusun Data Terkait](ch05-00-structs.md)

  - [Mendefinisikan dan Instansiasi Struct](ch05-01-defining-structs.md)
  - [Contoh Program Menggunakan Struct](ch05-02-example-structs.md)
  - [Sintaks Method](ch05-03-method-syntax.md)

- [Enum dan Pencocokan Pola](ch06-00-enums.md)
  - [Mendefinisikan Enum](ch06-01-defining-an-enum.md)
  - [Konstruk Aliran Kontrol `match`](ch06-02-match.md)
  - [Aliran Kontrol Ringkas dengan `if let`](ch06-03-if-let.md)

## Literasi Dasar Rust

- [Mengelola Proyek yang Berkembang dengan Packages, Crates, dan Modul](ch07-00-managing-growing-projects-with-packages-crates-and-modules.md)

  - [Packages dan Crates](ch07-01-packages-and-crates.md)
  - [Mendefinisikan Modul untuk Menongtrol Ruang Lingkup dan Privasi](ch07-02-defining-modules-to-control-scope-and-privacy.md)
  - [Jalur untuk Merujuk ke Item di Pohon Modul](ch07-03-paths-for-referring-to-an-item-in-the-module-tree.md)
  - [Membawa Jalur ke Cakupan dengan Kata Kunci `use`](ch07-04-bringing-paths-into-scope-with-the-use-keyword.md)
  - [Memisahkan Modul menjadi File yang Berbeda](ch07-05-separating-modules-into-different-files.md)

- [Koleksi Umum](ch08-00-common-collections.md)

  - [Menyimpan Daftar Nilai dengan Vector](ch08-01-vectors.md)
  - [Menyimpan Teks UTF-8 Encoded dengan String](ch08-02-strings.md)
  - [Menyimpan Kunci dengan Nilai Terkait di Hash Map](ch08-03-hash-maps.md)

- [Penanganan Kesalahan](ch09-00-error-handling.md)

  - [Kesalahan yang Tidak Dapat Dipulihkan dengan `panic!`](ch09-01-unrecoverable-errors-with-panic.md)
  - [Kesalahan yang Dapat Dipulihkan dengan `Result`](ch09-02-recoverable-errors-with-result.md)
  - [`panic!` atau jangan `panic!`](ch09-03-to-panic-or-not-to-panic.md)

- [Tipe Generik, Trait, dan Lifetime](ch10-00-generics.md)

  - [Tipe Data Generik](ch10-01-syntax.md)
  - [Trait: Mendefinisikan Perilaku Bersama](ch10-02-traits.md)
  - [Memvalidasi Reference dengan Lifetime](ch10-03-lifetime-syntax.md)

- [Menulis Tes Otomatis](ch11-00-testing.md)

  - [Cara Menulis Tes](ch11-01-writing-tests.md)
  - [Mengontrol Bagaiaman Tes Dijalankan](ch11-02-running-tests.md)
  - [Organisasi Tes](ch11-03-test-organization.md)

- [Projek I/O: Membangun Program Baris Perintah](ch12-00-an-io-project.md)
  - [Menerima Argumen Baris Perintah](ch12-01-accepting-command-line-arguments.md)
  - [Membaca File](ch12-02-reading-a-file.md)
  - [Refactoring untuk Meningkatkan Modularitas dan Penanganan Kesalahan](ch12-03-improving-error-handling-and-modularity.md)
  - [Mengembangkan Fungsionalitas Library dengan Test Driven Development](ch12-04-testing-the-librarys-functionality.md)
  - [Bekerja dengan Environment Variable](ch12-05-working-with-environment-variables.md)
  - [Menulis Pesan Kesalahan ke Standard Error Alih-alih Standard Output](ch12-06-writing-to-stderr-instead-of-stdout.md)

## Berpikir di Rust

- [Fitur Bahasa Fungsional: Iterator dan Closure](ch13-00-functional-features.md)

  - [Closure: Fungsi Anonim yang Menangkap Lingkungannya](ch13-01-closures.md)
  - [Memproses Serangkaian Item dengan Iterator](ch13-02-iterators.md)
  - [Meningkatkan Proyek I/O Kami](ch13-03-improving-our-io-project.md)
  - [Membandingkan Performa: Loop vs Iterator](ch13-04-performance.md)

- [Lebih Lanjut Tentang Cargo dan Crates.io](ch14-00-more-about-cargo.md)

  - [Menyesuaikan Build dengan Profil Rilis](ch14-01-release-profiles.md)
  - [Menerbitkan Crate ke Crates.io](ch14-02-publishing-to-crates-io.md)
  - [Ruang Kerja Cargo](ch14-03-cargo-workspaces.md)
  - [Menginstal Binari dari Crates.io dengan `cargo install`](ch14-04-installing-binaries.md)
  - [Memperpanjang Cargo dengan Perintah Khusus](ch14-05-extending-cargo.md)

- [Smart Pointer](ch15-00-smart-pointers.md)

  - [Menggunakan `Box<T>` untuk Menunjuk ke Data di Heap](ch15-01-box.md)
  - [Memperlakukan Smart Pointer Seperti Reference Biasa dengan Trait `Deref`](ch15-02-deref.md)
  - [Menjalankan Kode pada Pembersihan dengan Trait `Drop`](ch15-03-drop.md)
  - [`Rc<T>`, Smart Pointer Reference Terhitung](ch15-04-rc.md)
  - [`RefCell<T>` dan Pola Mutabilitas Interior](ch15-05-interior-mutability.md)
  - [Siklus Reference Dapat Membocorkan Memori](ch15-06-reference-cycles.md)

- [Konkurensi Tanpa Takut](ch16-00-concurrency.md)

  - [Menggunakan Thread untuk Menjalankan Kode secara Bersamaan](ch16-01-threads.md)
  - [Menggunakan Message Passing untuk Mentransfer Data Antar Thread](ch16-02-message-passing.md)
  - [Konkurensi Shared-State](ch16-03-shared-state.md)
  - [Konkurensi yang Dapat Diperluas dengan Trait `Sync` dan `Send`](ch16-04-extensible-concurrency-sync-and-send.md)

- [Fitur Pemrograman Berorientasi Objek dari Rust](ch17-00-oop.md)
  - [Karakteristik Bahasa Berorientasi Objek](ch17-01-what-is-oo.md)
  - [Menggunakan Objek Trait yang Memungkinkan Nilai dari Berbagai Tipe](ch17-02-trait-objects.md)
  - [Menerapkan Pola Desain Berorientasi Objek](ch17-03-oo-design-patterns.md)

## Topik Lanjutan

- [Pola dan Pencocokan](ch18-00-patterns.md)

  - [Semua Tempat Pola Dapat Digunakan](ch18-01-all-the-places-for-patterns.md)
  - [Sanggahan: Apakah suatu Pola Mungkin Gagal Mencocokkan](ch18-02-refutability.md)
  - [Sintaks Pola](ch18-03-pattern-syntax.md)

- [Fitur Lanjutan](ch19-00-advanced-features.md)

  - [Unsafe Rust](ch19-01-unsafe-rust.md)
  - [Trait Lanjutan](ch19-03-advanced-traits.md)
  - [Tipe Lanjutan](ch19-04-advanced-types.md)
  - [Fungsi Lanjutan dan Closure](ch19-05-advanced-functions-and-closures.md)
  - [Makro](ch19-06-macros.md)

- [Tugas Akhir: Membangun Server Web Multithreaded](ch20-00-final-project-a-web-server.md)

  - [Membangun Server Web Single-Threaded](ch20-01-single-threaded.md)
  - [Mengubah Server Single-Threaded ke Server Multithreaded](ch20-02-multithreaded.md)
  - [Shutdown dan Pembersihan Anggun](ch20-03-graceful-shutdown-and-cleanup.md)

- [Lampiran](appendix-00.md)
  - [A - Kata Kunci](appendix-01-keywords.md)
  - [B - Operator dan Simbol](appendix-02-operators.md)
  - [C - Derivable Trait](appendix-03-derivable-traits.md)
  - [D - Alat Pengembangan yang Berguna](appendix-04-useful-development-tools.md)
  - [E - Edisi](appendix-05-editions.md)
  - [F - Terjemahan Buku](appendix-06-translation.md)
  - [G - Bagaimana Rust Dibuat dan “Nightly Rust”](appendix-07-nightly-rust.md)

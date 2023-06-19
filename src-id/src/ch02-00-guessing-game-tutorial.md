# Memprogram Game Tebak-tebakan

Mari lompat ke Rust dengan mengerjakan proyek langsung bersama! Bab ini memperkenalkan Anda pada beberapa konsep umum Rust dengan menunjukkan cara menggunakannya dalam program nyata. Anda akan belajar tentang `let`, `match`, _method_, fungsi terkait, crates eksternal, dan banyak lagi! Dalam bab-bab berikut, kita akan mengeksplorasi ide-ide ini secara lebih mendetail. Dalam bab ini, Anda hanya akan mempraktikkan dasar-dasarnya.

Kami akan menerapkan masalah pemrograman pemula klasik: permainan tebak-tebakan. Begini cara kerjanya: program akan menghasilkan bilangan bulat acak antara 1 dan 100. Kemudian program akan meminta pemain untuk memasukkan tebakan. Setelah tebakan dimasukkan, program akan menunjukkan apakah tebakannya terlalu rendah atau terlalu tinggi. Jika tebakannya benar, game akan mencetak pesan ucapan selamat dan keluar.

## Menyiapkan Proyek Baru

Untuk menyiapkan proyek baru, buka direktori _projects_ yang Anda buat di Bab 1 dan buat proyek baru menggunakan Cargo, seperti:

```console
$ cargo new guessing_game
$ cd guessing_game
```

Perintah pertama, `cargo new`, mengambil nama proyek (`guessing_game`) sebagai argumen pertama. Perintah kedua mengubah direktori ke direktori proyek baru.

Lihat file _Cargo.toml_ yang dihasilkan :

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial
rm -rf no-listing-01-cargo-new
cargo new no-listing-01-cargo-new --name guessing_game
cd no-listing-01-cargo-new
cargo run > output.txt 2>&1
cd ../../..
-->

<span class="filename">Nama file: Cargo.toml</span>

```toml
{{#include ../../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/Cargo.toml}}
```

Seperti yang Anda lihat di Bab 1, `cargo new` menghasilkan "Hello, world!" program untuk Anda. Lihat file _src/main.rs_:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/src/main.rs}}
```

Sekarang mari kita kompilasi program “Hello, world!” dan jalankan dengan langkah yang sama menggunakan perintah `cargo run`:

```console
{{#include ../../listings/ch02-guessing-game-tutorial/no-listing-01-cargo-new/output.txt}}
```

Perintah `run` berguna saat Anda perlu melakukan iterasi dengan cepat pada sebuah proyek, seperti yang akan kita lakukan di game ini, dengan cepat menguji setiap iterasi sebelum melanjutkan ke iterasi berikutnya.

Buka kembali file _src/main.rs_. Anda akan menulis semua kode di file ini.

## Memproses Tebakan

Bagian pertama dari program permainan tebak-tebakan akan menanyakan masukan pengguna, memproses masukan tersebut, dan memeriksa apakah masukan tersebut dalam bentuk yang diharapkan. Untuk memulai, kami akan mengizinkan pemain untuk memasukkan tebakan. Masukkan kode pada Daftar 2-1 ke dalam _src/main.rs_.

The first part of the guessing game program will ask for user input, process
that input, and check that the input is in the expected form. To start, we’ll
allow the player to input a guess. Enter the code in Listing 2-1 into
_src/main.rs_.

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:all}}
```

<span class="caption">Daftar 2-1: Kode untuk mendapat tebakan dari pengguna dan mencetaknya</span>

Kode ini berisi banyak informasi, jadi mari kita bahas baris demi baris. Untuk mendapatkan input pengguna dan kemudian mencetak hasilnya sebagai output, kita perlu memasukkan library `io` input/output ke dalam scope. Library `io` berasal dari _standard library_, yang dikenal sebagai `std`:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:io}}
```

Secara default, Rust memiliki sekumpulan item yang ditentukan di _standard library_ yang dibawanya ke dalam cakupan setiap program. Set ini disebut _prelude_, dan Anda dapat melihat semua yang ada di dalamnya [dalam dokumentasi _standard library_][prelude].

Jika jenis yang ingin Anda gunakan tidak ada di prelude, Anda harus memasukkan jenis itu ke dalam ruang lingkup secara eksplisit dengan pernyataan `use`. Menggunakan `std::io` perpustakaan memberi Anda sejumlah fitur berguna, termasuk kemampuan untuk menerima input pengguna.

Seperti yang Anda lihat di Bab 1, fungsi `main` adalah titik masuk ke dalam program:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:main}}
```

Sintaks `fn` mendeklarasikan fungsi baru; tanda kurung, `()`, menunjukkan tidak ada parameter; dan kurung kurawal, `{`, memulai badan fungsi.

Seperti yang juga Anda pelajari di Bab 1, `println!` adalah makro yang mencetak string ke layar:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:print}}
```

Kode ini mencetak prompt yang menyatakan apa game itu dan meminta masukan dari pengguna.

### Menyimpan Nilai dengan Variabel

Selanjutnya, kita akan membuat variabel untuk menyimpan input pengguna, seperti ini:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:string}}
```

Sekarang programnya semakin menarik! Ada banyak hal yang terjadi di garis kecil ini. Kami menggunakan pernyataan `let` untuk membuat variabel. Ini contoh lainnya:

```rust,ignore
let apples = 5;
```

Baris ini membuat variabel baru bernama `apples` dan mengikatnya ke nilai 5. Di Rust, variabel tidak dapat diubah secara default, artinya setelah kita memberi nilai pada variabel, nilainya tidak akan berubah. Kita akan membahas konsep ini secara detail di bagian [“Variabel dan Mutabilitas”][variables-and-mutability] di Bab 3. Untuk membuat variabel bisa berubah, kita tambahkan `mut` sebelum nama variabel:

```rust,ignore
let apples = 5; // immutable (tidak dapat diubah)
let mut bananas = 5; // mutable (dapat diubah)
```

> Catatan: Sintaks `//` memulai komentar yang berlanjut hingga akhir baris. Rust mengabaikan semuanya dalam komentar. Kita akan membahas komentar lebih detail di [Bab 3][comments].

Kembali ke program permainan tebak-tebakan, sekarang Anda tahu bahwa `let mut guess` akan memperkenalkan variabel yang dapat berubah bernama `guess`. Tanda sama dengan (`=`) memberi tahu Rust bahwa kita ingin mengikat sesuatu ke variabel sekarang. Di sebelah kanan tanda sama dengan adalah nilai yang diikat ke `guess`, yang merupakan hasil dari pemanggilan `String::new`, sebuah fungsi yang mengembalikan instance baru dari sebuah `String`. [`String`][string] adalah tipe string yang disediakan oleh _standard library_ yang berupa bit teks berkode UTF-8 yang dapat berkembang.

Sintaks `::` di baris `::new` menunjukkan bahwa `new` itu adalah fungsi terkait (_associated
function_) dari tipe `String`. Fungsi terkait adalah fungsi yang diimplementasikan pada sebuah tipe, dalam hal ini `String`. Fungsi `new` ini membuat string baru yang kosong. Anda akan menemukan fungsi `new` pada banyak tipe karena itu adalah nama umum untuk fungsi yang membuat semacam nilai baru.

Secara penuh, baris `let mut guess = String::new();` telah membuat variabel yang dapat diubah yang saat ini terikat ke _instance_ baru yang kosong dari `String`. Wah!

### Menerima Masukan Pengguna

Ingatlah bahwa kami menyertakan fungsi input/output dari _standard library_ `use std::io;` pada baris pertama program. Sekarang kita akan memanggil fungsi `stdin` dari modul `io`, yang memungkinkan kita untuk menangani input pengguna:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:read}}
```

Jika kita tidak mengimpor pustaka `io`, `use std::io;` di awal program, kita masih bisa menggunakan fungsi dengan menulis pemanggilan fungsi ini sebagai `std::io::stdin`. Fungsi `stdin` mengembalikan instance dari [`std::io::Stdin`][iostdin], yang merupakan tipe yang mewakili pegangan ke _standard input_ untuk terminal Anda.

Selanjutnya, baris `.read_line(&mut guess)` memanggil method [`read_line`][read_line] pada pegangan input standar untuk mendapatkan input dari pengguna. Kami juga memberikan argumen `&mut guess` untuk memberi tahu `read_line` string apa untuk menyimpan input pengguna. Tugas `read_line` adalah mengambil apa pun yang diketik pengguna ke dalam input standar dan menambahkannya ke dalam string (tanpa menimpa isinya), jadi oleh karena itu kami berikan string itu sebagai argumen. Argumen string harus dapat diubah agar method dapat mengubah konten string.

`&` menunjukkan bahwa argumen ini adalah referensi, yang memberi Anda cara untuk membiarkan beberapa bagian kode Anda mengakses satu bagian data tanpa perlu menyalin data tersebut ke dalam memori beberapa kali. Referensi adalah fitur yang kompleks, dan salah satu keunggulan utama Rust adalah betapa aman dan mudahnya menggunakan referensi. Anda tidak perlu mengetahui banyak detail tersebut untuk menyelesaikan program ini. Untuk saat ini, yang perlu Anda ketahui adalah, seperti variabel, referensi tidak dapat diubah secara default. Karenanya, Anda perlu menulis `&mut guess` alih-alih `&guess` sehingga membuatnya bisa berubah. (Bab 4 akan menjelaskan referensi lebih menyeluruh.)

<!-- Old heading. Do not remove or links may break. -->

<a id="handling-potential-failure-with-the-result-type"></a>

### Menangani Potensi Kegagalan dengan `Result`

Kami masih mengerjakan baris kode ini. Kita sekarang membahas baris teks ketiga, tetapi perhatikan bahwa itu masih merupakan bagian dari satu baris kode logis. Bagian selanjutnya adalah method ini:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:expect}}
```

Kita bisa menulis kode ini sebagai:

```rust,ignore
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

Namun, satu baris panjang sulit dibaca, jadi sebaiknya dipisahkan. Seringkali bijaksana untuk memperkenalkan baris baru dan spasi putih lainnya untuk membantu memecah garis panjang saat Anda memanggil method dengan sintaks.`method_name()`. Sekarang mari kita bahas apa yang dilakukan baris ini.

Seperti disebutkan sebelumnya, `read_line` menempatkan apa pun yang dimasukkan pengguna ke dalam string yang kita berikan padanya, tetapi juga mengembalikan nilai `Result`. [`Result`][result] adalah [_enumeration_][enums], sering disebut _enum_, yang merupakan tipe yang dapat berada di salah satu dari beberapa status yang mungkin. Kami menyebut setiap status yang mungkin sebagai varian.

[Chapter 6][enums] akan membahas enum lebih detail. Tujuan dari tipe `Result` ini adalah untuk menyandikan informasi penanganan kesalahan.

Varian `Result` adalah `Ok` dan `Err`. Varian `Ok` menunjukkan operasi berhasil, dan di dalam `Ok` adalah nilai yang berhasil dihasilkan. Varian `Err` berarti operasi gagal, dan `Err` berisi informasi tentang bagaimana atau mengapa operasi gagal.

Nilai tipe `Result`, seperti nilai tipe lain, memiliki metode yang telah ditentukan di dalamnya. Contoh dari `Result` memiliki [metode `expect`][expect] yang dapat Anda panggil. Jika turunan dari `Result` ini adalah sebuah nilai `Err`, `expect` akan menyebabkan program macet dan menampilkan pesan sesuai dengan pesan yang Anda berikan sebagai argumen untuk `expect`. Jika metode `read_line` mengembalikan `Err`, kemungkinan itu adalah hasil dari kesalahan yang berasal dari sistem operasi yang mendasarinya. Jika dalam contoh ini `Result` adalah sebuah nilai `Ok`, `expect` akan mengambil nilai kembalian yang ditahan `Ok` dan mengembalikan nilai itu kepada Anda sehingga Anda dapat menggunakannya. Dalam hal ini, nilai tersebut adalah jumlah byte dalam masukan pengguna.

Jika Anda tidak memanggil `expect`, program akan dikompilasi, tetapi Anda akan mendapat peringatan:

```console
{{#include ../../listings/ch02-guessing-game-tutorial/no-listing-02-without-expect/output.txt}}
```

Rust memperingatkan bahwa Anda belum menggunakan nilai `Result` yang dikembalikan dari `read_line`, yang menunjukkan bahwa program belum menangani kemungkinan kesalahan.

Cara yang tepat untuk menekan peringatan adalah dengan benar-benar menulis kode penanganan kesalahan, tetapi dalam kasus kami, kami hanya ingin menghentikan program ini saat terjadi masalah, sehingga kami dapat menggunakan `expect`. Anda akan belajar tentang pemulihan dari kesalahan di bab [Chapter 9][recover].

### Mencetak Nilai dengan Placeholder `println!`

Selain kurung kurawal penutup, sejauh ini hanya ada satu baris lagi untuk didiskusikan dalam kode:

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-01/src/main.rs:print_guess}}
```

Baris ini mencetak string yang sekarang berisi input pengguna. Tanda kurung kurawal `{}` adalah _placeholder_: bayangkan `{}` sebagai penjepit kepiting kecil yang memiliki nilai di tempatnya. Saat mencetak nilai variabel, nama variabel bisa masuk ke dalam kurung kurawal. Saat mencetak hasil evaluasi ekspresi, tempatkan tanda kurung kurawal kosong di string format, lalu ikuti string format dengan daftar ekspresi yang dipisahkan koma untuk dicetak di setiap tempat penampung kurung kurawal kosong dalam urutan yang sama. Mencetak variabel dan hasil ekspresi dalam satu panggilan ke `println!` akan terlihat seperti ini:

```rust
let x = 5;
let y = 10;

println!("x = {x} and y + 2 = {}", y + 2);
```

Kode ini akan mencetak `x = 5 and y + 2 = 12`.

### Menguji Bagian Pertama

Mari kita uji bagian pertama dari permainan tebak-tebakan. Jalankan menggunakan `cargo run`:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-01/
cargo clean
cargo run
input 6 -->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 6.44s
     Running `target/debug/guessing_game`
Guess the number!
Please input your guess.
6
You guessed: 6
```

Pada titik ini, bagian pertama permainan selesai: kami mendapatkan input dari keyboard dan kemudian mencetaknya.

## Menghasilkan Nomor Rahasia

Selanjutnya, kita perlu membuat nomor rahasia yang akan coba ditebak oleh pengguna. Nomor rahasia harus berbeda setiap saat sehingga permainan ini menyenangkan untuk dimainkan lebih dari satu kali. Kami akan menggunakan angka acak antara 1 dan 100 agar permainan tidak terlalu sulit. Rust belum menyertakan fungsi nomor acak di pustaka standarnya. Namun, tim Rust memang menyediakan [`rand` crate][randcrate] dengan fungsionalitas tersebut.

### Menggunakan Crate untuk Mendapatkan Lebih Banyak Fungsi

Ingat bahwa crate adalah kumpulan file kode sumber Rust. Proyek yang kami bangun adalah _binary crate_, yang dapat dieksekusi. Crate `rand` adalah _library crate_, yang berisi kode yang dimaksudkan untuk digunakan dalam program lain dan tidak dapat dijalankan sendiri.

Koordinasi kargo untuk crate eksternal adalah tempat Kargo benar-benar bersinar. Sebelum kita dapat menulis kode yang menggunakan `rand`, kita perlu memodifikasi file _Cargo.toml_ untuk menyertakan crate `rand` sebagai dependensi. Buka file itu sekarang dan tambahkan baris berikut ke bawah, di bawah header `[dependencies]` bagian yang dibuat Cargo untuk Anda. Pastikan untuk menentukan `rand` persis seperti yang kita miliki di sini, dengan nomor versi ini, jika tidak contoh kode dalam tutorial ini mungkin tidak berfungsi:

<!-- When updating the version of `rand` used, also update the version of
`rand` used in these files so they all match:
* ch07-04-bringing-paths-into-scope-with-the-use-keyword.md
* ch14-03-cargo-workspaces.md
-->

<span class="filename">Nama file: Cargo.toml</span>

```toml
{{#include ../../listings/ch02-guessing-game-tutorial/listing-02-02/Cargo.toml:8:}}
```

Di file _Cargo.toml_, semua yang mengikuti header adalah bagian dari bagian tersebut yang berlanjut hingga bagian lain dimulai. Di dalam `[dependencies]` Anda memberi tahu Cargo crate eksternal mana yang bergantung pada proyek Anda dan versi crate mana yang Anda butuhkan. Dalam hal ini, kami menentukan `rand` crate dengan penentu versi semantik `0.8.5`. Cargo memahami [Semantic Versioning][semver] (terkadang disebut _SemVer_), yang merupakan standar penulisan nomor versi. Specifier `0.8.5` sebenarnya adalah kependekan dari `^0.8.5`, yang berarti versi apa pun yang setidaknya 0.8.5 tetapi di bawah 0.9.0.

Cargo menganggap versi ini memiliki API publik yang kompatibel dengan versi 0.8.5, dan spesifikasi ini memastikan Anda akan mendapatkan rilis _patch_ terbaru yang masih dapat dikompilasi dengan kode di bab ini. Setiap versi 0.9.0 atau lebih tinggi tidak dijamin memiliki API yang sama seperti yang digunakan dalam contoh disini.

Sekarang, tanpa mengubah kode apa pun, mari buat proyeknya, seperti yang ditunjukkan pada Daftar 2-2.

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
rm Cargo.lock
cargo clean
cargo build -->

```console
$ cargo build
    Updating crates.io index
  Downloaded rand v0.8.5
  Downloaded libc v0.2.127
  Downloaded getrandom v0.2.7
  Downloaded cfg-if v1.0.0
  Downloaded ppv-lite86 v0.2.16
  Downloaded rand_chacha v0.3.1
  Downloaded rand_core v0.6.3
   Compiling libc v0.2.127
   Compiling getrandom v0.2.7
   Compiling cfg-if v1.0.0
   Compiling ppv-lite86 v0.2.16
   Compiling rand_core v0.6.3
   Compiling rand_chacha v0.3.1
   Compiling rand v0.8.5
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 2.53s
```

<span class="caption">Daftar 2-2: Output dari menjalankan `cargo build` setelah menambahkan crate rand sebagai dependensi</span>

Anda mungkin melihat nomor versi yang berbeda (tetapi semuanya akan kompatibel dengan kode ini, terima kasih kepada SemVer!) Dan baris yang berbeda (tergantung pada sistem operasi), dan baris tersebut mungkin berada dalam urutan yang berbeda.

Saat kami menyertakan dependensi eksternal, Cargo mengambil versi terbaru dari semua yang dibutuhkan dependensi dari registri, yang merupakan salinan data dari [Crates.io][cratesio]. Crates.io adalah tempat orang-orang di ekosistem Rust memposting proyek Rust open source mereka untuk digunakan orang lain.

Setelah memperbarui registri, Cargo memeriksa bagian `[dependencies]` dan mengunduh setiap crate yang terdaftar yang belum diunduh. Dalam hal ini, meskipun kami hanya mendaftarkan `rand` sebagai dependensi, Cargo juga mengambil crate lain dimana `rand` bergantung agar dapat bekerja. Setelah mengunduh crate, Rust mengkompilasinya dan kemudian mengkompilasi proyek dengan dependensi yang tersedia.

Jika Anda menjalankan `cargo build` lagi tanpa melakukan perubahan apa pun, Anda tidak akan mendapatkan hasil apa pun selain dari baris `Finished`. Cargo mengetahui bahwa ia telah mengunduh dan mengompilasi dependensi, dan Anda belum mengubah apa pun di file _Cargo.toml_ Anda. Cargo juga mengetahui bahwa Anda belum mengubah apa pun tentang kode Anda, jadi Cargo juga tidak mengkompilasi ulang. Tanpa melakukan apa pun, itu hanya keluar.

Jika Anda membuka file _src/main.rs_, membuat perubahan sepele, lalu menyimpannya dan membangun kembali, Anda hanya akan melihat dua baris keluaran:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
touch src/main.rs
cargo build -->

```console
$ cargo build
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 2.53 secs
```

Baris-baris ini menunjukkan bahwa Cargo hanya memperbarui build dengan perubahan kecil Anda pada file _src/main.rs_. Dependensi Anda tidak berubah, jadi Cargo tahu bahwa ia dapat menggunakan kembali apa yang telah diunduh dan dikompilasi untuk itu.

#### Memastikan Build yang Dapat Direproduksi dengan File _Cargo.lock_

Cargo memiliki mekanisme yang memastikan Anda dapat membangun kembali artefak yang sama setiap kali Anda atau orang lain membuat kode Anda: Cargo hanya akan menggunakan versi dependensi yang Anda tentukan hingga Anda menyatakan sebaliknya. Misalnya, minggu depan versi crate `rand` 0.8.6 keluar, dan versi itu berisi perbaikan bug penting, tetapi juga berisi regresi yang akan merusak kode Anda. Untuk mengatasinya, Rust membuat file _Cargo.lock_ saat pertama kali Anda menjalankannya `cargo build`, jadi sekarang kita memilikinya di direktori _guessing_game_.

Saat Anda membangun proyek untuk pertama kalinya, Cargo mengetahui semua versi dependensi yang sesuai dengan kriteria dan kemudian menulisnya ke file _Cargo.lock_. Ketika Anda membangun proyek Anda di masa mendatang, Cargo akan melihat bahwa file _Cargo.lock_ ada dan akan menggunakan versi yang ditentukan di sana alih-alih melakukan semua pekerjaan mencari tahu lagi versinya. Ini memungkinkan Anda memiliki build yang dapat direproduksi secara otomatis. Dengan kata lain, proyek Anda akan tetap di 0.8.5 hingga Anda secara eksplisit memutakhirkan, berkat file _Cargo.lock_. Karena file _Cargo.lock_ penting untuk build yang dapat direproduksi, sering kali file ini dimasukkan ke kontrol sumber dengan kode lainnya di proyek Anda.

#### Memperbarui Crate untuk Mendapatkan Versi Baru

Saat Anda ingin memperbarui crate, Cargo menyediakan perintah `update`, yang akan mengabaikan file _Cargo.lock_ dan mengetahui semua versi terbaru yang sesuai dengan spesifikasi Anda di _Cargo.toml_ . Cargo kemudian akan menulis versi tersebut ke file _Cargo.lock_. Jika tidak, secara default, Cargo hanya akan mencari versi yang lebih besar dari 0.8.5 dan kurang dari 0.9.0. Jika crate `rand` telah merilis dua versi baru 0.8.6 dan 0.9.0, Anda akan melihat yang berikut jika Anda menjalankan `cargo update`:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-02/
cargo update
assuming there is a new 0.8.x version of rand; otherwise use another update
as a guide to creating the hypothetical output shown here -->

```console
$ cargo update
    Updating crates.io index
    Updating rand v0.8.5 -> v0.8.6
```

Cargo mengabaikan rilis 0.9.0. Pada titik ini, Anda juga akan melihat perubahan pada file _Cargo.lock_ Anda yang mencatat bahwa versi crate `rand` yang Anda gunakan sekarang adalah 0.8.6. Untuk menggunakan `rand` versi 0.9.0 atau versi apapun dalam seri 0.9._x_, Anda harus memperbarui file _Cargo.toml_ hingga terlihat seperti ini:

```toml
[dependencies]
rand = "0.9.0"
```

Ketika Anda menjalankan `cargo build`, Cargo akan memperbarui registri crate yang tersedia dan mengevaluasi kembali keperluan `rand` sesuai dengan versi baru yang telah Anda tentukan.

Masih banyak yang bisa dibahas tentang [Cargo][doccargo] dan [ekosistemnya][doccratesio], yang akan kita bahas di Bab 14, tetapi untuk saat ini, hanya itu yang perlu Anda ketahui. Cargo membuatnya sangat mudah untuk menggunakan kembali perpustakaan, sehingga Rustacean dapat menulis proyek yang lebih kecil yang dirangkai dari sejumlah paket.

### Menghasilkan Nomor Acak

Mari kita mulai gunakan `rand` untuk menghasilkan angka untuk ditebak. Langkah selanjutnya adalah memperbarui _src/main.rs_, seperti yang ditunjukkan pada Daftar 2-3.

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-03/src/main.rs:all}}
```

<span class="caption">Daftar 2-3: Menambahkan kode untuk menghasilkan angka acak</span>

Pertama kita tambahkan baris `use rand::Rng;`. Trait `Rng` tersebut menentukan metode yang diterapkan oleh generator angka acak, dan trait ini harus berada dalam cakupan agar kita dapat menggunakan metode tersebut. Bab 10 akan membahas trait secara rinci.

Selanjutnya, kami menambahkan dua baris di tengah. Di baris pertama, kita memanggil `rand::thread_rng` fungsi yang memberi kita penghasil angka acak tertentu yang akan kita gunakan: yang lokal untuk utas eksekusi saat ini dan dihasilkan oleh sistem operasi. Kemudian kami memanggil metode `gen_range` pada generator angka acak. Metode ini ditentukan oleh trait `Rng` yang kami bawa ke dalam scope dengan pernyataan `use rand::Rng;`. Metode `gen_range` mengambil ekspresi rentang sebagai argumen dan menghasilkan angka acak dalam rentang. Jenis ekspresi rentang yang kita gunakan di sini mengambil bentuk `start..=end` dan disertakan pada batas bawah dan atas, jadi kita perlu menentukan `1..=100` untuk meminta angka antara 1 dan 100.

> Catatan: Anda tidak hanya mengetahui trait mana yang harus digunakan dan metode serta fungsi mana yang akan dipanggil dari crate, sehingga setiap crate memiliki dokumentasi dengan instruksi untuk menggunakannya. Fitur menarik lainnya dari Cargo adalah menjalankan perintah `cargo doc --open` akan membangun dokumentasi yang disediakan oleh semua dependensi Anda secara lokal dan membukanya di browser Anda. Jika Anda tertarik dengan fungsionalitas lain di dalam crate `rand`, misalnya, jalankan `cargo doc --open` dan klik `rand` di sidebar di sebelah kiri.

Baris baru kedua mencetak nomor rahasia. Ini berguna saat kami mengembangkan program agar dapat mengujinya, tetapi kami akan menghapusnya dari versi final. Ini bukan permainan jika program mencetak jawabannya segera setelah dimulai!

Coba jalankan program beberapa kali:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-03/
cargo run
4
cargo run
5
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 2.53s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 7
Please input your guess.
4
You guessed: 4

$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 83
Please input your guess.
5
You guessed: 5
```

Anda harus mendapatkan angka acak yang berbeda, dan semuanya harus berupa angka antara 1 dan 100. Kerja bagus!

## Membandingkan Tebakan dengan Angka Rahasia

Sekarang kami memiliki input pengguna dan nomor acak, kami dapat membandingkannya. Langkah tersebut ditunjukkan pada Daftar 2-4. Perhatikan bahwa kode ini belum dapat dikompilasi, seperti yang akan kami jelaskan.

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-04/src/main.rs:here}}
```

<span class="caption">Daftar 2-4: Menangani kemungkinan nilai kembalian dari membandingkan dua angka</span>

Pertama kita tambahkan pernyataan `use` lain, membawa tipe yang dipanggil `std::cmp::Ordering` ke dalam ruang lingkup dari perpustakaan standar. Tipe `Ordering` adalah enum lain dan memiliki varian `Less`, `Greater`, dan `Equal`. Ini adalah tiga hasil yang mungkin terjadi ketika Anda membandingkan dua nilai.

Kemudian kami menambahkan lima baris baru di bagian bawah yang menggunakan tipe `Ordering` tersebut. Metode `cmp` ini membandingkan dua nilai dan dapat dipanggil pada apa saja yang dapat dibandingkan. Dibutuhkan referensi ke apa pun yang ingin Anda bandingkan: ini dia membandingkan `guess` dengan `secret_number`. Kemudian ia mengembalikan varian enum `Ordering` yang kami bawa ke dalam ruang lingkup dengan pernyataan `use`. Kami menggunakan ekspresi [`match`][match] untuk memutuskan apa yang harus dilakukan selanjutnya berdasarkan varian `Ordering` mana yang dikembalikan dari panggilan ke `cmp` dengan nilai di dalam `guess` dan `secret_number`.

Ekspresi `match` terdiri dari _arms_. Arm (lengan) terdiri dari _pattern_ (pola) untuk dicocokkan, dan kode yang harus dijalankan jika nilai yang diberikan ke `match` sesuai dengan pola lengan itu. Rust mengambil nilai yang diberikan ke `match` dan melihat pola masing-masing lengan secara bergantian. Pola dan konstruk `match` adalah fitur Rust yang kuat: mereka memungkinkan Anda mengekspresikan berbagai situasi yang mungkin dihadapi kode Anda dan memastikan Anda menangani semuanya. Fitur-fitur ini akan dibahas secara rinci masing-masing di Bab 6 dan Bab 18.

Mari telusuri contoh dengan ekspresi `match` yang kita gunakan di sini. Katakanlah pengguna telah menebak 50 dan nomor rahasia yang dihasilkan secara acak kali ini adalah 38.

Saat kode membandingkan 50 dengan 38,metode `cmp` akan mengembalikan `Ordering::Greater` karena 50 lebih besar dari 38. Ekspresi `match` mengembalikan nilai `Ordering::Greater` dan mulai memeriksa pola setiap lengan. Itu melihat pola lengan pertama, `Ordering::Less`, dan melihat bahwa nilai `Ordering::Greater` tidak cocok dengan `Ordering::Less`, sehingga mengabaikan kode di lengan itu dan pindah ke lengan berikutnya. Pola lengan selanjutnya adalah `Ordering::Greater`, yang cocok dengan `Ordering::Greater`! Kode terkait di lengan itu akan dieksekusi dan mencetak `Too big!` ke layar. Ekspresi `match` berakhir setelah perbandingan pertama yang berhasil, sehingga tidak akan terlihat pada lengan terakhir dalam skenario ini.

Namun, kode di Listing 2-4 belum dapat dikompilasi. Mari kita coba:

<!--
The error numbers in this output should be that of the code **WITHOUT** the
anchor or snip comments
-->

```console
{{#include ../../listings/ch02-guessing-game-tutorial/listing-02-04/output.txt}}
```

Inti dari kesalahan menyatakan bahwa ada tipe yang tidak cocok (_mismatched types_). Rust memiliki sistem tipe statis yang kuat. Namun, ia juga memiliki inferensi tipe. Saat kami menulis `let mut guess = String::new()`, Rust dapat menyimpulkan bahwa `guess` seharusnya `String` dan tidak membuat kami mengharuskan menulis tipenya. `secret_number`, di sisi lain, adalah tipe angka. Beberapa tipe angka Rust dapat memiliki nilai antara 1 dan 100: `i32`, angka 32-bit; `u32`, angka 32-bit yang tidak ditandatangani (_unsigned_); i64, angka 64-bit; serta yang lain. Kecuali ditentukan yang lain, Rust secara default memberikan tipe i32 ke angka, yang merupakan tipe `secret_number` kecuali Anda menambahkan informasi tipe di tempat lain yang akan menyebabkan Rust menyimpulkan jenis numerik yang berbeda. Alasan kesalahannya adalah Rust tidak dapat membandingkan tipe string dengan angka.

Pada akhirnya, kami ingin mengonversi `String` yang dibaca sebagai input menjadi tipe bilangan real sehingga kami dapat membandingkannya secara numerik dengan angka rahasia. Kami melakukannya dengan menambahkan baris ini ke badan fungsi `main`:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/no-listing-03-convert-string-to-number/src/main.rs:here}}
```

Barisnya adalah:

```rust,ignore
let guess: u32 = guess.trim().parse().expect("Please type a number!");
```

Kami membuat variabel bernama `guess`. Tapi tunggu, bukankah program tersebut sudah memiliki variabel bernama `guess`? Ya, tapi membantu Rust memungkinkan kita untuk membayangi (_shadowing_) nilai `guess` sebelumnya dengan yang baru. Shadowing memungkinkan kita menggunakan kembali nama variabel `guess` alih-alih memaksa kita membuat dua variabel unik, seperti `guess_str` dan `guess`, misalnya. Kami akan membahasnya lebih detail di [Bab 3][shadowing], tetapi untuk saat ini, ketahuilah bahwa fitur ini sering digunakan saat Anda ingin mengonversi nilai dari satu tipe ke tipe lainnya.

Kami mengikat variabel baru ini ke ekspresi `guess.trim().parse()`. Ekspresi `guess` mengacu pada variabel asli `guess` yang berisi input string. Metode `trim` pada instance `String` akan menghilangkan spasi di awal dan akhir, yang harus kita lakukan untuk dapat membandingkan string dengan `u32`, yang hanya dapat berisi data numerik. Pengguna harus menekan <span class="keystroke">enter</span> untuk mengakhiri `read_line` dan memasukkan tebakan mereka, yang menambahkan karakter baris baru ke string. Misalnya, jika pengguna mengetik <span class="keystroke">5</span> dan menekan <span class="keystroke">enter</span>, tampilan `guess` seperti ini: `5\n`. `\n` mewakili “baris baru.” (Pada Windows, menekan <span class="keystroke">enter</span> menghasilkan _carriage return_ dan baris baru, `\r\n`.) Metode `trim` menghilangkan `\n` atau `\r\n`, hanya menghasilkan `5`.

Metode [`parse` pada string][parse] mengubah string menjadi tipe lain. Di sini, kami menggunakannya untuk mengonversi dari string ke angka. Kita perlu memberi tahu Rust tipe angka persis yang kita inginkan dengan menggunakan `let guess: u32`. Tanda titik dua (`:`) setelah `guess` memberi tahu Rust bahwa kita akan memberi anotasi pada tipe variabel. Rust memiliki beberapa tipe angka bawaan; `u32` yang terlihat di sini adalah bilangan bulat 32-bit _unsigned_. Ini adalah pilihan default yang bagus untuk angka positif kecil. Anda akan belajar tentang tipe angka lainnya di [Bab 3][integers].

Selain itu, anotasi `u32` dalam program contoh ini dan perbandingan dengan `secret_number` Rust akan menyimpulkan bahwa `secret_number` seharusnya `u32`. Jadi sekarang perbandingannya adalah antara dua nilai dengan tipe yang sama!

Metode `parse` ini hanya akan bekerja pada karakter yang secara logis dapat diubah menjadi angka sehingga dapat dengan mudah menyebabkan kesalahan. Jika, misalnya, string berisi `A👍%`, tidak akan ada cara untuk mengubahnya menjadi angka. Karena mungkin gagal, metode `parse` mengembalikan sebuah tipe `Result`, seperti halnya metode `read_line` (dibahas sebelumnya di [“Menangani Potensi Kegagalan dengan `Result`”](#handling-potential-failure-with-result)). Kami akan memperlakukan `Result` dengan cara yang sama dengan menggunakan metode `expect`. Jika `parse` mengembalikan `Err` varian `Result` karena tidak dapat membuat nomor dari string, panggilan `expect` akan menghentikan permainan dan mencetak pesan yang kami berikan. Jika `parse` berhasil mengubah string menjadi angka, itu akan mengembalikan varian `Ok` dari `Result`, dan `expect` akan mengembalikan nomor yang kita inginkan dari nilai `Ok`.

Mari kita jalankan programnya sekarang:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/no-listing-03-convert-string-to-number/
cargo run
  76
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 0.43s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 58
Please input your guess.
  76
You guessed: 76
Too big!
```

Bagus! Meskipun spasi ditambahkan sebelum tebakan, program tetap mengetahui bahwa pengguna menebak 76. Jalankan program beberapa kali untuk memverifikasi perilaku yang berbeda dengan jenis masukan yang berbeda: tebak angka dengan benar, tebak angka yang terlalu tinggi, dan tebak angka yang terlalu rendah.

Kami memiliki sebagian besar permainan yang berfungsi sekarang, tetapi pengguna hanya dapat membuat satu tebakan. Mari ubah itu dengan menambahkan _loop_!

## Mengizinkan Banyak Tebakan dengan Perulangan

Kata kunci `loop` membuat perulangan tak terbatas. Kami akan menambahkan perulangan untuk memberi pengguna lebih banyak peluang untuk menebak nomornya:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/no-listing-04-looping/src/main.rs:here}}
```

Seperti yang Anda lihat, kami telah memindahkan semuanya dari tebakan input prompt ke dalam satu perulangan. Pastikan untuk membuat indentasi baris di dalam loop masing-masing empat spasi lagi dan jalankan program lagi. Program sekarang akan meminta tebakan lain selamanya, yang sebenarnya menimbulkan masalah baru. Sepertinya pengguna tidak bisa berhenti!

Pengguna selalu dapat menginterupsi program dengan menggunakan pintasan keyboard <span class="keystroke">ctrl-c</span>. Tapi ada cara lain untuk menghindari monster yang tak pernah puas ini, seperti yang disebutkan dalam diskusi `parse` di [“Membandingkan Tebakan dengan Angka Rahasia”](#comparing-the-guess-to-the-secret-number): jika pengguna memasukkan jawaban non-angka, program akan macet. Kami dapat memanfaatkan itu untuk memungkinkan pengguna keluar, seperti yang ditunjukkan di sini:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/no-listing-04-looping/
cargo run
(too small guess)
(too big guess)
(correct guess)
quit
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 1.50s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 59
Please input your guess.
45
You guessed: 45
Too small!
Please input your guess.
60
You guessed: 60
Too big!
Please input your guess.
59
You guessed: 59
You win!
Please input your guess.
quit
thread 'main' panicked at 'Please type a number!: ParseIntError { kind: InvalidDigit }', src/main.rs:28:47
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

Mengetik `quit` akan keluar dari game, tetapi seperti yang akan Anda lihat, begitu juga dengan memasukkan input non-angka lainnya. Ini kurang optimal, setidaknya; kami ingin permainan juga berhenti ketika angka yang benar sudah ditebak.

### Berhenti Setelah Tebakan yang Benar

Mari memprogram game untuk berhenti saat pengguna menang dengan menambahkan pernyataan `break`:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/no-listing-05-quitting/src/main.rs:here}}
```

Menambahkan baris `break` setelah `You win!` membuat program keluar dari loop saat pengguna menebak nomor rahasia dengan benar. Keluar dari loop juga berarti keluar dari program, karena loop adalah bagian terakhir dari `main`.

### Menangani Input yang Tidak Valid

Untuk lebih menyempurnakan perilaku game, alih-alih menghentikan program saat pengguna memasukkan non-angka, mari buat game mengabaikan non-angka sehingga pengguna dapat terus menebak. Kita dapat melakukannya dengan mengubah baris dimana `guess` yang dikonversi dari `String` menjadi `u32`, seperti yang ditunjukkan pada Daftar 2-5.

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-05/src/main.rs:here}}
```

<span class="caption">Daftar 2-5: Mengabaikan tebakan non-angka dan meminta tebakan lain alih-alih menghentikan program</span>

Kami beralih dari panggilan `expect` ke ekspresi `match` untuk beralih dari menabrak kesalahan ke menangani kesalahan. Ingat bahwa `parse` mengembalikan tipe `Result` dan `Result` merupakan enum yang memiliki varian `Ok` dan `Err`. Kami menggunakan ekspresi `match` di sini, seperti yang kami lakukan dengan hasil `Ordering` metode `cmp`.

Jika `parse` berhasil mengubah string menjadi angka, itu akan mengembalikan nilai `Ok` yang berisi angka yang dihasilkan. Nilai `Ok` akan cocok dengan pola lengan pertama, dan ekspresi `match` hanya akan mengembalikan nilai `num` yang dihasilkan `parse` dan dimasukkan ke dalam nilai `Ok`. Angka itu akan berakhir tepat di tempat yang kita inginkan di variabel `guess` baru yang kita buat.

Jika `parse` tidak dapat mengubah string menjadi angka, ini akan mengembalikan nilai `Err` yang berisi lebih banyak informasi tentang kesalahan tersebut. Nilai `Err` tidak cocok dengan pola `Ok(num)` di lengan pertama `match`, tetapi cocok dengan pola `Err(_)` di lengan kedua. Garis bawah, `_`, adalah nilai umum; dalam contoh ini, kami mengatakan kami ingin mencocokkan semua nilai `Err`, tidak peduli informasi apa yang mereka miliki di dalamnya. Jadi program akan mengeksekusi kode lengan kedua, `continue`, yang memberi tahu program untuk pergi ke iterasi loop berikutnya dan meminta tebakan lain. Jadi, secara efektif, program mengabaikan semua kesalahan `parse` yang mungkin terjadi!

Sekarang semua yang ada di program harus berfungsi seperti yang diharapkan. Mari kita coba:

<!-- manual-regeneration
cd listings/ch02-guessing-game-tutorial/listing-02-05/
cargo run
(too small guess)
(too big guess)
foo
(correct guess)
-->

```console
$ cargo run
   Compiling guessing_game v0.1.0 (file:///projects/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 4.45s
     Running `target/debug/guessing_game`
Guess the number!
The secret number is: 61
Please input your guess.
10
You guessed: 10
Too small!
Please input your guess.
99
You guessed: 99
Too big!
Please input your guess.
foo
Please input your guess.
61
You guessed: 61
You win!
```

Luar biasa! Dengan satu perubahan kecil terakhir, kita akan menyelesaikan permainan tebak-tebakan. Ingatlah bahwa program masih mencetak nomor rahasia. Itu bekerja dengan baik untuk pengujian, tetapi itu merusak permainan. Mari kita hapus `println!` yang mengeluarkan nomor rahasia. Daftar 2-6 menunjukkan kode akhir.

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch02-guessing-game-tutorial/listing-02-06/src/main.rs}}
```

<span class="caption">Daftar 2-6: Menyelesaikan kode permainan tebak-tebakan</span>

Pada titik ini, Anda telah berhasil membuat game tebak-tebakan. Selamat!

## Ringkasan

Proyek ini adalah cara praktis untuk memperkenalkan Anda pada banyak konsep Rust baru: `let`, `match`, fungsi, penggunaan crate eksternal, dan banyak lagi. Dalam beberapa bab berikutnya, Anda akan mempelajari konsep-konsep ini secara lebih mendetail. Bab 3 mencakup konsep yang dimiliki sebagian besar bahasa pemrograman, seperti variabel, tipe data, dan fungsi, dan menunjukkan cara menggunakannya di Rust. Bab 4 mengeksplorasi kepemilikan, sebuah fitur yang membuat Rust berbeda dari bahasa lain. Bab 5 membahas struct dan sintaks metode, dan Bab 6 menjelaskan cara kerja enum.

[prelude]: ../std/prelude/index.html
[variables-and-mutability]: ch03-01-variables-and-mutability.html#variables-and-mutability
[comments]: ch03-04-comments.html
[string]: ../std/string/struct.String.html
[iostdin]: ../std/io/struct.Stdin.html
[read_line]: ../std/io/struct.Stdin.html#method.read_line
[result]: ../std/result/enum.Result.html
[enums]: ch06-00-enums.html
[expect]: ../std/result/enum.Result.html#method.expect
[recover]: ch09-02-recoverable-errors-with-result.html
[randcrate]: https://crates.io/crates/rand
[semver]: http://semver.org
[cratesio]: https://crates.io/
[doccargo]: http://doc.crates.io
[doccratesio]: http://doc.crates.io/crates-io.html
[match]: ch06-02-match.html
[shadowing]: ch03-01-variables-and-mutability.html#shadowing
[parse]: ../std/primitive.str.html#method.parse
[integers]: ch03-02-data-types.html#integer-types

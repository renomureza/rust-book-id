## Tipe Data

Setiap nilai di Rust memiliki tipe data tertentu, yang memberi tahu Rust jenis data apa yang ditentukan sehingga Rust mengetahui cara bekerja dengan data tersebut. Kita akan melihat dua himpunan bagian tipe data: _scalar_ dan _compound_.

Perlu diingat bahwa Rust adalah bahasa _statically typed_, yang berarti ia harus mengetahui tipe semua variabel pada waktu kompilasi. Kompiler biasanya dapat menyimpulkan tipe apa yang ingin kita gunakan berdasarkan nilai dan bagaimana kita menggunakannya. Dalam kasus ketika banyak tipe dimungkinkan, seperti ketika kita mengonversi `String` ke tipe numerik menggunakan `parse` di bagian [“Membandingkan Tebakan dengan Angka Rahasia”][comparing-the-guess-to-the-secret-number] di Bab 2, kita harus menambahkan anotasi tipe, seperti ini:

```rust
let guess: u32 = "42".parse().expect("Not a number!");
```

Jika kami tidak menambahkan anotasi tipe `: u32` yang ditunjukkan pada kode sebelumnya, Rust akan menampilkan kesalahan berikut, yang berarti kompiler memerlukan lebih banyak informasi dari kami untuk mengetahui tipe yang ingin kami gunakan:

```console
{{#include ../../listings/ch03-common-programming-concepts/output-only-01-no-type-annotations/output.txt}}
```

Anda akan melihat beragam jenis anotasi untuk tipe data lainnya.

### Tipe Scalar

Tipe _scalar_ mewakili nilai tunggal. Rust memiliki empat tipe _scalar_ utama: _integer_, _floating-point_, Boolean, dan karakter. Anda mungkin mengenali ini dari bahasa pemrograman lain. Mari lompat ke cara kerjanya di Rust.

#### Tipe Integer

Bilangan bulat (_integer_) adalah bilangan tanpa komponen pecahan. Kami menggunakan satu tipe integer di Bab 2, tipe `u32`. Deklarasi tipe ini menunjukkan bahwa nilai yang dikaitkan dengannya harus berupa bilangan bulat yang tidak ditandatangani (_unsigned_) (jenis bilangan bulat yang ditandatangani (_signed_) dimulai dengan `i` alih-alih `u`) yang membutuhkan ruang 32 bit. Tabel 3-1 menunjukkan tipe integer bawaan di Rust. Kita dapat menggunakan salah satu varian ini untuk mendeklarasikan tipe nilai integer.

<span class="caption">Table 3-1: Tipe Integer dalam Rust</span>

| Length  | Signed  | Unsigned |
| ------- | ------- | -------- |
| 8-bit   | `i8`    | `u8`     |
| 16-bit  | `i16`   | `u16`    |
| 32-bit  | `i32`   | `u32`    |
| 64-bit  | `i64`   | `u64`    |
| 128-bit | `i128`  | `u128`   |
| arch    | `isize` | `usize`  |

Setiap varian bisa _signed_ atau _unsigned_ dan memiliki ukuran eksplisit. Bertanda tangan dan tidak bertanda mengacu pada apakah angka itu mungkin negatif — dengan kata lain, apakah angka tersebut perlu diberi tanda (_signed_) atau apakah angka itu hanya akan selalu positif dan oleh karena itu dapat direpresentasikan tanpa tanda (_unsigned_). Ini seperti menulis angka di atas kertas: ketika tanda itu penting, sebuah angka ditunjukkan dengan tanda plus atau minus; namun, jika aman untuk menganggap angkanya positif, angka itu ditampilkan tanpa tanda. Nomor yang ditandatangani disimpan menggunakan representasi [komplemen dua][twos-complement].

Setiap varian _signed_ dapat menyimpan angka dari -(2<sup>n - 1</sup>) hingga 2<sup>n -
1</sup> - 1 inklusif, di mana `n` adalah jumlah bit yang digunakan varian. Jadi `i8` menyimpan angka dari -(2<sup>7</sup>) hingga 2<sup>7</sup> - 1, yang sama dengan -128 hingga 127. Varian _unsigned_ dapat menyimpan angka dari 0 hingga 2<sup>n</sup> - 1, jadi `u8` menyimpan angka dari 0 hingga 2<sup>8</sup> - 1, yang sama dengan 0 sampai 255.

Selain itu, tipe `isize` dan `usize` bergantung pada arsitektur komputer tempat program Anda berjalan, yang ditunjukkan dalam tabel sebagai “arch”: 64 bit jika Anda menggunakan arsitektur 64 bit dan 32 bit jika Anda menggunakan arsitektur 32-bit.

Anda dapat menulis integer literal dalam salah satu bentuk yang ditunjukkan pada Tabel 3-2. Perhatikan bahwa angka literal yang bisa berupa beberapa tipe numerik memungkinkan tipe sufiks, seperti `57u8`, untuk menunjukkan tipenya. Angka literal juga dapat menggunakan `_` sebagai pemisah visual untuk membuat angka lebih mudah dibaca, seperti `1_000`, yang akan memiliki nilai yang sama seperti jika Anda telah menentukan `1000`.

<span class="caption">Table 3-2: Literal Integer di Rust</span>

| Number literals  | Example       |
| ---------------- | ------------- |
| Decimal          | `98_222`      |
| Hex              | `0xff`        |
| Octal            | `0o77`        |
| Binary           | `0b1111_0000` |
| Byte (`u8` only) | `b'A'`        |

Jadi, bagaimana Anda tahu jenis bilangan bulat mana yang digunakan? Jika Anda tidak yakin, default Rust umumnya adalah tempat yang baik untuk memulai: tipe integer default ke `i32`. Situasi utama di mana Anda akan menggunakan `isize` atau `usize` saat mengindeks semacam koleksi.

> ##### Integer Overflow
>
> Misalkan Anda memiliki variabel bertipe `u8` yang dapat menampung nilai antara 0 hingga 255. Jika Anda mencoba mengubah variabel ke nilai di luar rentang tersebut, seperti 256, akan terjadi _integer overflow_, yang dapat mengakibatkan salah satu dari dua perilaku. Saat Anda mengompilasi dalam mode debug, Rust menyertakan pemeriksaan untuk _integer overflow_ yang menyebabkan program Anda panik saat runtime jika perilaku ini terjadi. Rust menggunakan istilah panik saat program keluar dengan kesalahan; kita akan membahas kepanikan secara lebih mendalam di bagian “Kesalahan yang Tidak Dapat Dipulihkan dengan panic!” [“Kesalahan yang Tidak Dapat Dipulihkan dengan `panic!`”][unrecoverable-errors-with-panic] di Bab 9.
>
> Saat Anda mengkompilasi dalam mode rilis dengan bendera `--release`, Rust tidak menyertakan pemeriksaan untuk _integer overflow_ yang menyebabkan kepanikan. Sebagai gantinya, jika terjadi _overflow_, Rust melakukan _two's complement wrapping_. Singkatnya, nilai-nilai yang lebih besar dari nilai maksimum yang dapat disimpan oleh tipe "membungkus" hingga nilai minimum yang dapat dipegang oleh tipe tersebut. Dalam kasus `u8`, nilai 256 menjadi 0, nilai 257 menjadi 1, dan seterusnya. Program tidak akan panik, tetapi variabel akan memiliki nilai yang mungkin tidak seperti yang Anda harapkan. Mengandalkan perilaku pembungkusan _integer overflow_ dianggap sebagai kesalahan.
>
> Untuk secara eksplisit menangani kemungkinan _overflow_, Anda dapat menggunakan rangkaian metode berikut yang disediakan oleh pustaka standar untuk tipe numerik primitif:
>
> - Bungkus semua mode dengan method `wrapping_*`, seperti `wrapping_add`.
> - Kembalikan nilai `None` jika ada _overflow_ dengan method `checked_*`.
> - Kembalikan nilai dan boolean yang menunjukkan apakah ada kelebihan dengan method `overflowing_*`.
> - _Saturate_ pada nilai minimum atau nilai maksimum dengan method `saturating_*`.

#### Tipe Floating-Point

Karat juga memiliki dua tipe primitif untuk angka _floating-point_ , yaitu angka dengan titik desimal. Tipe _floating-point_ Rust adalah `f32` dan `f64`, yang masing-masing berukuran 32 bit dan 64 bit. Tipe defaultnya adalah `f64` karena pada CPU modern, kecepatannya kira-kira sama dengan `f32` tetapi lebih presisi. Semua tipe _floating-point_ adalah _signed_.

Berikut adalah contoh yang menunjukkan aksi bilangan _floating-point_:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-06-floating-point/src/main.rs}}
```

Angka _floating-point_ direpresentasikan sesuai dengan standar IEEE-754. Tipe `f32` adalah _single-precision_, dan `f64` _double precision_.

#### Operasi Numerik

Rust mendukung operasi matematika dasar yang Anda harapkan untuk semua jenis angka: penjumlahan, pengurangan, perkalian, pembagian, dan sisa. Pembagian bilangan bulat terpotong menuju nol ke bilangan bulat terdekat. Kode berikut menunjukkan bagaimana Anda akan menggunakan setiap operasi numerik dalam sebuah pernyataan `let`:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-07-numeric-operations/src/main.rs}}
```

Setiap ekspresi dalam pernyataan ini menggunakan operator matematika dan mengevaluasi ke satu nilai, yang kemudian terikat ke variabel. [Lampiran B][appendix_b] berisi daftar semua operator yang disediakan oleh Rust.

#### Tipe Boolean

Seperti kebanyakan bahasa pemrograman lainnya, tipe Boolean di Rust memiliki dua kemungkinan nilai: `true` dan `false`. Boolean berukuran satu byte. Tipe Boolean di Rust ditentukan menggunakan `bool`. Misalnya:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-08-boolean/src/main.rs}}
```

Cara utama untuk menggunakan nilai Boolean adalah melalui kondisional, seperti ekspresi `if`. Kami akan membahas cara kerja ekspresi `if` di Rust di bagian [Aliran Kontrol”][control-flow].

#### Tipe Karakter

Tipe `char` Rust adalah tipe abjad bahasa yang paling primitif. Berikut adalah beberapa contoh mendeklarasikan nilai `char`:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-09-char/src/main.rs}}
```

Perhatikan bahwa kami menentukan literal `char` dengan kutip tunggal, berbeda dengan string literal, yang menggunakan kutip ganda. Tipe `char` Rust berukuran empat byte dan mewakili Unicode Scalar Value, yang artinya dapat mewakili lebih dari sekadar ASCII. Huruf beraksen; Karakter Cina, Jepang, dan Korea; emoji; dan spasi dengan lebar nol adalah nilai `char` yang valid di Rust. Unicode Scalar Value berkisar dari `U+0000` hingga `U+D7FF` dan `U+E000` hingga `U+10FFFF` inklusif. Namun, "char" sebenarnya bukan konsep di Unicode, jadi intuisi manusia tentang apa itu "karakter" mungkin tidak cocok dengan `char` yang ada di Rust. Kami akan membahas topik ini secara detail di [“Menyimpan Teks Bersandi UTF-8 dengan String”][strings] di Bab 8.

### Tipe Compound (Tipe Gabungan)

_Compound Type_ dapat mengelompokkan beberapa nilai menjadi satu tipe. Rust memiliki dua tipe _compound_ primitif: tuple dan array.

#### Tipe Tuple

Tuple adalah cara umum untuk mengelompokkan sejumlah nilai dari berbagai tipe menjadi satu tipe majemuk. Tuple memiliki panjang tetap: setelah dideklarasikan, mereka tidak dapat tumbuh atau menyusut ukurannya.

Kami membuat tuple dengan menulis daftar nilai yang dipisahkan koma di dalam tanda kurung. Setiap posisi dalam tuple memiliki tipe, dan tipe setiap nilai dalam tuple tidak harus sama. Kami telah menambahkan anotasi tipe opsional dalam contoh ini:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-10-tuples/src/main.rs}}
```

Variabel `tup` mengikat seluruh tuple karena tuple dianggap sebagai elemen majemuk tunggal. Untuk mendapatkan nilai individual dari tuple, kita dapat menggunakan pencocokan pola untuk men-_destructure_ nilai tuple, seperti ini:

<span class="filename">Filename: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-11-destructuring-tuples/src/main.rs}}
```

Program ini pertama-tama membuat tuple dan mengikatnya ke variabel `tup`. Ini kemudian menggunakan pola dengan `let` untuk mengambil `tup` dan mengubahnya menjadi tiga variabel terpisah, `x`, `y`, dan `z`. Ini disebut destrukturisasi karena memecah tupel tunggal menjadi tiga bagian. Akhirnya, program mencetak nilai `y`, yaitu `6.4`.

Kita juga bisa mengakses elemen tuple secara langsung dengan menggunakan tanda titik (`.`) diikuti dengan indeks dari nilai yang ingin kita akses. Misalnya:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-12-tuple-indexing/src/main.rs}}
```

Program ini membuat tuple `x` dan kemudian mengakses setiap elemen tuple menggunakan indeksnya masing-masing. Seperti kebanyakan bahasa pemrograman, indeks pertama dalam sebuah tuple adalah 0.

Tuple tanpa nilai apa pun memiliki nama khusus, _unit_. Nilai ini dan tipe yang sesuai keduanya ditulis `()` dan mewakili nilai kosong atau tipe kembalian kosong. Ekspresi secara implisit mengembalikan nilai unit jika tidak mengembalikan nilai lainnya.

#### Tipe Array

Cara lain untuk memiliki kumpulan beberapa nilai adalah dengan _array_. Tidak seperti tuple, setiap elemen array harus memiliki tipe yang sama. Tidak seperti array di beberapa bahasa lain, array di Rust memiliki panjang yang tetap.

Kami menulis nilai dalam array sebagai daftar yang dipisahkan koma di dalam tanda kurung siku:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-13-arrays/src/main.rs}}
```

Array berguna saat Anda ingin data Anda dialokasikan di _stack_ dan bukan di _heap_ (kita akan membahas tumpukan dan tumpukan lebih lanjut di [Bab 4][stack-and-heap]) atau saat Anda ingin memastikan bahwa Anda selalu memiliki jumlah elemen yang tetap. Array tidak sefleksibel tipe vector. _Vector_ adalah jenis koleksi serupa yang disediakan oleh pustaka standar yang diizinkan untuk memperbesar atau memperkecil ukurannya. Jika Anda tidak yakin apakah akan menggunakan array atau vector, kemungkinan besar Anda harus menggunakan vector. [Bab 8][vectors] membahas vector secara lebih rinci.

Namun, array lebih berguna ketika Anda mengetahui jumlah elemen tidak perlu diubah. Misalnya, jika Anda menggunakan nama bulan dalam sebuah program, Anda mungkin akan menggunakan array daripada vector karena Anda tahu itu akan selalu berisi 12 elemen:

```rust
let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
```

Anda menulis tipe array menggunakan tanda kurung siku dengan tipe setiap elemen, titik koma, dan kemudian jumlah elemen dalam array, seperti ini:

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

Di sini, `i32` adalah tipe setiap elemen. Setelah titik koma, angka `5` menunjukkan array berisi lima elemen.

Anda juga dapat menginisialisasi array agar berisi nilai yang sama untuk setiap elemen dengan menentukan nilai awal, diikuti dengan titik koma, lalu panjang array dalam tanda kurung siku, seperti yang ditunjukkan di sini:

```rust
let a = [3; 5];
```

Array bernama `a` akan berisi `5` elemen yang semuanya akan disetel ke nilai `3` awalnya. Ini sama dengan menulis `let a = [3, 3, 3, 3, 3];` tetapi dengan cara yang lebih ringkas.

##### Mengakses Elemen Array

Array adalah potongan tunggal memori dengan ukuran tetap yang diketahui yang dapat dialokasikan pada stack. Anda dapat mengakses elemen array menggunakan pengindeksan, seperti ini:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-14-array-indexing/src/main.rs}}
```

Dalam contoh ini, variabel bernama `first` akan mendapatkan nilai `1` karena itu adalah nilai array dalam indeks `[0]`. Variabel bernama `second` akan mendapatkan nilai `2` dari indeks `[1]` dalam array.

##### Akses Elemen Array Tidak Valid

Mari kita lihat apa yang terjadi jika Anda mencoba mengakses elemen array yang melewati akhir array. Katakanlah Anda menjalankan kode ini, mirip dengan permainan tebak-tebakan di Bab 2, untuk mendapatkan indeks array dari pengguna:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore,panics
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-15-invalid-array-access/src/main.rs}}
```

Kode ini berhasil dikompilasi. Jika Anda menjalankan kode ini menggunakan `cargo run` dan memasukkan `0`, `1`, `2`, `3`, atau `4`, program akan mencetak nilai yang sesuai pada indeks di dalam array tersebut. Jika Anda memasukkan angka setelah akhir array, seperti `10`, Anda akan melihat keluaran seperti ini:

<!-- manual-regeneration
cd listings/ch03-common-programming-concepts/no-listing-15-invalid-array-access
cargo run
10
-->

```console
thread 'main' panicked at 'index out of bounds: the len is 5 but the index is 10', src/main.rs:19:19
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

Program mengakibatkan kesalahan runtime saat menggunakan nilai yang tidak valid dalam operasi pengindeksan. Program keluar dengan pesan kesalahan dan tidak mengeksekusi pernyataan akhir `println!`. Saat Anda mencoba mengakses elemen menggunakan pengindeksan, Rust akan memeriksa apakah indeks yang Anda tentukan kurang dari panjang array. Jika indeks lebih besar dari atau sama dengan panjangnya, Rust akan panik. Pemeriksaan ini harus terjadi pada waktu runtime, terutama dalam kasus ini, karena kompiler tidak mungkin mengetahui nilai apa yang akan dimasukkan pengguna saat mereka menjalankan kode nanti.

Ini adalah contoh penerapan prinsip keamanan memori Rust. Dalam banyak bahasa tingkat rendah, pemeriksaan semacam ini tidak dilakukan, dan saat Anda memberikan indeks yang salah, memori yang tidak valid dapat diakses. Rust melindungi Anda dari kesalahan semacam ini dengan segera keluar alih-alih mengizinkan akses memori dan melanjutkan. Bab 9 membahas lebih lanjut tentang penanganan kesalahan Rust dan bagaimana Anda dapat menulis kode aman yang dapat dibaca yang tidak membuat panik atau mengizinkan akses memori yang tidak valid.

[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[twos-complement]: https://en.wikipedia.org/wiki/Two%27s_complement
[control-flow]: ch03-05-control-flow.html#control-flow
[strings]: ch08-02-strings.html#storing-utf-8-encoded-text-with-strings
[stack-and-heap]: ch04-01-what-is-ownership.html#the-stack-and-the-heap
[vectors]: ch08-01-vectors.html
[unrecoverable-errors-with-panic]: ch09-01-unrecoverable-errors-with-panic.html
[appendix_b]: appendix-02-operators.md

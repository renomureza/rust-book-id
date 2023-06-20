## Aliran Kontrol

Kemampuan untuk menjalankan beberapa kode tergantung pada apakah suatu kondisi `true` dan untuk menjalankan beberapa kode berulang kali saat kondisi adalah `true` blok bangunan dasar di sebagian besar bahasa pemrograman. Konstruksi paling umum yang memungkinkan Anda mengontrol aliran eksekusi kode Rust adalah ekspresi `if` dan loop.

### Ekspresi `if`

Ekspresi `if` memungkinkan Anda untuk mencabangkan kode Anda tergantung pada kondisi. Anda memberikan kondisi dan kemudian menyatakan, “Jika kondisi ini terpenuhi, jalankan blok kode ini. Jika syaratnya tidak terpenuhi, jangan jalankan blok kode ini.”

Buat proyek baru bernama _branches_ di direktori _projects_ Anda untuk menjelajahi ekspresi `if`. Di file _src/main.rs_, masukkan yang berikut ini:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-26-if-true/src/main.rs}}
```

Semua ekspresi `if` dimulai dengan kata kunci `if`, diikuti dengan kondisi. Dalam hal ini, kondisi memeriksa apakah variabel `number` memiliki nilai kurang dari `5` atau tidak. Kami menempatkan blok kode untuk dieksekusi jika kondisi tepat `true` setelah kondisi di dalam kurung kurawal. Blok kode yang terkait dengan kondisi dalam ekspresi terkadang `if` disebut lengan, seperti lengan dalam ekspresi `match` yang telah kita bahas di bagian [“Membandingkan Tebakan dengan Angka Rahasia”][comparing-the-guess-to-the-secret-number] di Bab 2.

Opsional, kami juga dapat menyertakan ekspresi `else`, yang kami pilih untuk dilakukan di sini, untuk memberikan program blok kode alternatif untuk dieksekusi jika kondisi dievaluasi menjadi `false`. Jika Anda tidak memberikan ekspresi `else` dan kondisinya adalah `false`, program hanya akan melewatkan blok `if` dan melanjutkan ke bit kode berikutnya.

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-26-if-true/output.txt}}
```

Mari kita coba mengubah nilai `number` menjadi nilai yang membuat kondisi `false` untuk melihat apa yang terjadi:

```rust,ignore
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-27-if-false/src/main.rs:here}}
```

Jalankan program lagi, dan lihat hasilnya:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-27-if-false/output.txt}}
```

Perlu diperhatikan juga bahwa kondisi dalam kode ini _harus_ berupa `bool`. Jika kondisinya bukan `bool`, kita akan mendapatkan error. Misalnya, coba jalankan kode berikut:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/src/main.rs}}
```

Kondisi `if` dievaluasi ke nilai `3` saat ini, dan Rust melontarkan kesalahan:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/output.txt}}
```

Kesalahan menunjukkan bahwa Rust mengharapkan `bool` tetapi mendapat bilangan bulat. Tidak seperti bahasa Ruby dan JavaScript, Rust tidak akan secara otomatis mencoba mengubah tipe non-Boolean menjadi Boolean. Anda harus eksplisit dan selalu menyediakan `if` dengan Boolean sebagai syaratnya. Jika kita ingin blok kode `if` berjalan hanya ketika sebuah angka tidak sama dengan `0`, misalnya, kita dapat mengubah ekspresi `if` menjadi berikut:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-29-if-not-equal-0/src/main.rs}}
```

Menjalankan kode ini akan mencetak `number was something other than zero`.

#### Menangani Berbagai Kondisi dengan `else if`

Anda dapat menggunakan beberapa kondisi dengan menggabungkan `if` dan `else` dalam sebuah ekspresi `else if`. Misalnya:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-30-else-if/src/main.rs}}
```

Program ini memiliki empat kemungkinan jalur yang dapat diambil. Setelah menjalankannya, Anda akan melihat output berikut:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-30-else-if/output.txt}}
```

Saat program ini dijalankan, program ini memeriksa setiap ekspresi `if` secara bergiliran dan mengeksekusi badan pertama yang kondisinya dievaluasi menjadi `true`. Perhatikan bahwa meskipun 6 habis dibagi 2, kita tidak melihat output `number is divisible by 2`, juga tidak melihat teks `number is not divisible by 4, 3, or 2` dari blok `else`. Itu karena Rust hanya mengeksekusi blok untuk kondisi `true` pertama, dan setelah menemukannya, ia bahkan tidak memeriksa sisanya.

Menggunakan terlalu banyak ekspresi `else if` dapat mengacaukan kode Anda, jadi jika Anda memiliki lebih dari satu, Anda mungkin ingin memperbaiki kode Anda. Bab 6 menjelaskan konstruksi percabangan Rust yang kuat yang disebut `match` untuk kasus ini.

#### Menggunakan `if` dalam Pernyataan `let`

Karena `if` adalah ekspresi, kita dapat menggunakannya di sisi kanan pernyataan `let` untuk menetapkan hasil ke variabel, seperti pada Daftar 3-2.

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-02/src/main.rs}}
```

<span class="caption">Daftar 3-2: Menugaskan hasil ekspresi `if` ke variabel</span>

Variabel `number` akan terikat pada nilai sesuai hasil ekspresi `if`. Jalankan kode ini untuk melihat apa yang terjadi:

```console
{{#include ../../listings/ch03-common-programming-concepts/listing-03-02/output.txt}}
```

Ingatlah bahwa blok kode mengevaluasi ekspresi terakhir di dalamnya, dan angka itu sendiri juga merupakan ekspresi. Dalam hal ini, nilai seluruh ekspresi `if` bergantung pada blok kode mana yang dieksekusi. Artinya nilai-nilai yang berpotensi dihasilkan dari masing-masing lengan `if` harus bertipe sama; pada Daftar 3-2, hasil lengan `if` dan `else` adalah `i32` bilangan bulat. Jika tipenya tidak cocok, seperti contoh berikut, kita akan mendapatkan kesalahan:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/src/main.rs}}
```

Saat kami mencoba mengkompilasi kode ini, kami akan mendapatkan kesalahan. Lengan `if` and `else` memiliki tipe nilai yang tidak kompatibel, dan Rust menunjukkan dengan tepat di mana menemukan masalah dalam program:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/output.txt}}
```

Ekspresi di blok `if` dievaluasi ke integer, dan ekspresi di blok `else` dievaluasi ke string. Ini tidak akan berhasil karena variabel harus memiliki satu tipe, dan Rust perlu mengetahui pada waktu kompilasi tipe variabel `number` tersebut, secara definitif. Mengetahui tipe `number` memungkinkan kompiler memverifikasi tipe valid di mana pun kami menggunakan `number`. Rust tidak akan dapat melakukan itu jika tipe dari `number` hanya ditentukan pada saat runtime; kompiler akan lebih kompleks dan akan membuat lebih sedikit jaminan tentang kode jika harus melacak beberapa tipe hipotetis untuk variabel apa pun.

### Pengulangan dengan Loop

Seringkali berguna untuk mengeksekusi blok kode lebih dari sekali. Untuk tugas ini, Rust menyediakan beberapa loop, yang akan dijalankan melalui kode di dalam loop body sampai akhir dan kemudian segera mulai kembali dari awal. Untuk bereksperimen dengan perulangan, mari buat proyek baru bernama _loops_.

Rust memiliki tiga jenis loop: `loop`, `while`, dan `for`. Mari kita coba masing-masing.

#### Mengulang Kode dengan `loop`

Kata kunci `loop` memberi tahu Rust untuk mengeksekusi blok kode berulang kali selamanya atau sampai Anda secara eksplisit menyuruhnya berhenti.

Sebagai contoh, ubah file _src/main.rs_ di direktori _loops_ Anda menjadi seperti ini:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-32-loop/src/main.rs}}
```

Saat kita menjalankan program ini, kita akan melihat `again!` dicetak terus menerus sampai kita menghentikan program secara manual. Sebagian besar terminal mendukung pintasan keyboard <span class="keystroke">ctrl-c</span> untuk menginterupsi program yang macet terus-menerus. Cobalah:

<!-- manual-regeneration
cd listings/ch03-common-programming-concepts/no-listing-32-loop
cargo run
CTRL-C
-->

```console
$ cargo run
   Compiling loops v0.1.0 (file:///projects/loops)
    Finished dev [unoptimized + debuginfo] target(s) in 0.29s
     Running `target/debug/loops`
again!
again!
again!
again!
^Cagain!
```

Simbol `^C` mewakili tempat Anda menekan <span class="keystroke">ctrl-c</span>. Anda mungkin atau mungkin tidak melihat kata `again!` yang dicetak setelah `^C`, tergantung di mana kode berada di loop saat menerima sinyal interupsi.

Untungnya, Rust juga menyediakan cara untuk keluar dari loop menggunakan kode. Anda dapat menempatkan kata kunci `break` di dalam loop untuk memberi tahu program kapan harus berhenti menjalankan loop. Ingatlah bahwa kita melakukan ini dalam permainan tebak-tebakan di bagian “Berhenti Setelah Menebak dengan Benar” [“Quitting After a Correct Guess”][quitting-after-a-correct-guess] pada Bab 2 untuk keluar dari program saat pengguna memenangkan permainan dengan menebak angka yang benar.

Kami juga menggunakan `continue` dalam permainan tebak-tebakan, yang dalam satu loop memberi tahu program untuk melewati kode yang tersisa dalam iterasi loop ini dan melanjutkan ke iterasi berikutnya.

#### Mengembalikan Nilai dari Loop

Salah satu kegunaan `loop` adalah mencoba kembali operasi yang Anda tahu mungkin gagal, seperti memeriksa apakah _thread_ telah menyelesaikan tugasnya. Anda mungkin juga perlu meneruskan hasil operasi itu keluar dari loop ke seluruh kode Anda. Untuk melakukan ini, Anda bisa menambahkan nilai yang ingin Anda kembalikan setelah ekspresi `break` yang Anda gunakan untuk menghentikan perulangan; nilai itu akan dikembalikan dari loop sehingga Anda dapat menggunakannya, seperti yang ditunjukkan di sini:

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-33-return-value-from-loop/src/main.rs}}
```

Sebelum loop, kami mendeklarasikan variabel bernama `counter` dan menginisialisasi ke `0`. Kemudian kami mendeklarasikan variabel bernama `result` untuk menampung nilai yang dikembalikan dari loop. Pada setiap iterasi loop, kita menambahkan `1` variabel counter, lalu memeriksa apakah `counter` sama dengan `10`. Saat itu, kami menggunakan kata kunci `break` dengan nilai `counter * 2`. Setelah perulangan, kita menggunakan titik koma untuk mengakhiri pernyataan yang menetapkan nilai ke `result`. Terakhir, kami mencetak nilai dalam `result`, yang dalam hal ini adalah `20`.

#### Label Loop untuk Disambiguasi Antara Beberapa Loop

Jika Anda memiliki loop di dalam loop, `break` dan `continue` diterapkan ke loop terdalam pada saat itu. Secara opsional, Anda dapat menentukan _label loop_ pada loop yang kemudian dapat Anda gunakan dengan `break` atau `continue` untuk menentukan bahwa kata kunci tersebut berlaku untuk loop berlabel, bukan loop terdalam. Label loop harus dimulai dengan kutip tunggal. Berikut adalah contoh dengan dua loop bersarang:

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-32-5-loop-labels/src/main.rs}}
```

Loop luar memiliki label `'counting_up`, dan akan menghitung dari 0 hingga 2. Loop dalam tanpa label menghitung mundur dari 10 hingga 9. `break` pertama yang tidak menentukan label hanya akan keluar dari loop di dalam. Pernyataan `break 'counting_up;` akan keluar dari loop luar. Kode ini mencetak:

```console
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-32-5-loop-labels/output.txt}}
```

#### Loop Bersyarat dengan `while`

Suatu program seringkali perlu mengevaluasi suatu kondisi dalam satu loop. Saat kondisinya `true`, loop berjalan. Ketika kondisi berhenti menjadi `true`, program memanggil `break`, menghentikan perulangan. Dimungkinkan untuk menerapkan perilaku seperti ini menggunakan kombinasi `loop`, `if`, `else`, dan `break`; Anda dapat mencobanya sekarang dalam sebuah program, jika Anda mau. Namun, pola ini sangat umum sehingga Rust memiliki konstruksi bahasa bawaan untuknya, yang disebut loop `while`. Dalam Daftar 3-3, kami menggunakan `while` untuk mengulang program tiga kali, menghitung mundur setiap iterasi, dan kemudian, setelah pengulangan, cetak pesan dan keluar.

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-03/src/main.rs}}
```

<span class="caption">Daftar 3-3: Menggunakan perulangan `while` untuk menjalankan kode saat kondisi benar</span>

Konstruk ini menghilangkan banyak sarang yang diperlukan jika Anda menggunakan `loop`, `if`, `else`, dan `break`, dan lebih jelas. Saat kondisi bernilai `true`, kode berjalan; jika tidak, itu keluar dari loop.

#### Pengulangan melalui Koleksi dengan `for`

Anda dapat memilih untuk menggunakan konstruk `while` untuk mengulang elemen koleksi, seperti array. Sebagai contoh, loop pada Daftar 3-4 mencetak setiap elemen dalam array `a`.

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-04/src/main.rs}}
```

<span class="caption">Daftar 3-4: Mengulang setiap elemen koleksi menggunakan loop `while`</span>

Di sini, kode dihitung melalui elemen-elemen dalam array. Ini dimulai pada index `0`, dan kemudian berulang hingga mencapai indeks terakhir dalam array (yaitu, ketika `index < 5` tidak lagi `true`). Menjalankan kode ini akan mencetak setiap elemen dalam array:

```console
{{#include ../../listings/ch03-common-programming-concepts/listing-03-04/output.txt}}
```

Kelima nilai array muncul di terminal, seperti yang diharapkan. Meskipun `index` akan mencapai nilai `5` di beberapa titik, loop berhenti mengeksekusi sebelum mencoba mengambil nilai keenam dari array.

Namun, pendekatan ini rawan kesalahan; dapat menyebabkan program kita menjadi panik jika nilai indeks atau kondisi pengujian salah. Misalnya, jika Anda mengubah definisi array `a` menjadi empat elemen tetapi lupa memperbarui kondisinya menjadi `while index < 4`, kode akan panik. Ini juga lambat, karena kompiler menambahkan kode runtime untuk melakukan pemeriksaan kondisional apakah indeks berada dalam batas array pada setiap iterasi melalui loop.

Sebagai alternatif yang lebih ringkas, Anda bisa menggunakan perulangan `for` dan mengeksekusi beberapa kode untuk setiap item dalam koleksi. Loop `for` terlihat seperti kode pada Daftar 3-5.

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-05/src/main.rs}}
```

<span class="caption">Daftar 3-5: Mengulang setiap elemen koleksi menggunakan loop `for`</span>

Saat kita menjalankan kode ini, kita akan melihat output yang sama seperti pada Daftar 3-4. Lebih penting lagi, kami sekarang telah meningkatkan keamanan kode dan menghilangkan kemungkinan bug yang mungkin dihasilkan dari melampaui akhir array atau tidak cukup jauh dan kehilangan beberapa item.

Dengan menggunakan `for`, Anda tidak perlu mengingat untuk mengubah kode lain jika Anda mengubah jumlah nilai dalam array, seperti yang Anda lakukan dengan metode yang digunakan pada Daftar 3-4.

Keamanan dan keringkasan `for` menjadikannya konstruksi loop yang paling umum digunakan di Rust. Bahkan dalam situasi di mana Anda ingin menjalankan beberapa kode beberapa kali, seperti dalam contoh hitung mundur yang menggunakan perulangan `while` di Daftar 3-3, kebanyakan Rustacean akan menggunakan perulangan `for`. Cara melakukannya adalah dengan menggunakan `Range`, yang disediakan oleh pustaka standar, yang menghasilkan semua angka secara berurutan mulai dari satu angka dan diakhiri sebelum angka lainnya.

Berikut tampilan hitungan mundur menggunakan perulangan `for` dan metode lain yang belum kita bicarakan, `rev`, untuk membalikkan rentang:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-34-for-range/src/main.rs}}
```

Kode ini sedikit lebih bagus, bukan?

## Ringkasan

Anda berhasil! Ini adalah bab yang cukup besar: Anda belajar tentang variabel, tipe data skalar dan _compound_, fungsi, komentar, ekspresi `if`, dan loop! Untuk berlatih dengan konsep yang dibahas dalam bab ini, cobalah membuat program untuk melakukan hal berikut:

- Mengkonversi suhu antara Fahrenheit dan Celsius.
- Hasilkan angka Fibonacci ke-_n_ .
- Cetak lirik lagu Natal “The Twelve Days of Christmas”, memanfaatkan pengulangan dalam lagu tersebut.

Saat Anda siap untuk melanjutkan, kita akan berbicara tentang konsep di Rust yang tidak umum ada dalam bahasa pemrograman lain: kepemilikan (_ownership_).

[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#membandingkan-tebakan-dengan-angka-rahasia
[quitting-after-a-correct-guess]: ch02-00-guessing-game-tutorial.html#berhenti-setelah-tebakan-yang-benar

## Fungsi

Fungsi lazim dalam kode Rust. Anda telah melihat salah satu fungsi terpenting dalam bahasa: fungsi `main`, yang merupakan titik masuk dari banyak program. Anda juga telah melihat kata kunci `fn`, yang memungkinkan Anda mendeklarasikan fungsi baru.

Kode Rust menggunakan _snake case_ sebagai gaya konvensional untuk nama fungsi dan variabel, di mana semua huruf adalah huruf kecil dan garis bawah sebagai pemisah kata. Berikut adalah program yang berisi contoh definisi fungsi:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-16-functions/src/main.rs}}
```

Kami mendefinisikan fungsi di Rust dengan memasukkan `fn` diikuti dengan nama fungsi dan satu set tanda kurung. Tanda kurung kurawal memberi tahu kompiler tempat badan fungsi dimulai dan berakhir.

Kita dapat memanggil fungsi apa pun yang telah kita definisikan dengan memasukkan namanya diikuti dengan tanda kurung. Karena `another_function` didefinisikan dalam program, maka dapat dipanggil dari dalam fungsi `main`. Perhatikan bahwa kami mendefinisikan `another_function` setelah fungsi `main` dalam kode sumber; kita bisa mendefinisikannya sebelumnya juga. Rust tidak peduli di mana Anda mendefinisikan fungsi Anda, hanya saja mereka didefinisikan di suatu tempat dalam lingkup yang dapat dilihat oleh pemanggil.

Mari kita mulai proyek biner baru bernama _functions_ untuk menjelajahi fungsi lebih lanjut. Tempatkan contoh `another_function` di _src/main.rs_ dan jalankan. Anda akan melihat output berikut:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-16-functions/output.txt}}
```

Baris dijalankan sesuai urutan kemunculannya dalam fungsi `main`. Pertama, pesan “Hello, world!” dicetak, lalu `another_function` dipanggil dan pesannya dicetak.

### Parameter

Kita dapat mendefinisikan fungsi untuk memiliki _parameter_, yang merupakan variabel khusus yang merupakan bagian dari tanda tangan fungsi. Ketika suatu fungsi memiliki parameter, Anda dapat memberikannya nilai konkret untuk parameter tersebut. Secara teknis, nilai konkret disebut _argumen_, tetapi dalam percakapan biasa, orang cenderung menggunakan kata _parameter_ dan _argumen_ secara bergantian untuk variabel dalam definisi fungsi atau nilai konkret yang diteruskan saat Anda memanggil suatu fungsi.

Dalam versi `another_function` ini kami menambahkan parameter:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-17-functions-with-parameters/src/main.rs}}
```

Coba jalankan program ini; Anda harus mendapatkan output berikut:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-17-functions-with-parameters/output.txt}}
```

Deklarasi `another_function` memiliki satu parameter bernama `x`. Tipe dari `x` ditentukan sebagai `i32`. Saat kita meneruskan `5` ke `another_function`, makro `println!` menempatkan `5` dimana pasangan kurung kurawal yang berisi `x` sebagai format string.

Dalam tanda tangan fungsi, Anda _harus_ mendeklarasikan tipe setiap parameter. Ini adalah keputusan yang disengaja dalam desain Rust: membutuhkan anotasi tipe dalam definisi fungsi berarti kompiler hampir tidak pernah membutuhkan Anda untuk menggunakannya di tempat lain dalam kode untuk mengetahui tipe apa yang Anda maksud. Kompiler juga dapat memberikan pesan kesalahan yang lebih bermanfaat jika ia mengetahui apa tipe yang diharapkan fungsi.

Saat mendefinisikan beberapa parameter, pisahkan deklarasi parameter dengan koma, seperti ini:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-18-functions-with-multiple-parameters/src/main.rs}}
```

Contoh ini membuat fungsi bernama `print_labeled_measurement` dengan dua parameter. Parameter pertama bernama `value` dan merupakan `i32`. Yang kedua bernama `unit_label` dan bertipe `char`. Fungsi tersebut kemudian mencetak teks yang berisi `value` dan `unit_label`.

Mari kita coba jalankan kode ini. Ganti program yang saat ini ada di file _src/main.rs_ proyek _functions_ Anda dengan contoh sebelumnya dan jalankan menggunakan: `cargo run`

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-18-functions-with-multiple-parameters/output.txt}}
```

Karena kita memanggil fungsi dengan `5` sebagai nilai untuk `value` dan `'h'` sebagai nilai untuk `unit_label`, keluaran program berisi nilai-nilai tersebut.

### Pernyataan dan Ekspresi

Badan fungsi terdiri dari serangkaian pernyataan (_statement_) yang secara opsional diakhiri dengan ekspresi. Sejauh ini, fungsi yang telah kita bahas belum menyertakan ekspresi akhir, tetapi Anda telah melihat ekspresi sebagai bagian dari pernyataan. Karena Rust adalah bahasa berbasis ekspresi (_expression-based_), ini adalah perbedaan penting untuk dipahami. Bahasa lain tidak memiliki perbedaan yang sama, jadi mari kita lihat apa itu pernyataan dan ekspresi dan bagaimana perbedaannya memengaruhi tubuh fungsi.

- **Pernyataan** adalah instruksi yang melakukan beberapa tindakan dan tidak mengembalikan nilai.
- **Ekspresi** mengevaluasi ke nilai yang dihasilkan. Mari kita lihat beberapa contoh.

Kami sebenarnya sudah menggunakan pernyataan dan ekspresi. Membuat variabel dan memberikan nilai padanya dengan kata kunci `let` adalah pernyataan. Dalam Daftar 3-1, `let y = 6;` adalah sebuah pernyataan.

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/listing-03-01/src/main.rs}}
```

<span class="caption">Daftar 3-1: Deklarasi fungsi `main` berisi satu pernyataan</span>

Definisi fungsi juga merupakan pernyataan; seluruh contoh sebelumnya adalah pernyataan itu sendiri.

Pernyataan tidak mengembalikan nilai. Oleh karena itu, Anda tidak dapat menetapkan pernyataan `let` ke variabel lain, seperti yang coba dilakukan oleh kode berikut; Anda akan mendapatkan kesalahan:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-19-statements-vs-expressions/src/main.rs}}
```

Saat Anda menjalankan program ini, kesalahan yang akan Anda dapatkan terlihat seperti ini:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-19-statements-vs-expressions/output.txt}}
```

Pernyataan itu `let y = 6` tidak mengembalikan nilai, jadi tidak ada yang harus diikat ke `x`. Ini berbeda dengan yang terjadi di bahasa lain, seperti C dan Ruby, di mana _assignment_ mengembalikan nilai _assignment_. Dalam bahasa tersebut, Anda dapat menulis `x = y = 6` dan memiliki keduanya `x` dan `y` yang memiliki nilai `6`; itu tidak terjadi di Rust.

Ekspresi mengevaluasi nilai dan membuat sebagian besar sisa kode yang akan Anda tulis di Rust. Pertimbangkan operasi matematika, seperti `5 + 6`, yang merupakan ekspresi yang mengevaluasi nilai `11`. Ekspresi dapat menjadi bagian dari pernyataan: pada Daftar 3-1, `6` dalam pernyataan `let y = 6;` adalah ekspresi yang mengevaluasi nilai `6`. Memanggil fungsi adalah ekspresi. Memanggil makro adalah ekspresi. Sebuah blok cakupan baru yang dibuat dengan kurung kurawal adalah sebuah ekspresi, misalnya:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-20-blocks-are-expressions/src/main.rs}}
```

Ini ekspresi:

```rust,ignore
{
    let x = 3;
    x + 1
}
```

adalah blok yang, dalam hal ini, bernilai `4`. Nilai itu terikat ke `y` sebagai bagian dari pernyataan `let`. Perhatikan bahwa baris `x + 1` tidak memiliki titik koma di bagian akhir, yang tidak seperti kebanyakan baris yang Anda lihat sejauh ini. Ekspresi tidak menyertakan titik koma akhir. Jika Anda menambahkan titik koma di akhir ekspresi, Anda mengubahnya menjadi pernyataan, dan kemudian tidak akan mengembalikan nilai. Ingatlah hal ini saat Anda menjelajahi fungsi mengembalikan nilai dan ekspresi selanjutnya.

### Fungsi dengan Nilai Pengembalian

Fungsi dapat mengembalikan nilai ke kode yang memanggilnya. Kami tidak memberi nama nilai pengembalian, tetapi kami harus mendeklarasikan tipenya setelah tanda panah (`->`). Di Rust, nilai pengembalian fungsi identik dengan nilai ekspresi akhir di blok badan fungsi. Anda bisa mengembalikan nilai lebih awal dari suatu fungsi dengan menggunakan kata kunci `return` dan menentukan nilainya, tetapi sebagian besar fungsi mengembalikan ekspresi terakhir secara implisit. Berikut adalah contoh fungsi yang mengembalikan nilai:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-21-function-return-values/src/main.rs}}
```

Tidak ada pemanggilan fungsi, makro, atau bahkan pernyataan `let` dalam fungsi `five` — hanya angka `5` itu sendiri. Itu fungsi yang sangat valid di Rust. Perhatikan bahwa tipe pengembalian fungsi juga ditentukan, sebagai `-> i32`. Coba jalankan kode ini; keluaran akan terlihat seperti ini:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-21-function-return-values/output.txt}}
```

`5` adalah nilai pengembalian fungsi `five`, itulah sebabnya tipe pengembaliannya adalah `i32`. Mari kita periksa ini lebih detail. Ada dua bit penting: pertama, baris `let x = five();` menunjukkan bahwa kita menggunakan nilai kembalian dari suatu fungsi untuk menginisialisasi variabel. Karena fungsi `five` mengembalikan `5`, baris itu sama dengan yang berikut:

```rust
let x = 5;
```

Kedua, fungsi `five` tidak memiliki parameter dan menentukan jenis nilai yang dikembalikan, tetapi isi fungsi adalah 5 sendiri tanpa titik koma karena ini adalah ekspresi yang nilainya ingin kita kembalikan.

Mari kita lihat contoh lain:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-22-function-parameter-and-return/src/main.rs}}
```

Menjalankan kode ini akan mencetak `The value of x is: 6`. Namun jika kita menempatkan titik koma di akhir baris yang berisi `x + 1`, mengubahnya dari ekspresi menjadi pernyataan, kita akan mendapatkan kesalahan:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-23-statements-dont-return-values/src/main.rs}}
```

Mengkompilasi kode ini menghasilkan kesalahan, sebagai berikut:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-23-statements-dont-return-values/output.txt}}
```

Pesan kesalahan utama, `mismatched types`, mengungkapkan masalah inti dari kode ini. Definisi fungsi `plus_one` mengatakan bahwa itu akan mengembalikan `i32`, tetapi pernyataan tidak mengevaluasi ke nilai, yang dinyatakan oleh `()`, tipe unit. Oleh karena itu, tidak ada yang dikembalikan, yang bertentangan dengan definisi fungsi dan menghasilkan kesalahan. Dalam keluaran ini, Rust memberikan pesan untuk membantu memperbaiki masalah ini: ia menyarankan untuk menghapus titik koma, yang akan memperbaiki kesalahan.

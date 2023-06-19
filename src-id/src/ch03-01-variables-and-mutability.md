## Variabel dan Mutabilitas

Seperti yang disebutkan di bagian [“Menyimpan Nilai dengan Variabel][storing-values-with-variables], secara default, variabel tidak dapat diubah. Ini adalah salah satu dari banyak dorongan yang diberikan Rust kepada Anda untuk menulis kode dengan cara yang memanfaatkan keamanan dan konkurensi mudah yang ditawarkan Rust. Namun, Anda masih memiliki opsi untuk membuat variabel Anda bisa berubah. Mari jelajahi bagaimana dan mengapa Rust mendorong Anda untuk menyukai kekekalan (_immutability_) dan mengapa terkadang Anda ingin memilih keluar.

Ketika sebuah variabel tidak dapat diubah, setelah sebuah nilai terikat pada sebuah nama, Anda tidak dapat mengubah nilai tersebut. Untuk mengilustrasikannya, buat proyek baru bernama _variables_ di direktori _projects_ Anda dengan menggunakan `cargo new variables`.

Kemudian, di direktori _variables_ Anda, buka _src/main.rs_ dan ganti kodenya dengan kode berikut, yang belum dapat dikompilasi:

<span class="filename">Nama file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/src/main.rs}}
```

Simpan dan jalankan program menggunakan `cargo run`. Anda akan menerima pesan kesalahan terkait kesalahan kekekalan, seperti yang ditampilkan dalam output ini:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/output.txt}}
```

Contoh ini menunjukkan bagaimana kompiler membantu Anda menemukan kesalahan dalam program Anda. Kesalahan kompiler bisa membuat frustasi, tetapi sebenarnya itu berarti program Anda belum melakukan apa yang Anda inginkan dengan aman; itu _tidak_ berarti bahwa Anda bukan programmer yang baik! Rustacean berpengalaman masih mendapatkan kesalahan kompiler.

Anda menerima pesan kesalahan `` cannot assign twice to immutable variable `x` `` karena mencoba menetapkan nilai kedua ke variabel `x` yang tidak dapat diubah.

Penting bagi kita untuk mendapatkan kesalahan pada waktu kompilasi saat kita mencoba mengubah nilai yang ditetapkan sebagai tidak dapat diubah, karena situasi ini dapat menyebabkan bug. Jika satu bagian dari kode kita beroperasi dengan asumsi bahwa suatu nilai tidak akan pernah berubah dan bagian lain dari kode kita mengubah nilai itu, kemungkinan bagian pertama dari kode tersebut tidak akan melakukan apa yang seharusnya dilakukan. Penyebab bug semacam ini bisa jadi sulit untuk dilacak setelah faktanya, terutama ketika potongan kode kedua _kadang-kadang_ hanya mengubah nilainya. Kompiler Rust menjamin bahwa ketika Anda menyatakan bahwa suatu nilai tidak akan berubah, itu benar-benar tidak akan berubah, jadi Anda tidak perlu melacaknya sendiri. Dengan demikian, kode Anda lebih mudah untuk dipikirkan.

Tapi mutabilitas bisa sangat berguna, dan bisa membuat kode lebih nyaman untuk ditulis. Meskipun variabel tidak dapat diubah secara default, Anda dapat membuatnya dapat diubah dengan menambahkan `mut` di depan nama variabel seperti yang Anda lakukan di [Bab 2][storing-values-with-variables]. Menambahkan `mut` juga menyampaikan maksud kepada pembaca kode di masa mendatang dengan menunjukkan bahwa bagian lain dari kode akan mengubah nilai variabel ini.

Misalnya, mari kita ubah _src/main.rs_ menjadi berikut ini:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/src/main.rs}}
```

Saat kita menjalankan program sekarang, kita mendapatkan ini:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/output.txt}}
```

Kami diizinkan untuk mengubah nilai yang terikat ke `x` dari `5` ke `6` saat `mut` digunakan. Pada akhirnya, memutuskan apakah akan menggunakan mutabilitas atau tidak terserah Anda dan bergantung pada apa yang menurut Anda paling jelas dalam situasi tertentu.

### Konstanta

Seperti variabel yang tidak dapat diubah, konstanta adalah nilai yang terikat pada nama dan tidak boleh diubah, tetapi ada beberapa perbedaan antara konstanta dan variabel.

Pertama, Anda tidak diizinkan menggunakan `mut` dalam konstanta. Konstanta tidak hanya tidak dapat diubah secara default — konstanta selalu tidak dapat diubah. Anda mendeklarasikan konstanta menggunakan kata kunci `const` alih-alih `let`, dan jenis nilainya _harus_ dianotasi. Kita akan membahas tipe dan anotasi tipe di bagian berikutnya, [Tipe Data][data-types], jadi jangan khawatir tentang detailnya sekarang. Ketahuilah bahwa Anda harus selalu membubuhi keterangan tipenya.

Konstanta dapat dideklarasikan dalam lingkup apa pun, termasuk lingkup global, yang membuatnya berguna untuk nilai yang perlu diketahui oleh banyak bagian kode.

Perbedaan terakhir adalah konstanta dapat disetel hanya ke ekspresi konstanta, bukan hasil dari nilai yang hanya dapat dihitung saat runtime.

Berikut adalah contoh deklarasi konstanta:

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

Nama konstanta tersebut adalah `THREE_HOURS_IN_SECONDS` dan nilainya ditetapkan sebagai hasil perkalian 60 (jumlah detik dalam satu menit) dengan 60 (jumlah menit dalam satu jam) dengan 3 (jumlah jam yang ingin kita hitung dalam program ini). Konvensi penamaan Rust untuk konstanta adalah menggunakan semua huruf besar dengan garis bawah di antara kata-kata. Kompiler dapat mengevaluasi serangkaian operasi terbatas pada waktu kompilasi, yang memungkinkan kita memilih untuk menuliskan nilai ini dengan cara yang lebih mudah dipahami dan diverifikasi, daripada menyetel konstanta ini ke nilai 10,800. Lihat bagian [Rust Reference tentang evaluasi konstanta][const-eval] untuk informasi lebih lanjut tentang operasi apa yang dapat digunakan saat mendeklarasikan konstanta.

Konstanta berlaku sepanjang waktu program berjalan, dalam lingkup di mana mereka dideklarasikan. Properti ini membuat konstanta berguna untuk nilai dalam domain aplikasi Anda yang mungkin perlu diketahui oleh beberapa bagian program, seperti jumlah poin maksimum yang boleh diperoleh pemain mana pun dari suatu game, atau kecepatan cahaya.

Memberi nama nilai _hardcode_ yang digunakan di seluruh program Anda sebagai konstanta berguna dalam menyampaikan arti nilai tersebut kepada pengelola kode di masa mendatang. Ini juga membantu untuk memiliki hanya satu tempat dalam kode Anda yang perlu Anda ubah jika nilai _hardcode_ perlu diperbarui di masa mendatang.

### Shadowing (Pembayangan)

Seperti yang Anda lihat di tutorial permainan tebak-tebakan di [Bab 2][comparing-the-guess-to-the-secret-number], Anda bisa mendeklarasikan variabel baru dengan nama yang sama dengan variabel sebelumnya. Rustaceans mengatakan bahwa variabel pertama dibayangi oleh yang kedua, yang berarti bahwa variabel kedua adalah apa yang akan dilihat oleh kompiler ketika Anda menggunakan nama variabel. Akibatnya, variabel kedua membayangi yang pertama, menggunakan nama variabel apa pun untuk dirinya sendiri sampai variabel itu sendiri dibayangi atau cakupannya berakhir. Kita bisa membayangi variabel dengan menggunakan nama variabel yang sama dan mengulangi penggunaan kata kunci `let` sebagai berikut:

<span class="filename">Nama file: src/main.rs</span>

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-03-shadowing/src/main.rs}}
```

Program ini pertama mengikat `x` ke nilai `5`. Kemudian ia membuat variabel baru `x` dengan mengulang `let x =`, mengambil nilai asli dan menambahkan `1` sehingga nilai `x` menjadi `6`. Kemudian, dalam lingkup baru yang dibuat dengan kurung kurawal, pernyataan `let` ketiga juga membayangi `x` dan membuat variabel baru, mengalikan nilai sebelumnya dengan `2` membuat `x` memiliki nilai `12`. Ketika ruang lingkup itu berakhir, bayangan didalam berakhir dan `x` kembali menjadi `6`. Ketika kami menjalankan program ini, itu akan menampilkan yang berikut:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-03-shadowing/output.txt}}
```

Shadowing berbeda dengan menandai variabel dengan `mut` karena kita akan mendapatkan kesalahan waktu kompilasi jika kita tidak sengaja mencoba menetapkan ulang ke variabel ini tanpa menggunakan kata kunci `let`. Dengan menggunakan `let`, kita dapat melakukan beberapa transformasi pada suatu nilai tetapi memiliki variabel yang tidak dapat diubah setelah transformasi tersebut selesai.

Perbedaan lain antara `mut` dan shadowing adalah karena kita membuat variabel baru secara efektif saat menggunakan kata kunci `let`, kita dapat mengubah tipe nilai tetapi menggunakan kembali nama yang sama. Misalnya, program kami meminta pengguna untuk menunjukkan berapa banyak spasi yang mereka inginkan di antara beberapa teks dengan memasukkan karakter spasi, lalu kami ingin menyimpan masukan itu sebagai angka:

```rust
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-04-shadowing-can-change-types/src/main.rs:here}}
```

Variabel `spaces` pertama adalah tipe string dan variabel `spaces` kedua adalah tipe angka. Shadowing dengan demikian menghindarkan kita dari keharusan memunculkan nama yang berbeda, seperti `spaces_str` dan `spaces_num`; sebagai gantinya, kita dapat menggunakan kembali nama `spaces` yang lebih sederhana. Namun, jika kami mencoba menggunakan `mut` untuk ini, seperti yang ditunjukkan di sini, kami akan mendapatkan kesalahan waktu kompilasi:

```rust,ignore,does_not_compile
{{#rustdoc_include ../../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/src/main.rs:here}}
```

Kesalahan mengatakan kami tidak diizinkan untuk mengubah tipe variabel:

```console
{{#include ../../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/output.txt}}
```

Sekarang setelah kita menjelajahi cara kerja variabel, mari kita lihat lebih banyak tipe data yang dapat mereka miliki.

[comparing-the-guess-to-the-secret-number]: ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[data-types]: ch03-02-data-types.html#data-types
[storing-values-with-variables]: ch02-00-guessing-game-tutorial.html#storing-values-with-variables
[const-eval]: ../reference/const_eval.html

## Hello, World!

Sekarang setelah Anda menginstal Rust, saatnya menulis program Rust pertama Anda. Sudah menjadi kebiasaan saat mempelajari bahasa baru untuk menulis program kecil yang mencetak teks `Hello, world!` ke layar, jadi kita akan melakukan hal yang sama di sini!

> Catatan: Buku ini mengasumsikan keakraban dasar dengan baris perintah. Rust tidak membuat tuntutan khusus tentang pengeditan atau perkakas Anda atau di mana kode Anda berada, jadi jika Anda lebih suka menggunakan lingkungan pengembangan terintegrasi (IDE) daripada baris perintah, silakan gunakan IDE favorit Anda. Banyak IDE sekarang memiliki beberapa tingkat dukungan Rust; periksa dokumentasi IDE untuk detailnya. Tim Rust berfokus untuk mengaktifkan dukungan IDE yang hebat melalui `rust-analyzer`. Lihat [Lampiran D][devtools] untuk lebih jelasnya.

### Membuat Direktori Proyek

Anda akan mulai dengan membuat direktori untuk menyimpan kode Rust Anda. Tidak masalah bagi Rust di mana kode Anda berada, tetapi untuk latihan dan proyek dalam buku ini, kami menyarankan untuk membuat direktori _projects_ di direktori home Anda dan menyimpan semua proyek Anda di sana.

Buka terminal dan masukkan perintah berikut untuk membuat direktori _projects_ dan direktori untuk proyek "Hello, world!" dalam direktori _projects_.

Untuk Linux, macOS, dan PowerShell di Windows, masukkan ini:

```console
$ mkdir ~/projects
$ cd ~/projects
$ mkdir hello_world
$ cd hello_world
```

Untuk Windows CMD, masukkan ini:

```cmd
> mkdir "%USERPROFILE%\projects"
> cd /d "%USERPROFILE%\projects"
> mkdir hello_world
> cd hello_world
```

### Menulis dan Menjalankan Program Rust

Selanjutnya, buat file sumber baru dan beri nama _main.rs_. File Rust selalu diakhiri dengan ekstensi _.rs_. Jika Anda menggunakan lebih dari satu kata dalam nama file Anda, aturannya adalah menggunakan garis bawah untuk memisahkannya. Misalnya, gunakan _hello_world.rs_ daripada _helloworld.rs_.

Sekarang buka file _main.rs_ yang baru saja Anda buat dan masukkan kode di Listing 1-1.

<span class="filename">Nama File: main.rs</span>

```rust
fn main() {
    println!("Hello, world!");
}
```

<span class="caption">Daftar 1-1: Sebuah program yang mencetak `Hello, world!`</span>

Simpan file dan kembali ke jendela terminal Anda di direktori _~/projects/hello_world_. Di Linux atau macOS, masukkan perintah berikut untuk mengompilasi dan menjalankan file:

```console
$ rustc main.rs
$ ./main
Hello, world!
```

Di Windows, masukkan perintah `.\main.exe` alih-alih `./main`:

```powershell
> rustc main.rs
> .\main.exe
Hello, world!
```

Terlepas dari sistem operasi Anda, string `Hello, world!` harus dicetak ke terminal. Jika Anda tidak melihat keluaran ini, lihat kembali bagian [Pemecahan Masalah][troubleshooting] pada bagian Instalasi untuk mendapatkan bantuan.

Jika `Hello, world!` berhasil dicetak, selamat! Anda telah secara resmi menulis program Rust. Itu menjadikan Anda seorang _programmer_ Rust — selamat datang!

### Anatomi Program Rust

Mari kita ulas program “Hello, world!” secara rinci. Inilah bagian pertama dari teka-teki itu:

```rust
fn main() {

}
```

Baris-baris ini mendefinisikan sebuah fungsi bernama `main`. Fungsinya `main` istimewa: selalu menjadi kode pertama yang dijalankan di setiap program Rust yang dapat dieksekusi. Di sini, baris pertama mendeklarasikan sebuah fungsi bernama `main` yang tidak memiliki parameter dan tidak mengembalikan apa pun. Jika ada parameter, mereka akan masuk ke dalam tanda kurung `()`.

Tubuh fungsi dibungkus `{}`. Rust membutuhkan tanda kurung kurawal di sekeliling semua badan fungsi. Ini gaya yang bagus untuk menempatkan kurung kurawal pembuka pada baris yang sama dengan deklarasi fungsi, menambahkan satu spasi di antaranya.

> Catatan: Jika Anda ingin tetap menggunakan gaya standar di seluruh proyek Rust, Anda dapat menggunakan alat pemformat otomatis yang disebut `rustfmt` untuk memformat kode Anda dalam gaya tertentu (selengkapnya `rustfmt` di [Lampiran D][devtools]). Tim Rust telah menyertakan alat ini dengan distribusi Rust standar, seperti `rustc`, jadi alat ini harus sudah terpasang di komputer Anda!

Tubuh fungsi `main` berisi kode berikut:

```rust
    println!("Hello, world!");
```

Baris ini melakukan semua pekerjaan dalam program kecil ini: ia mencetak teks ke layar. Ada empat detail penting yang perlu diperhatikan di sini.

Pertama, gaya Rust adalah indentasi dengan empat spasi, bukan tab.

Kedua, panggilan `println!` makro Rust. Jika itu memanggil fungsi, itu akan ditulis sebagai `println` (tanpa `!`). Kita akan membahas makro Rust lebih detail di Bab 19. Untuk saat ini, Anda hanya perlu tahu bahwa menggunakan `!` memanggil makro alih-alih fungsi normal dan makro tidak selalu mengikuti aturan yang sama seperti fungsi.

Ketiga, Anda melihat string `"Hello, world!"`. Kami meneruskan string ini sebagai argumen ke `println!`, dan string tersebut dicetak ke layar.

Keempat, akhiri baris dengan titik koma (`;`), yang menandakan bahwa ekspresi ini telah berakhir dan ekspresi berikutnya siap untuk dimulai. Sebagian besar baris kode Rust diakhiri dengan titik koma.

### Kompilasi dan Menjalankan Adalah Langkah Terpisah

Anda baru saja menjalankan program yang baru dibuat, jadi mari kita periksa setiap langkah dalam prosesnya.

Sebelum menjalankan program Rust, Anda harus mengompilasinya menggunakan kompiler Rust dengan memasukkan perintah `rustc` dan memberikannya nama file sumber Anda, seperti ini:

```console
$ rustc main.rs
```

Jika Anda memiliki latar belakang C atau C++, Anda akan melihat bahwa ini mirip dengan `gcc` atau `clang`. Setelah kompilasi berhasil, Rust mengeluarkan biner yang dapat dieksekusi.

Di Linux, macOS, dan PowerShell di Windows, Anda dapat melihat _executable_ dengan memasukkan perintah `ls` di shell Anda:

```console
$ ls
main  main.rs
```

Di Linux dan macOS, Anda akan melihat dua file. Dengan PowerShell di Windows, Anda akan melihat tiga file yang sama dengan yang Anda lihat menggunakan CMD. Dengan CMD di Windows, Anda akan memasukkan yang berikut ini:

```cmd
> dir /B %= the /B option says to only show the file names =%
main.exe
main.pdb
main.rs
```

Ini menunjukkan file kode sumber dengan ekstensi _.rs_, file yang dapat dieksekusi (_main.exe_ di Windows, tetapi main di semua platform lain), dan saat menggunakan Windows, file yang berisi informasi debug dengan ekstensi _.pdb_. Dari sini, Anda menjalankan file main atau _main.exe_, seperti ini:

```console
$ ./main # or .\main.exe on Windows
```

Jika _main.rs_ Anda adalah "“Hello, world!" program, baris ini mencetak `Hello, world!` ke terminal Anda.

Jika Anda lebih terbiasa dengan bahasa dinamis, seperti Ruby, Python, atau JavaScript, Anda mungkin tidak terbiasa mengompilasi dan menjalankan program sebagai langkah terpisah. Rust adalah bahasa yang _ahead-of-time compiled_, artinya Anda dapat mengkompilasi program dan memberikan file yang dapat dieksekusi kepada orang lain, dan mereka dapat menjalankannya bahkan tanpa menginstal Rust. Jika Anda memberikan file _.rb_, _.py_, atau _.js_ kepada seseorang, mereka harus menginstal implementasi Ruby, Python, atau JavaScript (masing-masing). Namun dalam bahasa tersebut, Anda hanya memerlukan satu perintah untuk mengkompilasi dan menjalankan program Anda. Semuanya merupakan _trade-off_ dalam desain bahasa.

Mengkompilasi dengan `rustc` saja tidak apa-apa untuk program sederhana, tetapi seiring berkembangnya proyek Anda, Anda pasti ingin mengelola semua opsi dan membuatnya mudah untuk membagikan kode Anda. Selanjutnya, kami akan memperkenalkan alat Cargo, yang akan membantu Anda menulis program Rust di dunia nyata.

[troubleshooting]: ch01-01-installation.html#troubleshooting
[devtools]: appendix-04-useful-development-tools.md

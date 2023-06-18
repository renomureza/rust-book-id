## Installation

The first step is to install Rust. We’ll download Rust through `rustup`, a
command line tool for managing Rust versions and associated tools. You’ll need
an internet connection for the download.

Langkah pertama adalah menginstal Rust. Kami akan mengunduh Rust melalui `rustup`, alat baris perintah untuk mengelola versi Rust dan alat terkait. Anda memerlukan koneksi internet untuk mengunduh.

> Catatan: Jika Anda memilih untuk tidak menggunakan `rustup` karena alasan tertentu, Silakan lihat [halaman Metode Instalasi Rust Lainnya][otherinstall] untuk opsi lainnya.

Langkah-langkah berikut menginstal versi stabil terbaru dari kompiler Rust. Jaminan stabilitas Rust memastikan bahwa semua contoh dalam buku yang dikompilasi akan terus dikompilasi dengan versi Rust yang lebih baru. Outputnya mungkin sedikit berbeda antar versi karena Rust sering memperbaiki pesan kesalahan dan peringatan. Dengan kata lain, versi Rust yang lebih baru dan stabil yang Anda instal menggunakan langkah-langkah ini akan berfungsi seperti yang diharapkan dengan konten buku ini.

> ### Notasi Baris Perintah
>
> Di bab ini dan di seluruh buku ini, kami akan menunjukkan beberapa perintah yang digunakan di terminal. Baris yang harus Anda masukkan di terminal semuanya dimulai dengan `$`. Anda tidak perlu mengetikkan karakter `$`; itu _prompt_ baris perintah yang ditampilkan untuk menunjukkan awal dari setiap perintah. Baris yang tidak dimulai dengan `$` biasanya menampilkan keluaran dari perintah sebelumnya. Selain itu, contoh khusus PowerShell akan menggunakan `>` alih-alih `$`.

### Menginstal `rustup` di Linux atau macOS

Jika Anda menggunakan Linux atau macOS, buka terminal dan masukkan perintah berikut:

```console
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

Perintah tersebut mengunduh skrip dan memulai penginstalan alat `rustup`, yang menginstal Rust versi stabil terbaru. Anda mungkin dimintai kata sandi. Jika penginstalan berhasil, baris berikut akan muncul:

```text
Rust is installed now. Great!
```

Anda juga memerlukan _linker_, yaitu program yang digunakan Rust untuk menggabungkan hasil kompilasinya menjadi satu file. Kemungkinan Anda sudah memilikinya. Jika Anda mendapatkan kesalahan linker, Anda harus menginstal kompiler C, yang biasanya menyertakan linker. Kompiler C juga berguna karena beberapa paket Rust umum bergantung pada kode C dan memerlukan kompiler C.

Di macOS, Anda bisa mendapatkan kompiler C dengan menjalankan:

```console
$ xcode-select --install
```

Pengguna Linux umumnya harus menginstal GCC atau Clang, sesuai dokumentasi distribusinya. Misalnya, jika Anda menggunakan Ubuntu, Anda dapat menginstal paket `build-essential`.

### Menginstal `rustup` di Windows

Di Windows, buka [https://www.rust-lang.org/tools/install][install] dan ikuti petunjuk untuk menginstal Rust. Di beberapa titik dalam penginstalan, Anda akan menerima pesan yang menjelaskan bahwa Anda juga memerlukan alat build MSVC untuk Visual Studio 2013 atau lebih baru.

Untuk mendapatkan alat build, Anda harus menginstal [Visual Studio 2022][visualstudio]. Saat ditanya _workloads_ mana yang akan diinstal, sertakan:

- “Desktop Development with C++”
- Windows 10 atau 11 SDK
- Komponen paket bahasa Inggris, bersama dengan paket bahasa lainnya yang Anda pilih

Bagian selanjutnya dari buku ini menggunakan perintah yang bekerja di _cmd.exe_ dan PowerShell. Jika ada perbedaan tertentu, kami akan menjelaskan mana yang akan digunakan.

### Penyelesaian masalah

Untuk memeriksa apakah Anda telah menginstal Rust dengan benar, buka shell dan masukkan baris ini:

```console
$ rustc --version
```

Anda akan melihat nomor versi, hash komit, dan tanggal komit untuk versi stabil terbaru yang telah dirilis, dalam format berikut:

```text
rustc x.y.z (abcabcabc yyyy-mm-dd)
```

Jika Anda melihat informasi ini, Anda telah berhasil menginstal Rust! Jika Anda tidak melihat informasi ini, periksa apakah Rust ada di variabel `%PATH%` sistem Anda, menggunakan perintah berikut.

Di Windows CMD, gunakan:

```console
> echo %PATH%
```

Di PowerShell, gunakan:

```powershell
> echo $env:Path
```

Di Linux dan macOS, gunakan:

```console
$ echo $PATH
```

Jika semuanya benar dan Rust masih tidak berfungsi, ada beberapa tempat di mana Anda bisa mendapatkan bantuan. Cari tahu cara berhubungan dengan Rustacea lain (nama panggilan konyol yang kami sebut sendiri) di [halaman komunitas][community].

### Memperbarui dan Menghapus Instalasi

Setelah Rust diinstal melalui `rustup`, memperbarui ke versi yang baru dirilis menjadi mudah. Dari shell Anda, jalankan skrip pembaruan berikut:

```console
$ rustup update
```

Untuk menghapus Rust dan `rustup`, jalankan skrip uninstall berikut dari shell Anda:

```console
$ rustup self uninstall
```

### Dokumentasi Lokal

Penginstalan Rust juga menyertakan salinan dokumentasi lokal sehingga Anda dapat membacanya secara offline. Jalankan `rustup doc` untuk membuka dokumentasi lokal di browser Anda.

Setiap kali sebuah tipe atau fungsi disediakan oleh pustaka standar dan Anda tidak yakin apa fungsinya atau bagaimana menggunakannya, gunakan dokumentasi antarmuka pemrograman aplikasi (API) untuk mencari tahu!

[otherinstall]: https://forge.rust-lang.org/infra/other-installation-methods.html
[install]: https://www.rust-lang.org/tools/install
[visualstudio]: https://visualstudio.microsoft.com/downloads/
[community]: https://www.rust-lang.org/community

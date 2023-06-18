# Perkenalan

> Catatan: Edisi buku ini sama dengan [The Rust Programming Language][nsprust] yang tersedia dalam format cetak dan ebook dari [No Starch Press][nsp].

[nsprust]: https://nostarch.com/rust-programming-language-2nd-edition
[nsp]: https://nostarch.com/

Selamat datang di _The Rust Programming Language_, sebuah buku pengantar tentang Rust. Bahasa pemrograman Rust membantu Anda menulis perangkat lunak yang lebih cepat dan lebih andal. Ergonomi tingkat tinggi dan kontrol tingkat rendah seringkali bertentangan dalam desain bahasa pemrograman; Rust menantang konflik itu. Dengan menyeimbangkan kapasitas teknis yang kuat dan pengalaman pengembang yang hebat, Rust memberi Anda opsi untuk mengontrol detail tingkat rendah (seperti penggunaan memori) tanpa semua kerumitan yang secara tradisional terkait dengan kontrol tersebut.

## Untuk Siapa Rust

Rust sangat ideal bagi banyak orang karena berbagai alasan. Mari kita lihat beberapa kelompok yang paling penting.

### Tim Pengembang

Rust terbukti menjadi alat yang produktif untuk berkolaborasi di antara tim besar pengembang dengan berbagai tingkat pengetahuan pemrograman sistem. Kode tingkat rendah rentan terhadap berbagai bug halus, yang di sebagian besar bahasa lain hanya dapat ditangkap melalui pengujian ekstensif dan tinjauan kode yang cermat oleh pengembang berpengalaman. Di Rust, kompiler memainkan peran penjaga gerbang dengan menolak mengkompilasi kode dengan bug yang sulit dipahami ini, termasuk bug konkurensi. Dengan bekerja bersama kompiler, tim dapat menghabiskan waktu mereka berfokus pada logika program daripada mengejar bug.

Rust juga menghadirkan alat pengembang kontemporer ke dunia pemrograman sistem:

- Cargo, manajer dependensi dan alat build yang disertakan, membuat penambahan, kompilasi, dan pengelolaan dependensi menjadi mudah dan konsisten di seluruh ekosistem Rust.
- Alat pemformatan Rustfmt memastikan gaya pengkodean yang konsisten di seluruh pengembang.
- Rust Language Server memberdayakan integrasi Integrated Development Environment (IDE) untuk _code completion_ dan pesan kesalahan sebaris.

Dengan menggunakan ini dan alat lainnya di ekosistem Rust, pengembang dapat menjadi produktif saat menulis kode tingkat sistem.

### Pelajar

Rust adalah untuk pelajar dan mereka yang tertarik mempelajari konsep sistem. Menggunakan Rust, banyak orang telah belajar tentang topik-topik seperti pengembangan sistem operasi. Komunitas sangat terbuka dan senang menjawab pertanyaan pelajar. Melalui upaya seperti buku ini, tim Rust ingin membuat konsep sistem lebih mudah diakses oleh lebih banyak orang, terutama mereka yang baru mengenal pemrograman.

### Perusahaan

Ratusan perusahaan, besar dan kecil, menggunakan Rust dalam produksi untuk berbagai tugas, termasuk alat baris perintah, layanan web, perkakas DevOps, perangkat yang disematkan, analisis dan transcoding audio dan video, cryptocurrency, bioinformatika, mesin pencari, aplikasi Internet of Things , pembelajaran mesin, dan bahkan bagian utama dari browser web Firefox.

### Pengembang Open Source

Rust adalah untuk orang yang ingin membangun bahasa pemrograman Rust, komunitas, alat pengembang, dan perpustakaan. Kami ingin Anda berkontribusi pada bahasa Rust.

### Orang yang Menghargai Kecepatan dan Stabilitas

Rust adalah untuk orang yang mendambakan kecepatan dan stabilitas dalam suatu bahasa. Yang kami maksud dengan kecepatan adalah seberapa cepat kode Rust dapat berjalan dan kecepatan di mana Rust memungkinkan Anda menulis program. Pemeriksaan kompiler Rust memastikan stabilitas melalui penambahan fitur dan pemfaktoran ulang. Ini berbeda dengan kode lama yang rapuh dalam bahasa tanpa pemeriksaan ini, yang sering kali takut diubah oleh pengembang. Dengan berjuang untuk abstraksi tanpa biaya, fitur tingkat tinggi yang dikompilasi ke kode tingkat rendah secepat kode yang ditulis secara manual, Rust berupaya membuat kode aman menjadi kode cepat juga.

Bahasa Rust berharap untuk mendukung banyak pengguna lain juga; yang disebutkan di sini hanyalah sebagian dari pemangku kepentingan terbesar. Secara keseluruhan, ambisi terbesar Rust adalah menghilangkan trade-off yang telah diterima programmer selama beberapa dekade dengan memberikan keamanan dan produktivitas, kecepatan, dan ergonomi. Cobalah Rust dan lihat apakah pilihannya cocok untuk Anda.

## Untuk Siapa Buku Ini

Buku ini mengasumsikan bahwa Anda telah menulis kode dalam bahasa pemrograman lain tetapi tidak membuat asumsi tentang yang mana. Kami telah mencoba membuat materi dapat diakses secara luas oleh mereka yang berasal dari berbagai latar belakang pemrograman. Kami tidak menghabiskan banyak waktu untuk berbicara tentang apa itu pemrograman atau bagaimana memikirkannya. Jika Anda benar-benar baru dalam pemrograman, sebaiknya Anda membaca buku yang secara khusus memberikan pengantar pemrograman.

## Cara Menggunakan Buku Ini

Secara umum, buku ini berasumsi bahwa Anda membacanya secara berurutan dari depan ke belakang. Bab-bab selanjutnya membangun konsep-konsep di bab-bab sebelumnya, dan bab-bab sebelumnya mungkin tidak membahas secara mendetail tentang topik tertentu tetapi akan meninjau kembali topik tersebut di bab selanjutnya.

Anda akan menemukan dua jenis bab dalam buku ini: bab konsep dan bab proyek. Dalam bab konsep, Anda akan belajar tentang aspek Rust. Dalam bab proyek, kita akan membuat program kecil bersama, menerapkan apa yang telah Anda pelajari sejauh ini. Bab 2, 12, dan 20 adalah bab proyek; sisanya adalah bab konsep.

Bab 1 menjelaskan cara menginstal Rust, cara menulis program "Hello, world!", dan cara menggunakan Cargo, pengelola paket Rust, dan alat _build_. Bab 2 adalah pengantar langsung untuk menulis program di Rust, mengajak Anda membuat permainan tebak angka. Di sini kami membahas konsep-konsep pada tingkat tinggi, dan bab-bab selanjutnya akan memberikan detail tambahan. Jika Anda ingin segera mengotori tangan Anda, Bab 2 adalah tempatnya. Bab 3 membahas fitur-fitur Rust yang mirip dengan bahasa pemrograman lain, dan di Bab 4 Anda akan belajar tentang sistem kepemilikan (_ownership_) Rust. Jika Anda seorang pembelajar yang sangat teliti yang lebih suka mempelajari setiap detail sebelum melanjutkan ke yang berikutnya, Anda mungkin ingin melewati Bab 2 dan langsung ke Bab 3, kembali ke Bab 2 jika Anda ingin mengerjakan proyek yang menerapkan detail yang telah Anda pelajari.

Bab 5 membahas struct dan _method_, dan Bab 6 mencakup enum, ekspresi `match`, dan konstruksi aliran kontrol `if let`. Anda akan menggunakan struct dan enum untuk membuat tipe khusus di Rust.

Di Bab 7, Anda akan belajar tentang sistem modul Rust dan tentang aturan privasi untuk mengatur kode Anda dan Application Programming Interface (API) publiknya. Bab 8 membahas beberapa struktur data koleksi umum yang disediakan perpustakaan standar, seperti vektor, string, dan hash map. Bab 9 mengeksplorasi filosofi dan teknik penanganan kesalahan Rust.

Bab 10 membahas tentang generik, trait, dan _lifetime_, yang memberi Anda kekuatan untuk menentukan kode yang berlaku untuk berbagai tipe. Bab 11 adalah tentang pengujian, yang bahkan dengan jaminan keamanan Rust diperlukan untuk memastikan logika program Anda benar. Di Bab 12, kita akan membuat implementasi subset fungsionalitas kita sendiri dari alat baris perintah `grep` yang mencari teks di dalam file. Untuk ini, kita akan menggunakan banyak konsep yang telah kita diskusikan di bab sebelumnya.

Bab 13 mengeksplorasi closure dan iterator: fitur Rust yang berasal dari bahasa pemrograman fungsional. Di Bab 14, kita akan mempelajari Cargo secara lebih mendalam dan membahas tentang praktik terbaik untuk berbagi pustaka Anda dengan orang lain. Bab 15 membahas smart pointer yang disediakan oleh perpustakaan standar dan trait yang mengaktifkan fungsinya.

Di Bab 16, kita akan menelusuri berbagai model pemrograman konkuren dan berbicara tentang bagaimana Rust membantu Anda memprogram di banyak _thread_ tanpa rasa takut. Bab 17 membahas bagaimana idiom Rust dibandingkan dengan prinsip pemrograman berorientasi objek yang mungkin sudah Anda kenal.

Bab 18 adalah referensi tentang pola dan pencocokan pola, yang merupakan cara ampuh untuk mengekspresikan ide di seluruh program Rust. Bab 19 berisi hamparan topik lanjutan yang menarik, termasuk Rust yang tidak aman, makro, dan lebih banyak lagi tentang _lifetime_, trait, tipe, fungsi, dan _closure_.

Di Bab 20, kita akan menyelesaikan proyek di mana kita akan mengimplementasikan server web multithread level rendah!

Terakhir, beberapa lampiran berisi informasi berguna tentang bahasa dalam format yang lebih mirip referensi. Lampiran A mencakup kata kunci Rust, Lampiran B mencakup operator dan simbol Rust, Lampiran C mencakup sifat turunan yang disediakan oleh perpustakaan standar, Lampiran D mencakup beberapa alat pengembangan yang berguna, dan Lampiran E menjelaskan edisi Rust. Di Lampiran F, Anda dapat menemukan terjemahan dari buku tersebut, dan di Lampiran G kami akan membahas bagaimana Rust dibuat dan apa itu nightly Rust.

Tidak ada cara yang salah untuk membaca buku ini: jika Anda ingin melewatinya, lakukan saja! Anda mungkin harus kembali ke bab sebelumnya jika mengalami kebingungan. Tetapi lakukan apa pun yang berhasil untuk Anda.

<span id="ferris"></span>

Bagian penting dari proses mempelajari Rust adalah mempelajari cara membaca pesan kesalahan yang ditampilkan kompiler: ini akan memandu Anda menuju kode yang berfungsi. Karena itu, kami akan memberikan banyak contoh yang tidak dapat dikompilasi bersama dengan pesan kesalahan yang akan ditampilkan oleh kompiler kepada Anda di setiap situasi. Ketahuilah bahwa jika Anda memasukkan dan menjalankan contoh acak, mungkin tidak dapat dikompilasi! Pastikan Anda membaca teks di sekitarnya untuk melihat apakah contoh yang Anda coba jalankan dimaksudkan untuk kesalahan. Ferris juga akan membantu Anda membedakan kode yang tidak dimaksudkan untuk berfungsi:

| Ferris                                                                                                           | Arti                                                  |
| ---------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| <img src="img/ferris/does_not_compile.svg" class="ferris-explain" alt="Ferris with a question mark"/>            | Kode ini tidak dapat dikompilasi!                     |
| <img src="img/ferris/panics.svg" class="ferris-explain" alt="Ferris throwing up their hands"/>                   | Kode ini panik!                                       |
| <img src="img/ferris/not_desired_behavior.svg" class="ferris-explain" alt="Ferris with one claw up, shrugging"/> | Kode ini tidak menghasilkan perilaku yang diinginkan. |

Dalam sebagian besar situasi, kami akan mengarahkan Anda ke versi yang benar dari kode apa pun yang tidak dapat dikompilasi.

## Kode sumber

File sumber dari mana buku ini dibuat dapat ditemukan di [GitHub][book].

[book]: https://github.com/renomureza/rust-book-id/tree/main/src-id

# Kebijakan Keamanan Snapdown

<!-- Copied from the Wira Delta Indonesia legal source (snapdown/security.id.md) on 2026-09-26.
     Edit the source, then copy it here again. -->

**Berlaku sejak:** 1 Oktober 2026

Snapdown berjalan sebagai proses pengguna biasa yang **tidak elevated**. Snapdown dipasang per pengguna tanpa hak Administrator, tidak meminta hak Administrator saat berjalan, tidak memasang keyboard hook tingkat rendah untuk seluruh sistem, dan tidak menjalankan service di latar belakang. Shortcut-nya didaftarkan lewat API Win32 standar `RegisterHotKey`, yang hanya mengantarkan kombinasi tombol yang Anda atur; API itu tidak bisa mengamati ketikan lain.

Tiga sifat lain juga layak Anda periksa, jadi kami sebutkan di depan. Snapdown **mendaftarkan dirinya untuk berjalan saat Anda masuk ke Windows** pada jalan pertama (registry `HKCU\...\CurrentVersion\Run`, bisa dimatikan di Settings). Saat tangkapan area dibuka, Snapdown **membaca daftar window yang terlihat** (`EnumWindows`) dan **menelusuri pohon UI Automation** window itu, hanya untuk mengambil kotak batas dan status terlihat tidaknya, supaya Anda bisa memilih area dengan satu klik; judul, teks, dan isi kontrol tidak dibaca. Dan Snapdown **mengunduh installer lalu menjalankannya**, hanya saat Anda memilih memasang update.

## Dua Fakta yang Paling Ingin Diketahui

1. **Snapdown tidak merekam ketikan.** Tidak ada panggilan `SetWindowsHookEx` di kode Snapdown maupun di library shortcut yang dipakainya (`global-hotkey`, yang di Windows memakai `RegisterHotKey`). Panel Key check di Settings hanya membaca tombol yang ditekan saat window Settings Snapdown sendiri sedang aktif.
2. **Snapdown membuat dua jenis permintaan keluar, dan hanya dua.** Cek update ke `https://wiradelta.com/api/v1/update/snapdown/`, di server situs kami di belakang Cloudflare, yang menyala secara default setiap 24 jam dan bisa dimatikan di Settings → About. Header `User-Agent`-nya membawa nama produk, versi Snapdown, versi Windows, dan arsitektur komputer, dan tidak ada lagi yang dilampirkan. Build biasa mengunduh installer dari GitHub Releases bila Anda memilih memasang update; build Microsoft Store menyerahkan pemasangan update ke Microsoft Store; build Scoop menampilkan perintah `scoop update snapdown` dan menyerahkan unduhan serta pemasangannya ke Scoop. Dan aktivasi lisensi ke Lemon Squeezy, hanya saat Anda menekan Activate atau Deactivate. `PRIVACY.md` menjelaskan persis apa yang dibawa setiap permintaan.

Keduanya memakai klien HTTP yang sama (`ureq`): hanya HTTPS, dengan batas waktu dan batas ukuran jawaban. Klien lisensi tidak mengikuti pengalihan (redirect) sama sekali. Endpoint cek update menjawab sendiri, tanpa pengalihan ke GitHub. Unduhan installer dari GitHub Releases mengikuti paling banyak satu pengalihan, hanya ke alamat HTTPS, dan hanya ke host GitHub yang ada di daftar izin. Tidak ada analitik, tidak ada akun, dan **tidak ada soket yang mendengarkan**: tidak ada apa pun di build rilis yang menerima koneksi masuk.

## Updater, dan Apa yang Benar-Benar Memverifikasinya

Manifest menyebut digest SHA-256 untuk setiap installer. Unduhan dialirkan ke file sementara, dihitung hash-nya selagi ditulis, dan dicocokkan dengan digest itu **sebelum apa pun dijalankan**; bila tidak cocok, proses dibatalkan, file sementara dihapus, dan tidak ada yang dijalankan. Pengalihan ke alamat `http://` biasa ditolak, jadi pengalihan tidak bisa diam-diam menurunkan transfer ke HTTP tanpa enkripsi.

Perlu tepat soal apa yang dibuktikan hal itu, karena batasnya sama dengan panduan checksum di bawah: ia membuktikan byte yang tiba adalah byte yang dijelaskan manifest. Ia **tidak** membuktikan siapa yang menulis manifest. Kepercayaan itu bertumpu pada manifest yang disajikan lewat HTTPS dari server resmi kami (di belakang Cloudflare), dan kelak, begitu code signing ada, pada tanda tangannya.

Sebelum memasang, Snapdown menampilkan catatan rilis dan tautan ke EULA versi baru. Installer yang sudah lolos pencocokan dijalankan tanpa menampilkan wizard, lalu Snapdown dibuka ulang. Build Microsoft Store tidak memakai updater ini: tombol pasangnya membuka Microsoft Store, yang memasang update-nya. Build Scoop juga tidak memakainya: tombol update-nya menampilkan perintah `scoop update snapdown`, dan Scoop memeriksa digest SHA-256 build portable dari manifest Scoop sebelum memasangnya. Cek otomatis **menyala secara default** pada pemasangan baru dan bisa dimatikan di Settings.

## Melaporkan Kerentanan

Kode sumber Snapdown **tidak publik**, jadi GitHub Security Advisories di repo sumbernya tidak bisa dijangkau pelapor dari luar. Laporkan dugaan kerentanan ke:

**security@wiradelta.com**

Jangan menaruh rincian eksploit di issue atau komentar publik mana pun, termasuk di repo rilis publik.

Yang membantu dalam laporan: build Windows, versi Snapdown, apa yang Anda lakukan, apa yang terjadi, dan bila ada, langkah minimal untuk mereproduksinya. Tidak ada program bug bounty, dan laporan ditangani sebaik-baiknya (best effort) tanpa jaminan waktu tanggapan.

**Dalam lingkup:** apa pun yang membuat Snapdown membaca, menulis, atau membuka data yang tidak semestinya; apa pun yang menjalankan kode yang tidak Anda minta, termasuk apa pun yang membuat update yang diunduh bisa berjalan tanpa cocok dengan digest manifest, atau membuat manifest bisa ditukar di tengah jalan; crash yang bisa dipicu oleh tangkapan, bundle, file impor, atau gambar tempelan yang dibuat khusus.

**Di luar lingkup:** penyerang yang sudah punya tingkat akses yang sama ke komputer Anda dengan tingkat akses Snapdown sendiri (proses pengguna yang tidak elevated tidak bisa menjadi sasaran eskalasi yang berarti bagi orang yang sudah menjadi Anda di komputer Anda sendiri); kerentanan pada komponen pihak ketiga (Slint, IBM Plex, Lucide) yang tidak khusus pada cara Snapdown memakainya. Laporkan itu ke pembuatnya.

## Integritas Rilis

**Binary Snapdown belum memakai code signing.** Ada dua akibat, kami sebutkan terang karena keduanya terlihat oleh pengguna:

- Windows SmartScreen akan memperingatkan pada jalan pertama ("Windows protected your PC" / aplikasi tidak dikenal). Itu wajar untuk build tanpa tanda tangan dan bukan, dengan sendirinya, bukti adanya perusakan. Karena itu pula, peringatan tersebut tidak bisa membantu Anda membedakan installer asli dari installer palsu.
- Karena kode sumbernya tidak publik, **satu-satunya verifikasi yang tersedia adalah checksum yang diterbitkan**, bukan "build sendiri lalu bandingkan". Setiap rilis menerbitkan digest SHA-256 per installer, di manifest dan di file `SHA256SUMS`. Updater di aplikasi memeriksanya untuk Anda; bila Anda mengunduh sendiri, periksa sebelum menjalankannya:

  ```powershell
  Get-FileHash .\Snapdown-<versi>-x64-setup.exe -Algorithm SHA256
  ```

  Build portable yang dibuat khusus untuk Scoop punya digest SHA-256 di manifest Scoop, dan Scoop memeriksanya saat memasang.

  Checksum yang diterbitkan di samping file yang dijelaskannya membuktikan unduhan tidak rusak atau ditukar di tengah jalan. Checksum itu **tidak** membuktikan siapa yang membuat build aslinya; kepercayaan itu bertumpu pada mengunduh hanya dari saluran resmi yang disebut di `README.md`.

Code signing adalah perbaikan yang sesungguhnya untuk butir kedua, dan belum diterapkan.

## Versi yang Didukung

Hanya rilis terbaru yang menerima perbaikan. Tidak ada cabang dukungan jangka panjang, dan tidak ada SLA (jaminan tingkat layanan), untuk Snapdown maupun Snapdown Pro.

## Catatan Rancangan

- Vault (screenshot) dan database pustaka berada di profil pengguna Anda sendiri dengan izin pengguna biasa (lihat `PRIVACY.md`). Snapdown tidak meminta elevated untuk melindunginya, dan memang tidak perlu, karena tidak ada di dalamnya yang perlu dilindungi dari akun Anda sendiri.
- Menghapus Finding atau bundle menghapus file-nya dari disk secara langsung, tidak lewat Recycle Bin, dan aplikasi tidak punya tempat pemulihan sendiri, jadi penghapusan tidak bisa dibatalkan dengan membuka ulang Snapdown.
- Uninstaller tidak pernah menghapus vault. Uninstaller menanyakan apakah preferensi dan database (`%APPDATA%\com.wiradelta.snapdown`) ikut dihapus; uninstall tanpa tampilan (silent) tidak menghapusnya. Uninstall lewat Scoop hanya menghapus folder aplikasi; pengaturan, database, dan `licence.json` di `%APPDATA%\com.wiradelta.snapdown` tetap ada.
- Export PDF menulis ke lokasi yang Anda pilih lewat dialog simpan Windows; Snapdown tidak diam-diam menulis file ekspor di tempat lain. Copy Markdown menyalin teks yang memuat path lengkap file di vault ke clipboard.
- Lisensi yang aktif disimpan di file kecil, `licence.json`, yang disegel dengan checksum berkunci (HMAC) supaya suntingan biasa terdeteksi. Itu penghalang, bukan batas keamanan: seperti setiap lisensi di sisi klien, ia bisa dikalahkan dengan memodifikasi programnya. Bila file itu rusak atau gagal diperiksa, Snapdown diam-diam berjalan sebagai Free; file rusak tidak pernah diperlakukan sebagai tuduhan.
- Aplikasi hanya menerima kunci bila Lemon Squeezy melaporkannya sebagai milik **Snapdown Pro** di toko Wira Delta Indonesia. Kunci yang sah untuk produk Lemon Squeezy lain ditolak.
- Status Pro dibaca sekali saat Snapdown dibuka dan diperbarui saat Anda menekan Activate atau Deactivate. Status itu hanya dipakai di satu tempat: menentukan apakah PDF yang diekspor memuat tanda atribusi.

## Bahasa

Bahasa. Naskah ini dibuat dalam bahasa Indonesia dan diterjemahkan ke bahasa Inggris. Bila terdapat
perbedaan tafsir antara keduanya, naskah bahasa Indonesia yang berlaku.

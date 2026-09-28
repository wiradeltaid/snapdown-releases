# Kebijakan Privasi Snapdown

<!-- Copied from the Wira Delta Indonesia legal source (snapdown/privacy.id.md) on 2026-09-26.
     Edit the source, then copy it here again. -->

**Berlaku sejak:** 1 Oktober 2026

Snapdown adalah software (perangkat lunak) untuk mengambil dan meninjau screenshot. Semua yang diambil dan disimpan Snapdown berada **hanya di komputer Anda sendiri**. Tidak ada analitik, laporan crash, akun pengguna, atau ID perangkat. Kebijakan ini berlaku sama untuk ketiga saluran pemasangan Snapdown: installer dari GitHub Releases, build Microsoft Store, dan build portable yang dibuat khusus untuk Scoop. Dua hal di aplikasi menyentuh jaringan, dan bagian di bawah menjelaskan keduanya secara lengkap, bukan meringkasnya. Yang pertama, **cek update**, menyala secara default, mengirim versi Snapdown, versi Windows, dan arsitektur komputer Anda ke server kami di `wiradelta.com`, dan bisa dimatikan. Yang kedua, **aktivasi Snapdown Pro**, terjadi hanya saat Anda menekan Activate atau Deactivate, dan tidak pernah dengan sendirinya.

## Yang Diambil Snapdown

Snapdown mengambil screenshot seluruh layar, satu window, atau satu area, hanya saat Anda memicunya (lewat shortcut atau tombol). Snapdown tidak pernah mengambil screenshot terus-menerus atau di latar belakang. Setiap tangkapan menjadi **Finding**: gambarnya sendiri, ditambah catatan, pin, atau anotasi yang Anda tambahkan.

Anda juga bisa membuat Finding dari file gambar yang Anda impor, atau dari gambar yang Anda tempel dari clipboard. Snapdown membaca clipboard hanya saat Anda menekan Paste.

Saat tangkapan area dibuka, Snapdown membaca posisi dan ukuran window serta panel yang sedang terlihat di layar, supaya Anda bisa memilih satu area dengan satu klik. Yang dibaca hanya kotak batasnya. Judul window, teks, dan isi kontrol di dalamnya tidak dibaca, dan kotak batas itu tidak disimpan.

**Perhatikan apa yang Anda ambil.** Screenshot bisa memuat apa saja yang terlihat di layar Anda saat itu: kata sandi di password manager yang terbuka, pesan pribadi, nomor rekening, data orang lain. Snapdown tidak bisa membedakan isi yang sensitif dari isi lain di layar. Penilaian itu ada pada Anda, baik saat mengambil screenshot maupun saat menyalin, mengekspor, atau membagikan bundle yang Anda susun dari Finding Anda.

## Yang Disimpan di Disk, dan di Mana

| Path | Isi | Retensi |
|---|---|---|
| `%APPDATA%\com.wiradelta.snapdown\library.db` | Database Finding dan bundle: catatan, pin, waktu, rujukan ke file gambar di vault, dan pengaturan Anda | Sampai Anda menghapus Finding atau bundle, atau menghapus file ini sendiri. Uninstaller menanyakan apakah folder ini ikut dihapus |
| `%USERPROFILE%\Pictures\SnapdownVault\` (default; installer menanyakan lokasinya, dan Anda bisa memindahkannya di Settings) | Vault: screenshot asli di `findings\`, dan per bundle satu folder `bundles\<id>\` berisi `bundle.md` dan file PNG dengan anotasi burn-in (menyatu di gambar) | Sampai Anda menghapus Finding atau bundle di aplikasi, atau menghapus folder ini sendiri. Snapdown tidak menghapus gambar asli secara otomatis, dan uninstaller tidak pernah menghapus vault |
| `%APPDATA%\com.wiradelta.snapdown\vault_path.txt` dan registry `HKCU\Software\Wira Delta Indonesia\Snapdown` (nilai `VaultPath`) | Lokasi vault Anda, supaya installer menemukannya saat update atau pemasangan ulang | Sampai Anda menjawab Yes saat uninstaller menanyakan penghapusan data, atau menghapusnya sendiri |
| `%APPDATA%\com.wiradelta.snapdown\licence.json` (hanya bila Snapdown Pro aktif) | License key Anda, ID aktivasi yang diberikan Lemon Squeezy, alamat email yang dipakai saat membeli, tanggal aktivasi, dan checksum berkunci | Sampai Anda menekan Deactivate dan Lemon Squeezy mengonfirmasinya (butuh koneksi internet). Uninstall dengan jawaban Yes juga menghapus file ini, tetapi tidak menonaktifkan aktivasinya |
| `%TEMP%\Snapdown-Setup-Update.exe` (hanya setelah Anda memasang update dari aplikasi) | Installer update yang diunduh dan sudah dicocokkan checksum-nya | Sampai update berikutnya menimpanya, atau Anda atau Windows membersihkan folder Temp |
| Registry `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` (nilai `Snapdown`) | Perintah untuk menjalankan Snapdown saat Anda masuk ke Windows. Dibuat saat Snapdown pertama kali dijalankan | Sampai Anda mematikan "Run Snapdown at Windows startup" di Settings. Uninstaller tidak menghapus nilai ini |

Pada build Scoop, uninstall lewat Scoop (`scoop uninstall snapdown`) hanya menghapus folder aplikasi. Pengaturan, database, dan `licence.json` di `%APPDATA%\com.wiradelta.snapdown` tetap ada sampai Anda menghapusnya sendiri, dan aktivasi Snapdown Pro tidak ikut dinonaktifkan, jadi tekan Deactivate lebih dulu.

File dan nilai registry ini ada di akun pengguna Windows Anda sendiri, dengan izin pengguna biasa: anggap semuanya bisa dibaca program lain yang berjalan atas nama Anda, sama seperti file lain di profil pengguna Anda. Memindahkan vault di Settings memindahkan semua file yang sudah ada ke lokasi baru; tidak ada yang digandakan atau tertinggal karena pemindahan itu.

**Menghapus Finding atau bundle bersifat permanen.** Menghapus Finding menghapus barisnya di database dan screenshot aslinya di vault; salinan burn-in di bundle yang memuat Finding itu tetap ada sampai bundle-nya dihapus. Menghapus bundle menghapus folder bundle-nya (`bundle.md` dan PNG-nya); Finding-nya tetap ada. File dihapus langsung, tidak dipindah ke Recycle Bin, dan aplikasi tidak punya tempat pemulihan sendiri.

## Mengeluarkan Hasil dari Snapdown

Ada tiga cara, dan ketiganya Anda yang memulai:

- **Copy image** menyalin satu gambar ke clipboard, dengan atau tanpa anotasi burn-in.
- **Copy Markdown** menyalin isi Markdown sebuah bundle ke clipboard. Teks itu memuat path lengkap file gambar di vault, yang biasanya berisi nama pengguna Windows Anda. Bila Anda mengaktifkan instruksi hand-off di Settings, instruksi itu ikut di awal teks.
- **Export PDF** menulis satu file PDF ke lokasi yang **Anda** pilih lewat dialog simpan Windows. Pada Snapdown Free, tanda di footer PDF adalah tautan ke `https://wiradelta.com/snapdown`; membukanya adalah kunjungan biasa ke situs kami.

Setelah itu, hasilnya adalah isi clipboard atau file biasa. Snapdown tidak terlibat lagi, tidak melacak ke mana hasil itu pergi, dan tidak mengunggahnya ke mana pun.

## Aktivitas Jaringan

Mengambil screenshot, memberi anotasi, menyusun bundle, menyalin, dan mengekspor berjalan sepenuhnya offline: tidak satu pun membuat permintaan jaringan. **Dua hal di Snapdown membuat permintaan jaringan: cek update, dan mengaktifkan atau menonaktifkan Snapdown Pro.** Memasang update adalah satu-satunya hal yang mengunduh file. Masing-masing dijelaskan lengkap di bawah.

### Cek Update

**Yang dikirim.** Permintaan HTTPS `GET` tanpa login ke `https://wiradelta.com/api/v1/update/snapdown/`, server milik Wira Delta Indonesia. Header `User-Agent` permintaan itu membawa empat hal: nama produk (Snapdown), nomor versi Snapdown yang Anda jalankan, versi Windows, dan arsitektur komputer (misalnya x64 atau ARM64). Selain itu tidak ada yang dilampirkan: tidak ada nama komputer, nama pengguna, detail perangkat keras lain, akun, ID perangkat, atau penghitung, dan hanya header standar yang tidak bisa dihilangkan dari sebuah permintaan (`Host`, `Accept`). Build Microsoft Store dan build Scoop mengirim cek yang sama. Endpoint itu menjawab sendiri dan tidak mengalihkan permintaan ke GitHub, jadi GitHub tidak menerima cek update.

**Yang tetap terungkap, karena sebuah permintaan tidak bisa menyembunyikannya.** Server kami melihat alamat IP asal permintaan, waktunya, dan isi `User-Agent`. Endpoint berada di server yang sama dengan situs `wiradelta.com`, di belakang Cloudflare. Cloudflare meneruskan permintaan ke server kami dan ikut melihat alamat IP serta isi permintaan itu, menurut kebijakan privasi Cloudflare.

**Yang kami simpan, dan berapa lama.** Server kami menyimpan catatan mentah setiap permintaan (alamat IP, waktu, dan isi `User-Agent`) selama **30 hari**, lalu menghapusnya. Yang tersisa sesudah itu hanya hitungan harian agregat berdasarkan data yang dikirim aplikasi (versi aplikasi, versi Windows, arsitektur) dan perkiraan jumlah perangkat, tanpa alamat IP. Kami memakainya untuk mengetahui berapa banyak pemasangan yang memakai tiap versi, di versi Windows dan arsitektur apa. Catatan ini tidak digabung dengan data pembelian atau daftar tunggu.

**Yang tidak dikirim, dan tidak mungkin dikirim.** Permintaan itu tidak membawa isi tentang pemakaian Anda: tidak berapa banyak Finding Anda, tidak apa yang Anda ambil, dan tidak apakah Anda memakai Snapdown Pro.

**Cara mematikannya.** Cek otomatis setiap 24 jam **menyala secara default** pada pemasangan baru, dan sakelarnya adalah "Check automatically every 24 hours" di Settings → About. Mematikannya menghentikan semua aktivitas jaringan berkala; tombol manual "Check for Updates" tetap ada, jadi Anda bisa bertanya sekali tanpa membiarkan apa pun berjalan. Tidak ada yang berkurang karenanya: cek update hanya memberi tahu bahwa ada versi lebih baru, dan tidak mengunci apa pun.

### Memasang Update

Ada tiga jalur update. Pada build biasa, sebelum memasang, Snapdown menampilkan catatan rilis dan tautan ke EULA versi baru. Bila Anda memilih memasang update dengan tombol Download and Install, Snapdown mengunduh installer yang disebut oleh manifest dari GitHub Releases repo `wiradeltaid/snapdown-releases`, lalu menjalankannya tanpa menampilkan wizard, dan Snapdown dibuka ulang sesudahnya. GitHub melihat alamat IP Anda saat unduhan itu, menurut kebijakan privasi GitHub. Itulah satu-satunya saat aplikasi mengambil sesuatu selain file teks kecil, dan satu-satunya saat aplikasi menjalankan program lain.

Manifest menyebut digest SHA-256 untuk setiap installer. Unduhan dihitung hash-nya selagi ditulis dan dicocokkan dengan digest itu **sebelum apa pun dijalankan**; bila tidak cocok, proses dibatalkan dan file tidak pernah dijalankan. Langkah ini tidak dimulai oleh cek berkala, hanya oleh Anda, dari Settings. Pada build Microsoft Store, cek versi tetap dilakukan ke `wiradelta.com` seperti di atas, tetapi tombol pasang membuka Microsoft Store: update dipasang oleh Store, dan Snapdown tidak mengunduh installer sendiri. Pada build Scoop, cek versi juga dilakukan ke `wiradelta.com`, tetapi tombol update tidak mengunduh installer: tombol itu menampilkan perintah `scoop update snapdown` untuk Anda jalankan sendiri. Scoop lalu mengunduh build portable yang baru dan memeriksa digest SHA-256-nya dengan yang tercantum di manifest Scoop sebelum memasangnya.

### Mengaktifkan Snapdown Pro

Ini terjadi **hanya saat Anda menekan Activate atau Deactivate** di Settings → About. Snapdown tidak pernah menghubungi layanan lisensi dengan sendirinya: tidak saat dibuka, tidak saat mengekspor, tidak di latar belakang, dan tidak untuk memeriksa ulang lisensi yang sudah aktif.

**Yang dikirim.** Permintaan HTTPS `POST` ke Lemon Squeezy (`api.lemonsqueezy.com`), merchant yang menjual Snapdown Pro atas nama kami. Mengaktifkan mengirim license key yang Anda tempel dan label untuk komputer ini. Menonaktifkan mengirim license key dan ID aktivasi yang diberikan Lemon Squeezy saat aktivasi.

**Apa label itu, dan apa yang bukan.** Bentuknya seperti `Snapdown on Windows · 2026-09-23 · 4f1a`: sistem operasi, tanggal aktivasi, dan empat karakter acak supaya Anda bisa membedakan komputer Anda di halaman pesanan Lemon Squeezy. **Label itu bukan nama komputer Anda**, yang sering memuat nama orang, dan tidak membawa detail perangkat keras.

**Yang tetap terungkap.** Lemon Squeezy melihat alamat IP asal permintaan, dan sudah memegang apa yang Anda berikan saat checkout: nama, alamat email, dan pesanan Anda. Penanganannya diatur kebijakan privasi Lemon Squeezy sendiri.

**Yang kembali, dan yang kami simpan.** Lemon Squeezy menjawab apakah kunci itu sah untuk Snapdown Pro, beserta alamat email yang dipakai saat membeli. Snapdown menyimpan jawaban itu di `licence.json` di komputer Anda (lihat "Yang Disimpan di Disk, dan di Mana"). Kami, penerbit, tidak menerima apa pun dari aplikasi lewat jalur ini; kami melihat pembelian Anda hanya lewat catatan pesanan merchant, seperti penjual mana pun.

**Bila Anda tidak pernah membeli Pro**, jalur ini tidak pernah dipakai.

## Daftar Tunggu Snapdown Pro

Daftar tunggu ada di situs `wiradelta.com`, bukan di aplikasi. Alamat email yang Anda daftarkan disimpan di server kami dan dipakai untuk mengirim kabar tentang Snapdown Pro dan produk Wira Delta Indonesia berikutnya. Dasarnya adalah persetujuan yang Anda berikan saat mendaftar, dan formulir pendaftaran menyatakan pemakaian ini. Setiap email memuat tautan berhenti berlangganan; saat Anda memakainya, alamat Anda dihapus dari daftar di server kami dan dari email pemberitahuan pendaftaran yang kami terima. Rinciannya ada di Kebijakan Privasi situs (`wiradelta.com/id/privacy/`).

## Komponen Pihak Ketiga

Snapdown dikirim bersama Slint, IBM Plex, dan ikon Lucide, masing-masing dengan lisensinya sendiri; daftar lengkap komponen pihak ketiga ada di `NOTICE.txt` di folder instalasi dan di tab About aplikasi. Tidak satu pun menghubungi server dari dalam Snapdown: semuanya library antarmuka dan rendering, serta aset font dan ikon, bukan layanan.

## Hak Anda

Satu-satunya data pribadi dari aplikasi yang sampai ke kami adalah alamat IP di catatan cek update, yang dihapus setelah 30 hari. Sesuai Undang-Undang Nomor 27 Tahun 2022 tentang Pelindungan Data Pribadi, Anda berhak meminta akses, perbaikan, atau penghapusan data pribadi Anda yang kami simpan. Data pembelian Snapdown Pro dipegang Lemon Squeezy sebagai merchant; permintaan atasnya bisa Anda ajukan ke Lemon Squeezy atau lewat kami. Kirim permintaan ke `support@wiradelta.com`.

## Pertanyaan

Lihat `SECURITY.md` untuk cara melaporkan masalah keamanan. Untuk hal lain tentang kebijakan ini, hubungi **support@wiradelta.com**.

## Bahasa

Bahasa. Naskah ini dibuat dalam bahasa Indonesia dan diterjemahkan ke bahasa Inggris. Bila terdapat
perbedaan tafsir antara keduanya, naskah bahasa Indonesia yang berlaku.

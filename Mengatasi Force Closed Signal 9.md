Soal "signal 9" dan "pembatasan proses anak" di Termux itu emang isu klasik yang sering bikin pusing kepala teman-teman ngoprek, hehe. 
Intinya sih, Android zaman sekarang itu suka 'galak' sama aplikasi yang jalan di background lama-lama atau yang punya banyak 'anak proses', termasuk Termux. 
Sistemnya berusaha hemat baterai, tapi kadang jadi kebablasan sampai proses penting di Termux ikut 'disapu bersih' alias di-kill paksa (itu dia si signal 9 / SIGKILL).

Nah, buat ngatasinnya, ada beberapa 'jurus' yang bisa kamu coba:
* [VIDEONYA DI SINI](https://youtu.be/J_xIr4yUvNA?si=WliFqvbb0QFJDXqO](https://youtube.com/shorts/biDXD-6fIhU?si=fmpaOcOqVqX7N_ic )

1.  **Nonaktifkan Optimasi Baterai buat Termux (WAJIB BANGET!):**
    Ini langkah pertama dan paling penting.
    * Buka **Pengaturan Android** di HP-mu.
    * Cari menu **Baterai** atau **Pengelolaan Baterai**.
    * Cari lagi bagian **Optimasi Baterai**, **Aplikasi yang Dioptimalkan**, atau yang mirip-mirip itu (tiap merk HP kadang beda istilahnya).
    * Di daftar aplikasi, cari **Termux**. Kalau ada aplikasi pendukung Termux lain yang kamu pakai (kayak Termux:API, Termux:Widget, Termux:X11), sekalian aja cari juga.
    * Pilih Termux, terus ubah pengaturannya jadi **"Jangan optimalkan"**, **"Tidak dibatasi"**, atau yang semacamnya. Intinya, kasih izin Termux buat 'hidup bebas' tanpa dikekang optimasi baterai.

2.  **Pakai `termux-wake-lock` (Biar Termux 'Melek' Terus):**
    Kalau kamu mau ngejalanin perintah atau script yang butuh waktu lama, sebelum mulai, ketik ini di Termux:
    ```bash
    termux-wake-lock
    ```
    Ini kayak ngasih kopi ke Termux biar dia gak 'ketiduran' dan prosesnya gak di-kill. Kalau udah selesai, kamu bisa lepasin kuncinya dengan:
    ```bash
    termux-wake-unlock
    ```
    Tapi, seringnya sih, cukup `termux-wake-lock` aja di awal sesi atau script panjang.

3.  **Nonaktifkan "Phantom Process Killing" (Buat Android 12 ke Atas):**
    Ini nih yang sering jadi biang keladi "pembatasan proses anak".
    * Aktifkan dulu **Opsi Pengembang** di HP-mu. Caranya:
        * Buka **Pengaturan Android > Tentang Ponsel**.
        * Cari **Nomor Versi** atau **Build Number** (atau yang mirip).
        * Ketuk bagian itu **7-10 kali** berturut-turut sampai muncul notifikasi "Anda kini adalah seorang pengembang!"
    * Setelah Opsi Pengembang aktif, kembali ke **Pengaturan Android > Sistem > Opsi Pengembang** (lokasinya bisa beda-beda tergantung merk HP).
    * Di dalam Opsi Pengembang, scroll ke bawah dan cari opsi yang bunyinya mirip:
        * **"Disable child process restrictions"**
        * **"Disable phantom process monitoring"**
        * **"Tangguhkan eksekusi untuk aplikasi dalam cache"** (kadang ini juga berpengaruh, coba dinonaktifkan)
    * Aktifkan/Nonaktifkan opsi tersebut sesuai kebutuhan (biasanya kita ingin *disable* pembatasannya). **PENTING:** Mengubah Opsi Pengembang bisa berisiko kalau gak hati-hati, jadi pastikan kamu tahu apa yang kamu ubah ya.

4.  **Pastikan Notifikasi Termux Selalu Ada:**
    Termux itu berusaha jalan sebagai *foreground service* dengan nampilin notifikasi. Kalau notifikasi ini ada, kemungkinan Termux buat di-kill sistem jadi lebih kecil. Jadi, jangan pernah *swipe* atau tutup notifikasi Termux pas lagi dipakai.

5.  **Settingan Khusus dari Merk HP Kamu:**
    Beberapa merk HP (kayak Xiaomi, Huawei, OnePlus, Samsung, dll) punya sistem manajemen daya yang super agresif. Kamu mungkin perlu cari settingan khusus di HP-mu:
    * Cari menu kayak **"Auto-start management"**, **"Background app management"**, **"App launch"**, atau yang sejenisnya.
    * Pastikan Termux diizinkan buat auto-start dan jalan di background tanpa batas.
    * Kamu bisa cek website `dontkillmyapp.com`. Di situ banyak info soal settingan spesifik buat berbagai merk HP biar aplikasi gak gampang di-kill.

6.  **Gunakan `termux-services` (Untuk 'Server' Jangka Panjang):**
    Kalau kamu jalanin sesuatu yang sifatnya kayak server (misal SSH server, web server, bot, dll) yang harus nyala terus, lebih baik dikelola pakai `termux-services`. Ini bikin prosesmu lebih 'tahan banting'.
    * Install dulu: `pkg install termux-services`
    * Terus kamu perlu bikin script service-nya. Agak teknis, tapi ampuh.

7.  **Periksa Aplikasi Pihak Ketiga:**
    Kalau kamu install aplikasi penghemat baterai atau task killer dari pihak ketiga, coba nonaktifkan dulu atau kasih pengecualian buat Termux.

**Ringkasnya, yang paling sering berhasil itu kombinasi:**
* Nonaktifkan optimasi baterai buat Termux.
* Pakai `termux-wake-lock`.
* Nonaktifkan "phantom process killing" di Opsi Pengembang (kalau ada & kamu nyaman ngopreknya).


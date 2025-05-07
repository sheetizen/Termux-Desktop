# 🚀 Panduan Lengkap: Sulap HP Android Jadi Desktop Debian (Gak Perlu Root!) + Shortcut Widget Kece! 🛠️

Halo, Sheetizen! 👋 
Pernah ngebayangin HP Android kamu bisa se-powerful PC? Install aplikasi Linux, multitasking dengan banyak jendela, semua dari genggamanmu? Nah, di sini aku bakal tuntun kamu langkah demi langkah biar HP-mu makin jagoan!

Kita bakal pasang Desktop Environment Debian (XFCE4 yang ringan) pakai Termux dan `proot-distro`. Dan yang paling seru? **INI GAK PERLU AKSES ROOT, lho!** Cocok banget buat kamu yang pengen nyicipin Linux desktop di HP tanpa ribet, plus nanti kita bikin shortcut keren via widget Termux!

Yuk, langsung aja kita mulai petualangannya! 👇

---

## 🛠️ Langkah 1: Siapin 'Amunisi' Awal: SETUP Termux

Ini fondasi kita, jadi pastiin semua siap tempur!

* **Install Aplikasi Wajib:**
    * **Termux:** Ambil dari F-Droid atau GitHub ya, jangan yang dari Play Store karena udah gak update. Ini 'terminal sakti' kita!
    * **Termux X11:** Ini buat nampilin grafis desktopnya. Cari aja di GitHub `termux-x11` terus install APK-nya.

* **Beri Termux Izin Akses Storage:**
    Buka Termux, terus masukkan perintah ini:
    ```bash
    termux-setup-storage
    ```

* **Update Termux**
    Buka Termux, terus masukkan perintah ini:
    ```bash
    pkg update
    pkg upgrade -y
    pkg install x11-repo
    pkg install termux-x11-nightly
    pkg install tur-repo
    pkg install pulseaudio
    pkg install proot-distro
    pkg install wget
    pkg install git
    ```
    Ini biar Termux-mu selalu fresh dan siap buat install Debian!

## 🛠️ Langkah 2: INSTALL DEBIAN

Distro Linux yang aku gunakan untuk proyek-proyekku.
Pakai Debian soalnya pengen aja hehehe

* **Pasang `proot-distro`:**
    Buka Termux, terus masukkan perintah ini:
    ```bash
    pkg install proot-distro
    ```
    Ini biar Termux-mu selalu fresh dan siap buat install Debian!

* **Install Debian, Distro yang Aku Gunakan:**
    ```bash
    proot-distro install debian
    ```
    Tungguin aja prosesnya, dia lagi 'ngebangun' sistem Debian di HP kamu.

* **Login ke Debian & Bikin User Pribadimu (Biar Tampilan User bukan Root Terus!):**
    ```bash
    proot-distro login debian
    ```
    Nah, sekarang kamu udah di 'dalam' Debian. Kita pasang `sudo` dan bikin user baru, misalnya `sheetizen` (ganti sesukamu ya!):
    ```bash
    apt update -y
    apt upgrade -y
    apt install sudo
    apt install sudo nano adduser -y
    adduser sheetizen 
    ```
    Nanti ada pertanyaan-pertanyaan, ikutin aja buat bikin password user barumu.
    Kalau mau simpel, tinggal ENTER-ENTER aja.

* **Kasih 'Kekuatan Super' (Sudo) ke User Barumu:**
    Masih di dalam Debian, kita edit file `sudoers` pakai `nano` (editor teks di terminal):
    ```bash
    nano /etc/sudoers
    ```
    Scroll ke bawah, cari baris `root ALL=(ALL:ALL) ALL`. Tepat di bawahnya, ketik:
    ```
    sheetizen ALL=(ALL:ALL) ALL
    ```
    Ingat, ganti `sheetizen` dengan username yang tadi kamu buat.
    Buat simpan, tekan `Ctrl+X`, terus `Y`, lalu `Enter`. Beres!

* **Logout & Login Lagi Pakai User Jagoanmu:**
    Ketik `exit` buat keluar dari sesi root Debian.
    Sekarang, login lagi pakai user barumu yang udah punya kekuatan sudo:
    ```bash
    proot-distro login debian --user sheetizen
    ```
    Tes kekuatan: `sudo whoami`. Kalau yang muncul `root`, selamat! Kamu udah jadi admin di Debian-mu! 🎉

---

## ✨ Langkah 3: Pasang XFCE4 (untuk tampilin mode Desktop) + Buat Shortcut biar Praktis!

XFCE4 ini Desktop Environment yang ringan tapi tetep fungsional. Cocok buat HP atau tab untuk keseharian!

* **Login ke Debian (kalau kamu lagi di luar - taunya cek aja kalau kodenya `$`, kamu ketikkan command ini. Tapi kalau awalannya `username@localhost` contoh `sheetizen@localhost`, lewati langkah ini):**
    Di Termux, panggil:
    ```bash
    proot-distro login debian --user sheetizen
    ```

* **Install XFCE4, Si Ringan Nan Gesit:**
    Di dalam Debian (sebagai `sheetizen` kodenya di awal termux `sheetizen@localhost`), eksekusi:
    ```bash
    sudo apt install xfce4 -y
    ```
    Sabar ya, biarkan dia download dan install semua paketnya.
    Kataku sambil NGOPI aja.
    Kalau ada pertanyaan soal layout keyboard, pilih aja yang paling kamu nyaman, aku pakai 1 sih, biar gampang hehehe.

* **Install GNOME, Biar Debianmu makin FullPower**
  Setelah selesai install xfce4, kita install juga GNOME biar debianmu lebih jos lagi.
    ```bash
    sudo apt install dbus-x11 nano gnome gnome-shell gnome-terminal gnome-tweaks gnome-software nautilus gnome-shell-extension-manager gedit tigervnc-tools gnupg2 -y
    ```
    
* **Balik Dulu ke Termux:**
    Ketik `exit`.
    
* **Download Script Shortcut Ajaib buat XFCE4:**
    Ini nih 'jalan pintasnya'.
    Aku pakai repo dari Droidmaster
    Stemasih di Termux biasa:
    ```bash
    wget [https://raw.githubusercontent.com/LinuxDroidMaster/Termux-Desktops/main/scripts/proot_debian/startxfce4_debian.sh](https://raw.githubusercontent.com/LinuxDroidMaster/Termux-Desktops/main/scripts/proot_debian/startxfce4_debian.sh)
    ```

* **‼️ SUPER PENTING: Edit Script Shortcutnya!**
    Script `startxfce4_debian.sh` itu bawaannya pakai user `droidmaster`. Kita harus ganti jadi username kamu (`sheetizen` atau apapun itu). Pakai `nano` aja di Termux, caranya:
    ```bash
    nano startxfce4_debian.sh
    ```
    Cari semua kata `droidmaster` di situ, terus ubah jadi username-mu. Kalau udah, simpan!
    *(Nanti di Langkah 3 kita bahas cara edit pakai FX File Explorer)*

---

## ✏️ Langkah 3: Oprek Shortcut & Simpan ke 'Penyimpanan' Widget!

Ikuti aja yang ada di video, ya! heheheh

* **Edit Scriptnya Pakai FX File Explorer (Ini juga masih sama):**
    1.  Buka FX File Explorer, navigasi ke "Internal Storage" (atau folder `shared` tadi), cari file `startxfce4_debian.sh`.
    2.  Tekan lama filenya, pilih "Open with...", lalu "Text Editor".
    3.  **WAJIB:** Ganti semua `username` jadi username-mu (misal `sheetizen`).
    4.  Simpan perubahannya.

* **Saatnya Pindahin Script ke 'Brankas' Widget Pakai FX File Explorer! (Ini Bagian yang Diubah)**
    1.  **Buka FX File Explorer.**
    2.  **Akses Penyimpanan Termux:** Di FX File Explorer, cari fitur "Connect to Storage", lalu pilih "Termux" dari daftar penyimpanan yang muncul. Tujuannya adalah kamu bisa melihat isi folder *home* Termux (yang path aslinya kira-kira `/data/data/com.termux/files/home/`).
    3.  **Buat Folder `.shortcuts` (Kalau Belum Ada):** Setelah kamu berada di dalam direktori *home* Termux via FX, cek apakah sudah ada folder bernama `.shortcuts`. Ingat, ada titik di depannya, jadi ini folder tersembunyi. Mungkin kamu perlu aktifkan opsi "Show hidden files" di pengaturan FX File Explorer. Kalau folder `.shortcuts` belum ada, buat folder baru di lokasi ini menggunakan fitur "New Folder" di FX dan kasih nama persis `.shortcuts`.
    4.  **Copy Script Jagoanmu:** Sekarang, di FX File Explorer, navigasi kembali ke tempat kamu menyimpan script yang sudah diedit (misalnya di "Internal Storage" / folder `shared`, nama filenya `startxfce4_debian.sh`). Tekan lama pada file script tersebut, lalu pilih "Copy".
    5.  **Paste dan Ganti Nama di Folder `.shortcuts`:** Kembali lagi navigasi (masih di FX File Explorer) ke dalam folder `.shortcuts` yang ada di direktori *home* Termux tadi. "Paste" script yang sudah kamu copy ke dalam folder ini. Setelah berhasil di-paste, tekan lama lagi pada file script yang baru saja di-paste tersebut, lalu pilih "Rename". Kasih nama yang kece dan mudah diingat buat nanti muncul di widget, misalnya `MulaiXFCE4Ku`.
    6.  **‼️ SUPER PENTING (Kembali ke Termux Sebentar!):** Nah, ini dia langkah krusial yang *tetap harus* dilakukan lewat Termux. Script kamu butuh izin eksekusi biar bisa 'lari' pas diklik dari widget. Buka aplikasi Termux-mu, lalu ketik perintah sakti ini:
        ```bash
        chmod +x ~/.shortcuts/startxfce4_debian.sh
        ```
        (Jangan lupa, ganti `startxfce4_debian.sh` dengan nama file persis yang kamu pakai di folder `.shortcuts` tadi). Tanpa ini, script-nya gak bakal bisa jalan dari widget!
---

## 📲 Langkah 4: Pasang 'Tombol Ajaib' Termux:Widget!

* **Install Termux:Widget:**
    Ini aplikasi pendamping Termux. Download APK-nya dari F-Droid atau rilis GitHub Termux.

* **Sulap Jadi Widget di Homescreen:**
    1.  Tekan lama di area kosong homescreen HP-mu.
    2.  Pilih "Widget" atau "Tambahkan Widget".
    3.  Cari "Termux" atau "Termux:Widget".
    4.  Seret dan letakkan widgetnya di homescreen.

---

## 🚀 Langkah 6: Wusshh! Jalankan Desktop via Widget!

Ini dia momen yang ditunggu-tunggu!

* Widget Termux di homescreen-mu sekarang bakal nampilin daftar script dari folder `~/.shortcuts/`.
* Lihat kan ada `startxfce4_debian.sh` (atau nama apapun yang kamu kasih tadi)?
* **SUPER PENTING LAGI:** Sebelum nge-klik tombol di widget, **PASTIKAN APLIKASI TERMUX X11 SUDAH TERBUKA** di background.
* Udah siap? Klik nama script di widget itu!
* Dan... *jeng jeng jeng!* Desktop Linux-mu bakal nongol dengan gagahnya! 💪

---

Mantap jiwa! Kamu berhasil menyulap HP Android-mu jadi mesin Linux yang lebih powerful! Kalau ada yang bikin bingung atau mau didiskusikan, jangan sungkan ya! Selamat ngoprek lebih lanjut! 🔥

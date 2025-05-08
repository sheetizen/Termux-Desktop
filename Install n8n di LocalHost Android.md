# 🚀 Panduan Seru: Pasang n8n di 'Rumah' Debian HP Android-mu!

Halo, teman ngoprek! 👋 Siap bikin HP Android-mu makin cerdas dengan n8n? n8n ini 'otak' buat bikin macem-macem aplikasi dan layanan ngobrol dan kerja bareng secara otomatis. Keren banget buat kamu yang suka efisiensi!

Di panduan ini, aku bakal tuntun kamu pasang n8n di lingkungan Debian yang udah kita sulap di Termux. Prosesnya seru dan dijamin HP-mu makin fullpower!

### Tutorial dalam bentuk Video
[Tutorial install n8n di Android (Localhost)](https://youtu.be/N0EJrw_GFz0?si=vt71vLM858RPsLmi)


---

## ⚙️ Langkah-Langkah Instalasi n8n di Debian (via Termux Proot-Distro)
Untuk install n8n, pastikan kamu memasukkan command di Debian, ya.

Kalau belum install Debian di Termux, bisa ikutin langkah berikut ini 👇

[Cara install Debian di link ini](https://github.com/sheetizen/Termux-Desktop/blob/main/InstallDebian.md)

### 👋 Masuk Dulu ke `rumah` Debian-mu:
   
Pastikan kamu udah login ke Debian sebagai user pribadimu ya (yang `sheetizen` atau usernamemu)
   
Kalau kamu mau ngejalanin perintah atau script yang butuh waktu lama, sebelum mulai, ketik ini di Termux:
    ```
    proot-distro login debian --user sheetizen
    ```
    (Jangan lupa, ganti `sheetizen` dengan username Debian yang udah kamu buat sebelumnya ya!)

### 🛠️ Siapin Node.js, npm, dan Kawan-Kawannyw
     
`nyawa` n8n ini bergantung sama Node.js, dan dia paling seneng sama versi LTS (Long Term Support) yang cukup update. Kita bakal pasang Node.js versi 20.x, yang sekarang ini jadi salah satu pilihan LTS paling stabil dan sangat direkomendasikan buat n8n.
* Tapi update dulu
      ```
      sudo apt update
      sudo apt upgrade -y
      ```
* Node.js (Namanya NodeSource) biar Dapetin Versi 20.x yang Paling Oke
    ```
    sudo apt install -y curl gnupg
    ```

* Terus kita ambil dari web resminya
  ```
    curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
    ```
  
* Install NodeJs
    ```
    sudo apt install -y nodejs
    ```
  
* Tes Dulu Biar Hati Tenang dan Gak Was-Was, Versi Node.js dan npm yang terinstall
    ```bash
    node -v
    npm -v
    ```  

### ⚙️ Instalasi n8n
Setelah semua 'alat tempur' dan 'bahan baku' utama siap, sekarang saatnya kita panggil dan install n8n secara global (artinya, n8n bisa kamu 'panggil' dari direktori mana aja di dalam Debian-mu) menggunakan npm.
  ```bash
  sudo npm install -g n8n
  ```

Sabar ya, boleh banget sambil seruput kopi, teh, atau cemilan favoritmu! ☕🍪

### 🚀 Waktunya Jalanin n8n!
Kalau proses instalasi tadi berjalan mulus tanpa ada pesan error merah-merah yang bikin panik, kamu bisa langsung 'nyalain' mesin n8n-mu dengan mengetik perintah simpel ini di terminal Debian-mu:
```bash
n8n
```

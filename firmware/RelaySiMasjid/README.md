# RelaySiMasjid - Modul Kontrol Relay IoT

`RelaySiMasjid` adalah firmware untuk perangkat ESP32 yang berfungsi sebagai modul kontrol relay cerdas. Proyek ini dirancang untuk menjadi bagian dari ekosistem **Aplikasi SIMasjid**, memungkinkan kontrol perangkat elektronik seperti amplifier sound system secara otomatis melalui jaringan WiFi.

Modul ini dapat menerima perintah untuk menyalakan atau mematikan relay dari aplikasi utama SIMasjid, sehingga amplifier bisa aktif secara otomatis saat Murottal atau kajian diputar, dan mati saat selesai.

---

## 🌟 Fitur Utama

- **Konfigurasi via Web:** Pengaturan awal yang mudah melalui portal web (Captive Portal) tanpa perlu mengubah kode.
- **Mode Ganda:**
  - **Mode AP (Access Point):** Untuk setup pertama kali, perangkat akan membuat hotspot WiFi bernama `SIMasjid-IoT-Setup`.
  - **Mode Station:** Mode operasi normal, di mana perangkat terhubung ke jaringan WiFi masjid.
- **Kontrol Fleksibel:**
  - **API Sederhana:** Kontrol relay melalui endpoint HTTP (`/on` dan `/off`) yang mudah diintegrasikan.
  - **Dashboard Web:** Halaman dashboard untuk kontrol manual, melihat status, dan mengubah konfigurasi.
- **Konfigurasi Dinamis:**
  - **Pemilihan Pin GPIO:** Pilih pin GPIO mana saja yang terhubung ke modul relay melalui antarmuka web.
  - **Mode Aktif Relay:** Mendukung relay *Active HIGH* dan *Active LOW* yang dapat diatur sesuai kebutuhan.
- **Penyimpanan Permanen:** Semua pengaturan (WiFi, pin, mode relay) disimpan di memori internal (NVS), sehingga tidak hilang saat listrik padam.
- **Reset Pabrik:** Opsi untuk menghapus semua pengaturan dan kembali ke mode setup awal melalui dashboard.

---

## 🛠️ Perangkat Keras yang Dibutuhkan

1.  **ESP32 Development Board:** Model apa saja (misal: ESP32-DevKitC, Wemos D1 R32).
2.  **Modul Relay 1 Channel:** Pastikan kompatibel dengan level tegangan 3.3V dari ESP32.
3.  **Adaptor Daya:** 5V Micro-USB atau sesuai dengan input daya board ESP32 Anda.
4.  **Kabel Jumper:** Untuk menghubungkan ESP32 ke modul relay.

---

## 🚀 Cara Penggunaan

### 1. Flash Firmware

- Buka proyek ini menggunakan **PlatformIO** di Visual Studio Code.
- Hubungkan board ESP32 Anda ke komputer.
- Upload firmware ke board ESP32.

### 2. Konfigurasi Pertama Kali (Mode AP)

1.  Nyalakan perangkat ESP32.
2.  Pada HP atau laptop Anda, cari dan hubungkan ke jaringan WiFi dengan nama **`SIMasjid-IoT-Setup`**.
3.  Setelah terhubung, halaman konfigurasi (Captive Portal) akan otomatis terbuka di browser. Jika tidak, buka browser secara manual dan akses alamat `http://192.168.4.1`.
4.  Pada halaman tersebut, isi formulir:
    - **Nama Wi-Fi (SSID):** Masukkan nama WiFi masjid Anda.
    - **Kata Sandi:** Masukkan password WiFi masjid.
    - **Pin Relay (GPIO):** Masukkan nomor pin GPIO pada ESP32 yang Anda hubungkan ke pin `IN` pada modul relay (contoh: `2`).
    - **Mode Aktif Relay:** Pilih `Active HIGH` atau `Active LOW` sesuai spesifikasi relay Anda.
5.  Klik **"Simpan & Restart"**. Perangkat akan menyimpan konfigurasi dan mencoba terhubung ke WiFi masjid.

### 3. Penggunaan Normal (Mode Station)

- Setelah restart, perangkat akan terhubung ke WiFi yang telah Anda konfigurasikan.
- Alamat IP perangkat akan ditampilkan di **Serial Monitor** Arduino IDE atau PlatformIO.
- Anda sekarang dapat mengontrol relay melalui beberapa cara:

#### A. Melalui Aplikasi SIMasjid
Aplikasi utama akan mengirim perintah ke endpoint API perangkat ini.

#### B. Melalui Dashboard Web
- Buka browser dan akses alamat IP perangkat (contoh: `http://192.168.1.15`).
- Di halaman dashboard, Anda bisa:
  - Menyalakan/mematikan relay secara manual.
  - Melihat status koneksi dan konfigurasi saat ini.
  - Mengubah konfigurasi WiFi, pin, atau mode relay.
  - Melakukan reset pabrik.

#### C. Melalui API Langsung
Anda bisa mengirim request HTTP langsung ke perangkat.

- **Nyalakan Relay:**
  ```
  http://<IP_PERANGKAT>/on
  ```
- **Matikan Relay:**
  ```
  http://<IP_PERANGKAT>/off
  ```

---

*© 2024 Yusuf Faisal | Devlover. Bagian dari Proyek SIMasjid.*
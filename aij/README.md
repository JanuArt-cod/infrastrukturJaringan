# 📘 Menganalisis Permasalahan Routing Statis

## 🧠 Pengertian Routing Statis

Routing statis adalah metode routing di mana administrator jaringan secara manual memasukkan rute ke dalam tabel routing perangkat jaringan (router). Rute ini bersifat tetap dan tidak berubah otomatis, hanya dapat diperbarui secara manual.

---

## ❗ Permasalahan Umum pada Routing Statis

| No | Permasalahan                        | Penjelasan                                                                 |
|----|-------------------------------------|----------------------------------------------------------------------------|
| 1  | Alamat tujuan atau subnet salah     | Router tidak dapat mengirim paket ke alamat yang tidak dikenali.           |
| 2  | Next hop tidak sesuai               | Router mengirim ke arah yang salah atau ke perangkat yang tidak aktif.     |
| 3  | Antarmuka (interface) down          | Router tidak dapat mengirim paket melalui interface yang mati atau error.  |
| 4  | Konfigurasi tidak disimpan          | Setelah restart, semua pengaturan hilang karena belum disimpan.            |
| 5  | Tidak semua jalur dikonfigurasi     | Paket hanya bisa ke sebagian jaringan, lainnya tidak dapat dijangkau.      |
| 6  | Tidak ada gateway default (jika perlu) | Router tidak tahu harus mengirim ke mana jika tujuan tidak dikenali.       |

---

## 🔎 Langkah-Langkah Analisis Masalah Routing Statis

1. **Cek Konektivitas:**
   - Gunakan perintah `ping` ke alamat tujuan.
   - Gunakan `traceroute` atau `tracert` untuk melihat jalur yang ditempuh paket.

2. **Periksa Tabel Routing:**
   ```bash
   show ip route
   ```
3. **Cek Konfigurasi Routing:**
   ```bash
   show running-config
   ```
4. **Periksa Status Interface:**
   ```bash
   show ip interface brief
   ```
5. **Pastikan Semua Jaringan Sudah Terhubung:**
   - Pastikan konfigurasi IP setiap perangkat benar.
   - Pastikan semua interface router aktif (up/up).
     
## 💡 Contoh Kasus
Topologi sederhana:
  ```bash
  PC1 -- R1 -- R2 -- PC2
  ```
 - PC1: 192.168.10.2/24
 - R1 ke R2: 192.168.12.1 ↔ 192.168.12.2
 - PC2: 192.168.20.2/24
**Jika PC1 tidak bisa ping ke PC2, periksa:**
 - Apakah R1 tahu ke mana harus mengirim paket ke 192.168.20.0?
 - Apakah R2 punya route balik ke 192.168.10.0?
 - Apakah semua interface aktif?

# M Gibran Khalilullah - 103072400035 - IF0405

# MODUL 11 : DHCP
## DHCP
DHCP merupakan sebuah protokol dalam jaringan yang berfungsi untuk mendistribusikan konfigurasi jaringan ke perangkat klien secara otomatis. Melalui sistem ini, perangkat yang baru terhubung bisa langsung mendapatkan IP address, subnet mask, gateway, hingga DNS server tanpa perlu melakukan penyetingan secara manual.

## Kelebihan DHCP
- Otomatis & Efisien: Mempercepat proses distribusi IP address ke perangkat klien secara otomatis.

- Manajemen Praktis: Memudahkan beban kerja administrator jaringan dalam mengelola dan mengontrol alokasi IP.

- Bebas Konflik IP: Meminimalkan risiko bentrokan (IP conflict) akibat penggunaan alamat IP yang sama oleh dua perangkat berbeda.

- Akurasi Konfigurasi: Mengurangi potensi kesalahan manusia (human error) saat memasukkan konfigurasi jaringan.

- Skalabilitas Tinggi: Sangat ideal dan efisien jika diterapkan pada jaringan berskala besar dengan banyak pengguna.

## Kekurangan DHCP
1. Pelacakan Lebih Rumit: Identifikasi perangkat menjadi lebih menantang karena alamat IP klien bisa berubah sewaktu-waktu (bersifat dinamis).
2. Ketergantungan pada Server: Jika pusat data atau server DHCP mengalami gangguan (down), seluruh perangkat klien baru tidak akan bisa terhubung ke jaringan.
3. Butuh Setup Tambahan: Diperlukan konfigurasi dan pemeliharaan ekstra pada sisi server agar performanya tetap optimal.
4. Butuh Setup Tambahan: Diperlukan konfigurasi dan pemeliharaan ekstra pada sisi server agar performanya tetap optimal.

## Proses DORA
DORA merupakan tahapan komunikasi antara client dan server DHCP untuk memperoleh IP address secara otomatis. DORA terdiri dari Discover, Offer, Request, dan Acknowledgement (ACK).

**Langkah-langkah**
1. Download dan ekstrak file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip
2. Buka file DHCP menggunakan Wireshark
4. Gunakan filter dhcp untuk menampilkan paket DHCP saja
  <img width="1024" height="295" alt="dhcp" src="https://github.com/user-attachments/assets/d447097f-4020-46a6-8025-5136c36c4432" />

**Tahapan Dora**
1. Discover

   Pada baris satu, dapat dilihat client mengirimkan pesan DHCP Discover untuk mencari server DHCP yang tersedia pada jaringan. IP source masih 0.0.0.0 karena perangkat belum memiliki IP address. Paket dikirim secara broadcast agar dapat diterima oleh seluruh server DHCP dalam jaringan.

2. Offer

   Pada baris kedua server DHCP yang menerima pesan Discover akan mengirimkan DHCP Offer. Pesan ini berisi penawaran IP address beserta konfigurasi jaringan lain yang dapat digunakan oleh client.

3. Request

   Pada baris ketiga client memilih salah satu penawaran dari server DHCP, kemudian mengirimkan DHCP Request sebagai tanda bahwa client menerima IP address yang ditawarkan.

4. Acknowledgement (ACK)

   Pada baris keempat server DHCP mengirimkan DHCP ACK untuk mengonfirmasi bahwa IP address telah resmi diberikan kepada client. Tahap ini merupakan proses finalisasi sehingga client dapat mulai menggunakan jaringan.

# Jaringan Komputer 13

## Modul 2: Pengenalan Tools

### Tujuan Praktikum

1. Mahasiswa dapat melakukan instalasi tool yang digunakan (Wireshark).
2. Mahasiswa dapat menggunakan tool (Wireshark) untuk menangkap dan mengidentifikasi paket data.

---

### 2.1 Pengantar

Pemahaman protokol jaringan dapat diperdalam dengan mengamati protokol “beraksi” dan mengeksplorasi urutan pesan yang saling bertukar antara dua entitas. Praktikum ini menggunakan Wireshark untuk mengamati protokol jaringan komputer berinteraksi dan bertukar pesan.

Wireshark adalah aplikasi Packet Sniffer yang menangkap pesan yang dikirim/diterima oleh komputer Anda. Packet Sniffer bersifat pasif, hanya mengamati pesan tanpa mengirim atau menerima paket itu sendiri. Wireshark terdiri dari dua bagian utama:

- **Packet Capture Library**: Menerima salinan setiap frame link layer yang dikirim/diterima komputer melalui antarmuka (Ethernet/WiFi).
- **Packet Analyzer**: Menampilkan isi semua bidang dalam pesan protokol.

Wireshark memungkinkan analisis berbagai protokol (HTTP, FTP, TCP, UDP, DNS, IP) yang dikemas dalam frame link layer.

---

### 2.2 Wireshark

Wireshark adalah penganalisa protokol jaringan gratis untuk Windows, Mac, dan Linux/Unix. Wireshark menggunakan packet capture library (lhark.org/download.html).

---ibpcap/WinPCap) untuk menangkap frame link layer. Unduh dan instal Wireshark dari [http://www.wireshark.org/download.html](http://www.wireshark.org/download.html).

---

### 2.3 Menjalankan Wireshark

Saat menjalankan Wireshark, tampilan awal akan menunjukkan daftar interfaces di bawah bagian Capture. Pilih interface (misal Wi-Fi/Ethernet) untuk mulai menangkap paket.

![Wireshark Welcome Screen](images/wireshark-welcome.png)

Antarmuka Wireshark terdiri dari lima komponen utama:

- **Command Menu**: Menu pull-down standar di bagian atas.
- **Packet-listing Window**: Ringkasan satu baris untuk setiap paket yang diambil.
- **Packet-header Details Window**: Rincian tentang paket yang dipilih.
- **Packet-contents Window**: Isi frame dalam format ASCII dan heksadesimal.
- **Packet Display Filter Field**: Menyaring informasi yang ditampilkan.

---

### 2.4 Menggunakan Wireshark Untuk Test Run

1. Jalankan browser web Anda.
2. Jalankan Wireshark, pilih interface untuk mulai menangkap paket.
3. Mulai pengambilan paket pada interface yang diinginkan.
4. Setelah pengambilan paket dimulai, gunakan browser untuk mengakses URL:  
   `http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html`
5. Setelah halaman tampil, hentikan pengambilan paket di Wireshark.

![Wireshark Packet Capture](images/wireshark-capture.png)

6. Ketik `http` pada filter display untuk menampilkan hanya paket HTTP.
7. Temukan pesan HTTP GET ke server `gaia.cs.umass.edu` di daftar paket.
8. Maksimalkan informasi protokol HTTP di jendela detail paket.
9. Keluar dari Wireshark.

---

> **Referensi:**
>
> - [Wireshark User Guide](http://www.wireshark.org/docs/wsug_html_chunked/)
> - [Wireshark FAQ](http://www.wireshark.org/faq.html)

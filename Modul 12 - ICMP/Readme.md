# M Gibran Khalilullah - 103072400035 - IF0405

# MODUL 12 : ICMP
## ICMP
ICMP (Internet Control Message Protocol) adalah protokol jaringan yang digunakan untuk mengirim pesan kontrol, informasi, atau laporan kesalahan (error reporting) dalam komunikasi jaringan IP.

**Fungsi ICMP**
1. Mendiagnosis jaringan : membantu mengetahui apakah koneksi jaringan berjalan dengan baik
2. Mengecek kondisi jaringan : memeriksa apakah host atau perangkat tujuan dapat dijangkau

**ICMP digunakan untuk**
1. Mengecek host dalam jaringan : contohnya menggunakan perintah ping untuk mengetahui apakah suatu host aktif
2. Mengetahui hop/jalur perjalanan paket : contohnya menggunakan traceroute/tracert untuk melihat jalur paket data
3. Memberikan informasi error : memberi tahu jika terjadi masalah pengiriman data, misalnya tujuan tidak dapat dijangkau

**Hubungan IP dengan ICMP**

ICMP bekerja bersama protokol IP. Saat IP mengirim data, ICMP berada di dalam payload paket IP untuk membawa pesan kontrol atau informasi error. Jadi, ICMP tidak menggantikan IP, tetapi membantu IP dalam proses komunikasi jaringan.

**Isi paket ICMP**
1. Type : menunjukkan jenis pesan ICMP
2. Code : memberikan detail tambahan dari jenis pesan ICMP
3. Checksum : digunakan untuk mengecek apakah paket mengalami error atau tidak
4. Identifier : penanda untuk membedakan paket ICMP
5. Sequence Number : menunjukkan urutan paket yang dikirim

## Analisis ICMP yang Dihasilkan Oleh Ping
1. Bukak wireshark dan pilih salah satu jaringan (Wifi), lalu aktifkan / capture
2. Buka CMD, kemudian ketikan perintah ping www.ust.hk
   <img width="726" height="335" alt="image" src="https://github.com/user-attachments/assets/8b0190da-ac65-4113-95f0-8891e8596e0f" />
3. Stop capture pada wireshark
4. Lakukan filter ICMP
5. Pilih dan expand salah satu paket ICMP Echo Request
6. Pilih dan expand salah satu paket ICMP Echo Reply

**Analisis**
- Pesan ICMP yang dihasilkan program Ping
  <img width="975" height="573" alt="image" src="https://github.com/user-attachments/assets/eb26212a-0d00-4c9d-ae52-3e19d02ddedd" />
  Program ping menghasilkan dua jenis pesan ICMP yaitu ICMP Echo Request dan ICMP Echo Reply. Pada percobaan ini, perintah di CMD (-n 10) menyatakan untuk melakukan 10 kali ping. Karena setiap ping menghasilkan 1 echo request dan 1 echo reply, maka total paket ICMP yang muncul di wireshark adalah 20 paket (10 request + 10 reply)
- Format dan Isi Pesan ICMP
  1. ICMP Echo Request
     <img width="944" height="266" alt="image" src="https://github.com/user-attachments/assets/0040a069-e453-4216-8342-1d1725ed40c2" />
     - Type = 8 -> menandakan paket adalah Echo Request atau permintaan ping
     - Code = 0 -> menunjukkan tidak ada detail error tambahan pada pesan ICMP tersebut
     - Checksum = 0x4d4c [correct] -> checksum valid sehingga paket tidak mengalami kerusakan/error saat dikirim
     - Identifier = 1 (0x0001) -> digunakan sebagai penanda agar Echo Reply dapat dikenali sebagai balasan dari request yang sama
     - Sequence Number = 15 (0x000f) -> menunjukkan bahwa paket ini merupakan urutan ping ke-15 yang dikirim
  2. ICMP Echo Reply
     <img width="945" height="299" alt="image" src="https://github.com/user-attachments/assets/8e97033d-07b9-4f61-88b5-949fcacde999" />
     - Type = 0 -> menunjukkan bahwa paket merupakan Echo Reply atau balasan ping
     - Code = 0 -> tidak terdapat informasi tambahan atau error pada paket balasan
     - Checksum = 0x554c [correct] -> checksum valid sehingga paket reply diterima tanpa kerusakan data
     - Identifier = 1 (0x0001) -> identifier sama dengan paket request agar sistem dapat mencocokkan balasan dengan permintaan sebelumnya
     - Sequence Number = 15 (0x000f) -> menunjukkan bahwa paket reply ini merupakan balasan untuk paket request urutan ke-15

## Analisis ICMP yang Dihasilkan Oleh Traceroute
1. Bukak wireshark dan pilih salah satu jaringan (Wifi), lalu aktifkan / capture
2. Buka CMD, kemudian ketikan perintah tracert www.ust.hk
  <img width="725" height="389" alt="image" src="https://github.com/user-attachments/assets/bdf80da9-b41b-46dc-b364-e165ec2cf3f0" />
3. Stop capture pada wireshark
4. Lakukan filter ICMP
5. Pilih dan expand salah satu paket ICMP Echo Request
6. Pilih dan expand salah satu paket Time To Live (TTL)

**Analisis**
- Pesan ICMP yang dihasilkan oleh program tracerout
  <img width="1049" height="595" alt="image" src="https://github.com/user-attachments/assets/1009e434-c293-40ba-8274-bd6796660bb2" />
  1. ICMP Echo Request : Paket ini digunakan untuk meminta respon dari host atau router yang dilewati
  2. ICMP Time Exceeded (TTL Expired) : pesan yang dikirim oleh router ketika nilai TTL pada suatu paket habis sebelum paket mencapai tujuan
- Format dan Isi Pesan ICMP
  1. ICMP Echo Request
      <img width="1024" height="576" alt="gambarpen" src="https://github.com/user-attachments/assets/0cf42cb5-4f57-4ebd-b600-7a40f6b63b20" />
     - Type = 8 -> menunjukkan paket merupakan Echo Request atau permintaan ping
     - Code = 0 -> tidak terdapat informasi tambahan/error pada paket
     - Checksum = 0xf7e5 [correct] -> checksum valid sehingga paket tidak mengalami kerusakan saat transmisi
     - Identifier = 1 (0x0001) -> digunakan sebagai penanda paket request
     - Sequence Number = 25 (0x0019)-> menunjukkan bahwa paket ini merupakan paket urutan ke-25
  2. ICMP Time Exceeded
     <img width="1049" height="329" alt="image" src="https://github.com/user-attachments/assets/5c8379a3-3d95-42ae-8499-9b2bd46ad149" />
     - Type = 11 -> menunjukkan paket merupakan Time Exceeded
     - Code = 0 -> berarti TTL exceeded in transit, yaitu TTL habis di perjalanan
     - Checksum = 0xf4ff [correct] -> menandakan paket diterima tanpa error
     - Source IP = 10.218.0.253 -> router yang mengirim pesan TTL exceeded
     - Destination IP = 10.218.10.188 -> Host pengirim traceroute
     

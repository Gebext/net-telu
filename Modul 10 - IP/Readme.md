# M Gibran Khalilullah - 103072400035 - IF0405

# MODUL 10 : IP
## IP
IP Address (Internet Protocol Address) adalah alamat unik yang digunakan untuk mengidentifikasi perangkat dalam jaringan, baik di internet maupun jaringan lokal. IP address berfungsi seperti “alamat rumah” supaya data bisa dikirim ke tujuan yang benar.

**Jenis-jenis**
- IPv4 : menggunakan 32-bit (contoh: 192.168.1.1)
- IPv6 : menggunakan 128-bit (contoh: 2001:db8::1)

**Cara menghitung**

IPv4 terdiri dari 4 oktet (masing-masing 8 bit) ex : 192.168.1.1
- 192 = 11000000
- 168 = 10101000
- 1 = 00000001

Subnetting digunakan untuk membagi jaringan menjadi Network ID (identitas jaringan) dan Host ID (identitas perangkat).

**Mengamati IP Address**
1. Buka CMD
2. Ketik ip r, atau ip a
 <img width="2108" height="673" alt="image" src="https://github.com/user-attachments/assets/99aff4b6-b155-4824-b84d-d7354720116b" />

Perangkat menggunakan alamat IP 172.20.10.3 dengan prefix /28 pada interface wlp62s0. Subnet mask yang digunakan adalah 255.255.255.240. Network ID dari jaringan tersebut adalah 172.20.10.0 dengan jumlah host yang dapat digunakan sebanyak 14 perangkat. Default gateway yang digunakan adalah 172.20.10.1 sebagai penghubung ke jaringan lain maupun internet. Selain itu, perangkat juga memiliki alamat IPv6 link-local yaitu fe80::607b:f19e:b82e:3a15/64 yang digunakan untuk komunikasi lokal dalam satu segmen jaringan.

## Traceroute
Traceroute adalah teknik untuk mengetahui jalur yang dilewati paket data dari komputer kita menuju suatu tujuan (misalnya website).

**Fungsi Traceroute**
- Menampilkan router (hop) yang dilewati
- Mengetahui waktu tempuh tiap hop
- Mendeteksi gangguan jaringan

**Mengamati Traceroute dari suatu Website**
1. Buka CMD
2. Ketik tracert google.com
3. <img width="2108" height="673" alt="image" src="https://github.com/user-attachments/assets/cac9d253-b34d-4f72-a58a-ba319de476a2" />
ket data melewati 13 hop (router) sebelum mencapai jaringan tujuan Google. Hop 1 merupakan router lokal atau gateway Wi-Fi yang digunakan. Hop 2–4 masih berada pada jaringan internal ISP dengan alamat IP privat (10.x.x.x). Mulai hop 5 paket memasuki jaringan publik dan backbone internet. Pada hop 5–13 terlihat paket telah melewati beberapa router milik Google yang ditandai dengan domain 1e100.net dan alamat IP yang terasosiasi dengan jaringan Google.

Tanda (*) pada hop 8 dan 13 menunjukkan bahwa router tersebut tidak memberikan respons terhadap paket traceroute (ICMP Time Exceeded), namun tetap meneruskan paket ke tujuan berikutnya. Hal ini merupakan perilaku yang umum dan tidak selalu menunjukkan adanya gangguan jaringan.

Waktu tempuh (latency) yang terukur berkisar antara 3 ms hingga 80 ms, dengan sebagian besar hop berada pada rentang 38–70 ms. Nilai tersebut masih tergolong baik untuk akses internet umum dan menunjukkan bahwa koneksi jaringan berada dalam kondisi normal. Berdasarkan hasil traceroute ini, jalur komunikasi menuju server Google dapat dicapai dengan stabil tanpa indikasi kehilangan konektivitas yang signifikan.

## IMCP, MTU, TTL
**IMCP** adalah protokol yang digunakan untuk mengirim pesan kontrol dalam jaringan. ICMP digunakan untuk:
- Mengecek koneksi (ping)
- Mengirim pesan error
- Digunakan pada traceroute

**MTU** adalah ukuran maksimum paket data yang bisa dikirim dalam satu kali transmisi. Contoh: Ethernet -> 1500 byte. Jika paket lebih besar dari MTU akan terjadi fragmentasi.

**TTL** adalah batas jumlah hop (router) yang bisa dilewati paket. Setiap melewati router maka TTL berkurang 1. Jika TTL = 0 maka paket dibuang. TTL digunakan untuk mencegah 
looping jaringan.

## Fragmentasi
Fragmentasi adalah proses pemecahan paket data menjadi beberapa bagian yang lebih kecil karena ukuran paket melebihi MTU (Maximum Transmission Unit) jaringan. Fragmentasi terjadi ketika paket terlalu besar dan melewati jaringan dengan MTU lebih kecil.

**Percobaan Fragmentasi**
1. Jalankan Wireshark pilih interface Wifi yang aktif
2. Klik Start
3. Buka CMD
4. Ketik ping google.com -l 2000 (mengirim paket besar (2000 byte) yg melebihi MTU sehingga memicu fragmentasi)
5. Kembali ke Wireshark, gunakan filter ip.flags.mf == 1 || ip.frag_offset > 0

  <img width="1024" height="225" alt="ss2" src="https://github.com/user-attachments/assets/51387ddf-ea67-4ede-bd74-e0860dfe3701" />

Berdasarkan hasil capture menggunakan Wireshark, ditemukan paket dengan keterangan:

- Fragmented IP protocol (proto=ICMP) yang menunjukkan terjadinya fragmentasi
- Paket memiliki ukuran sebesar 1514 bytes, melebihi batas MTU (±1500 byte)
- Terdapat nilai Identification yang menandakan setiap fragment berasal dari satu paket yang sama
- Nilai Fragment Offset (off=0) menunjukkan urutan fragment pertama
- Ditemukan keterangan Reassembled in #203 yang menunjukkan bahwa fragment berhasil digabung kembali

Sehingga dapat disimpulkan bahwa paket ICMP yang dikirim mengalami fragmentasi karena ukurannya melebihi MTU jaringan.

## IPv6
IPv6 (Internet Protocol version 6) adalah versi terbaru dari IP yang digunakan untuk menggantikan IPv4. Ciri-ciri IPv6 adalah menggunakan 128-bit address dan ditulis dalam bentuk heksadesimal.

**Analisis IPv6 di Wireshark**
1. Membuka file ipv6_sample dengan wireshark 
2. Gunakan filter IPv6

   <img width="1761" height="608" alt="ss" src="https://github.com/user-attachments/assets/0c772ad1-885d-416e-93a4-0f310920d05f" />

Berdasarkan hasil capture menggunakan Wireshark, ditemukan paket dengan protokol IPv6. Hal ini dibuktikan dengan adanya informasi:

- Internet Protocol Version 6 pada detail paket
- Alamat source: 2001:db8:1::10 dan Alamat destination: 2a00:1450:4009:80b::200e
- Alamat tersebut memiliki format heksadesimal dengan tanda titik dua (:) yang merupakan ciri khas IPv6.
- Next Header menunjukkan penggunaan TCP
- Paket dikirim ke port 443 (HTTPS) yang menandakan komunikasi web
- Ditemukan juga TCP Retransmission yang menunjukkan adanya pengiriman ulang paket

Sehingga dapat disimpulkan bahwa komunikasi jaringan menggunakan IPv6 berhasil diamati dan digunakan untuk akses layanan web.

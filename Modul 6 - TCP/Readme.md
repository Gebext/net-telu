# M Gibran Khalilullah - 103072400035 - IF0405

# Modul 6 TCP

# Menangkap Tansfer TCP dalam Jumlah Besar dari Komputer Pribadi ke Remote Server
## Langkah-langkah :

1. Buka file yg ada di Modul Jarkom (http://gaia.cs.umass.edu/wireshark-labs/alice.txt) lalu download file tersebut.

<img width="1920" height="1080" alt="Screenshot From 2026-06-16 12-28-37" src="https://github.com/user-attachments/assets/f7e8f09a-43ea-4f24-9bf6-4d2e7a3a15ed" />


2. lalu buka halaman (http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html), masukan file yg sudah di download

<img width="1010" height="83" alt="Screenshot From 2026-06-16 12-29-08" src="https://github.com/user-attachments/assets/ebc26eb6-c0f4-42b4-b6e0-07aa1bec1356" />

3. Jalankan wireshark, lalu start capture dan kembali ke browser untuk upload file alice.txt. Setelah itu stop capture jika sudah selesai upload.

<img width="1920" height="1080" alt="Screenshot From 2026-06-16 12-28-20" src="https://github.com/user-attachments/assets/846a4210-43c5-465d-9f67-cff13a9062c9" />

4. Lalu ketik di wireshark bagian filter (tcp contains "POST"). untuk menemukan paket upload.

<img width="1018" height="16" alt="image" src="https://github.com/user-attachments/assets/9fb16a7c-ec07-4d40-918f-dcfdd0543ef6" />

## Pertanyaan

1. Berapa alamat IP dan nomor port TCP yang digunakan oleh komputer klien (sumber) untuk mentransfer file ke gaia cs.umass.edu?

<img width="1019" height="109" alt="image" src="https://github.com/user-attachments/assets/c479ef81-dd83-4938-b55e-1a706d802ae3" />

Berdasarkan hasil analisis paket HTTP POST pada Wireshark, komputer klien menggunakan alamat IP 192.168.1.53 dan nomor port 58898 untuk mentransfer file ke server.

2. Apa alamat IP dari gaia.cs.umass.edu? Pada nomor port berapa ia mengirim dan menerima segmen TCP untuk koneksi ini? 

<img width="526" height="117" alt="image" src="https://github.com/user-attachments/assets/ce61c72d-46ac-4b00-a17c-07f268fe4829" />
<img width="579" height="72" alt="image" src="https://github.com/user-attachments/assets/36c60b16-239a-48f4-809d-88771b304621" />

Server gaia.cs.umass.edu memiliki alamat IP 128.119.245.12 dan menggunakan port 80 untuk komunikasi TCP karena menggunakan protokol HTTP.

3. Berapa alamat IP dan nomor port TCP yang digunakan oleh komputer klien Anda (sumber) untuk mentransfer  ke gaia.cs.umass.edu? 

<img width="726" height="194" alt="image" src="https://github.com/user-attachments/assets/138e6e2a-bc7c-4761-be67-5fe5aad47f72" />

Dari hasil capture yg didapatkan pada Wireshark, alamat IP tujuan (gaia.cs.umass.edu) adalah 128.119.245.12. Hasil ini didapat dari nslookup gaia.cs.umass.edu 8.8.8.8, yang menunjukkan alamat IP yang sama. Dengan demikian, alamat IP pada Wireshark sesuai dengan hasil resolusi DNS.

# Uji Coba Dasar TCP

## Langkah-langkah :

1. Download dan extrak file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip

2. Buka file tcp-ethereal-trace-1 dengan wireshark

<img width="1008" height="413" alt="image" src="https://github.com/user-attachments/assets/d6bc8486-a1a5-4036-a75f-932681ac9d49" />

## Pertanyaan

1. Berapa nomor urut segmen TCP SYN yang digunakan untuk memulai sambungan TCP antara komputer klien dan gaia.cs.umass.edu? Apa yang dimiliki segmen tersebut sehingga teridentifikasi sebagai segmen SYN? 

<img width="1005" height="258" alt="image" src="https://github.com/user-attachments/assets/44b70aef-717d-4f3e-a952-b6dc62cf6227" />

Berdasarkan hasil filter menggunakan tcp.flags.syn == 1 && tcp.flags.ack == 0, diperoleh segmen TCP SYN dengan Sequence Number sebesar 0. Segmen ini diidentifikasi sebagai SYN karena memiliki flag SYN = 1 dan ACK = 0, yang menunjukkan bahwa segmen tersebut merupakan awal dari proses pembentukan koneksi TCP (three-way handshake).

2. Berapa nomor urut segmen SYNACK yang dikirim oleh gaia.cs.umass.edu ke komputer klien sebagai balasan dari SYN? Berapa nilai dari field Acknowledgement pada segmen SYNACK? Bagaimana gaia.cs.umass.edu menentukan nilai tersebut? Apa yang dimiliki oleh segmen sehingga teridentifikasi sebagai segmen SYNACK?.

<img width="1011" height="317" alt="image" src="https://github.com/user-attachments/assets/8551215f-ceb2-449b-baf6-9daa4a764048" />

Berdasarkan hasil filter menggunakan tcp.flags.syn == 1 && tcp.flags.ack == 1, diperoleh segmen TCP SYN-ACK dengan Sequence Number sebesar 0 dan Acknowledgement Number sebesar 1. Nilai ACK diperoleh dari Sequence Number segmen SYN sebelumnya yang bernilai 0, kemudian ditambahkan 1. Segmen ini diidentifikasi sebagai SYN-ACK karena memiliki flag SYN = 1 dan ACK = 1, yang menunjukkan bahwa server merespons permintaan koneksi dari klien dalam proses three-way handshake.

3. Berapa nomor urut segmen TCP yang berisi perintah HTTP POST?

<img width="1007" height="316" alt="image" src="https://github.com/user-attachments/assets/01d1d7c9-81f5-46d6-9dc3-1aa067b2fd1b" />

Berdasarkan hasil filter menggunakan tcp.port == 1161 && tcp contains "POST", diperoleh segmen TCP yang berisi perintah HTTP POST dengan Sequence Number sebesar 1. Segmen ini merupakan awal pengiriman data dari klien ke server setelah proses three-way handshake selesai.

4. Hitung RTT, waktu kirim, waktu ACK, dan Estimated RTT

<img width="1011" height="463" alt="image" src="https://github.com/user-attachments/assets/36a9a13e-21f8-4d8b-90f7-dc285f0883ac" />

Berdasarkan hasil analisis menggunakan filter tcp.port == 1161 dan fitur Statistics → TCP Stream Graph → Round Trip Time, diperoleh bahwa nilai RTT (Round Trip Time) berkisar antara sekitar 50 ms hingga 270 ms. Nilai RTT diperoleh dari selisih waktu antara pengiriman segmen TCP oleh klien dan penerimaan acknowledgement (ACK) dari server. Variasi nilai RTT dipengaruhi oleh kondisi jaringan selama proses transmisi data.

5. Berapa panjang setiap enam segmen TCP pertama?

<img width="802" height="190" alt="image" src="https://github.com/user-attachments/assets/13eb8ea9-73ac-4b36-84ef-02a64b7f8718" />

Berdasarkan hasil analisis menggunakan filter tcp.port == 1161, panjang enam segmen TCP pertama diperoleh dari bagian Reassembled TCP Segments, yaitu sebesar 565 byte, 1460 byte, 1460 byte, 1460 byte, 1460 byte, dan 1460 byte. Jika dijumlahkan, total panjang keenam segmen tersebut adalah 7865 byte.

6. Berapa jumlah minimum ruang buffer tersedia yang disarankan kepada penerima dan diterima untuk seluruh trace? Apakah kurangnya ruang buffer penerima pernah menghambat pengiriman?

<img width="501" height="84" alt="image" src="https://github.com/user-attachments/assets/4d8774e4-cd16-4d92-8708-5d7e627ea299" />

Berdasarkan hasil analisis menggunakan filter tcp.port == 1161, nilai minimum ruang buffer (window size) yang diterima adalah sebesar 5840 byte. Nilai ini menunjukkan kapasitas buffer yang tersedia pada sisi penerima. Selama proses transmisi, tidak ditemukan indikasi bahwa kekurangan ruang buffer menghambat pengiriman data, karena tidak terlihat adanya penundaan atau retransmission akibat window yang penuh.

7. Apakah ada segmen yang ditransmisikan ulang dalam file trace?

<img width="1014" height="193" alt="image" src="https://github.com/user-attachments/assets/21ab04d1-172f-48ef-b29b-086b163d31c7" />

Segmen retransmission dicek menggunakan filter tcp.analysis.retransmission pada Wireshark. Berdasarkan hasil filter, tidak ditemukan adanya segmen yang ditransmisikan ulang dalam trace, sehingga dapat disimpulkan bahwa tidak terjadi retransmission selama proses komunikasi TCP.

8. Berapa banyak data yang biasanya diakui oleh penerima dalam ACK? Dapatkah anda mengidentifikasi kasus-kasus di mana penerima melakukan ACK untuk setiap segmen yang diterima?

<img width="1016" height="371" alt="image" src="https://github.com/user-attachments/assets/c386f3a4-96d2-43fc-9c4d-b0c745372629" />

Berdasarkan hasil analisis menggunakan filter tcp.port == 1161 && tcp.flags.ack == 1, terlihat bahwa nilai acknowledgment number meningkat dalam jumlah besar setiap kali ACK dikirim, sehingga menunjukkan bahwa penerima mengakui beberapa segmen sekaligus. Dengan demikian, penerima tidak selalu mengirim ACK untuk setiap segmen, melainkan menggunakan cumulative ACK untuk mengakui data dalam jumlah lebih besar.

9. Berapa throughput (byte yang ditransfer per satuan waktu) untuk sambungan TCP?

<img width="456" height="428" alt="image" src="https://github.com/user-attachments/assets/ad31e03a-ec3a-4cf8-a2f2-e350fd9af80c" />

Throughput koneksi TCP diperoleh menggunakan fitur Statistics → TCP Stream Graph → Throughput pada Wireshark dengan filter tcp.port == 1161. Berdasarkan grafik yang ditampilkan, nilai throughput berada pada kisaran sekitar 200 kbps hingga 260 kbps. Nilai ini menunjukkan jumlah data yang berhasil ditransmisikan per satuan waktu selama proses komunikasi berlangsung.

# Congestion Control Pada TCP

## Langkah-langkah :

1. Identifikasi Slow Start & Congestion Avoidance (file tcp-ethereal-trace-1)
  - Buka file tcp-ethereal-trace-1 dengan wireshark lalu setelah membuka file dalam wireshark filter "TCP"
  - Klik Statistics -> TCP Stream Graph -> Time-Sequence Graph (Stevens)

<img width="998" height="435" alt="image" src="https://github.com/user-attachments/assets/523c0383-3075-4ab6-b3a9-468dc6a9fc04" />

  - Di awal (0–±1 detik) grafik naik cepat, itu fase slow start. Setelah itu berubah jadi naik lebih pelan dan stabil (linear), tandanya masuk congestion avoidance. Grafiknya juga tidak terlalu stabil, kemungkinan karena delay/ACK, tapi secara keseluruhan masih stabil karena tidak ada penurunan tajam.

2. Identifikasi Slow Start & Congestion Avoidance (alice.txt)
  - Buka Wireshark lalu pilih opsi wifi dan start
  - Pada bagian ini sama seperti step yang sudah pernah di lakukan yaitu upload file "alice.txt" ke web http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html
  - Buka wireshark lalu filter "TCP"

<img width="999" height="512" alt="image" src="https://github.com/user-attachments/assets/ec92f4f2-fe7b-4ef6-8302-98964a6b1b14" />

  - Pada grafik kedua, kenaikan sequence number di awal tidak menunjukkan pola yang signifikan dan cenderung datar dalam beberapa waktu. Setelah itu, terjadi peningkatan secara tiba-tiba, sehingga fase slow start tidak terlihat jelas seperti pada grafik sebelumnya.

Perubahan berikutnya juga tidak menunjukkan pola linear yang stabil, melainkan berupa lonjakan-lonjakan. Hal ini mengindikasikan bahwa proses pengiriman data kurang konsisten kemungkinan dipengaruhi oleh variasi delay pada jaringan Wi-Fi. Meskipun demikian, koneksi masih tergolong stabil karena tidak terdapat penurunan drastis pada sequence number yang menandakan packet loss besar atau timeout.

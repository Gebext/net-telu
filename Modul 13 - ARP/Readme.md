# M Gibran Khalilullah - 103072400035 - IF0405

# MODUL 13 ARP
## ARP
ARP (Address Resolution Protocol) adalah protokol jaringan yang digunakan untuk menerjemahkan atau memetakan alamat IP menjadi alamat MAC Address pada jaringan lokal (LAN). ARP diperlukan karena komunikasi pada lapisan Data Link menggunakan MAC Address, sedangkan pengguna umumnya mengenali perangkat melalui alamat IP.

## Konsep ARP
ARP bekerja pada batas antara Layer 2 (Data Link Layer) dan Layer 3 (Network Layer) pada model OSI. Protokol ini memungkinkan perangkat mengetahui alamat fisik (MAC Address) dari suatu alamat logis (IP Address) sehingga komunikasi dalam jaringan lokal dapat berlangsung dengan benar.

## Cara Kerja ARP
1. Sebuah perangkat ingin mengirim data ke alamat IP tertentu dalam jaringan lokal
2. Perangkat memeriksa ARP Cache untuk melihat apakah pasangan IP dan MAC Address tujuan sudah tersimpan
3. Jika belum ada, perangkat mengirimkan ARP Request secara broadcast ke seluruh jaringan
4. Perangkat yang memiliki alamat IP yang dicari akan mengirimkan ARP Reply yang berisi MAC Address miliknya
5. Pengirim menyimpan pasangan IP dan MAC tersebut ke dalam ARP Cache untuk digunakan pada komunikasi berikutnya
6. Setelah MAC Address diketahui, data dapat dikirimkan ke perangkat tujuan

## Analisis ARP pada Wireshark
1. Bukak CMD sebagai Administrator jalankan perintah: arp -d * untuk menghapus seluruh isi ARP Cache, sehingga komputer harus melakukan proses ARP kembali ketika ingin berkomunikasi dengan perangkat lain
   <img width="734" height="283" alt="image" src="https://github.com/user-attachments/assets/c3c16ce5-2e43-4a57-828f-8ef1cd1fe603" />
2. Membuka Wireshark lalu memilih Analyze -> Enabled Protocols -> IPv4
3. Start capture Wireshark
4. Membuka browser dan mengakses: http://gaia.cs.umass.edu/wireshark-labs/HTTP-ethereal-lab-file3.html
5. Stop capture Wireshark
6. Ketik filter: arp
   <img width="962" height="47" alt="image" src="https://github.com/user-attachments/assets/8eb0c0ac-8481-494e-ab6a-f354dd6544f1" />
7. Pilih salah satu paket untuk dianalisis
   <img width="968" height="415" alt="image" src="https://github.com/user-attachments/assets/0562b29f-08a3-48f3-8fd6-22155fd31941" />
**Analisis Paket**
Berdasarkan hasil capture Wireshark, paket yang dipilih adalah ARP Request (Opcode = Request/1). Perangkat dengan IP 192.168.1.1 dan MAC cc:b0:71:e9:b1:80 mengirim permintaan untuk mencari MAC Address milik IP 192.168.1.10. Karena MAC tujuan belum diketahui, Target MAC Address masih bernilai 00:00:00:00:00:00 dan paket dikirim ke alamat Broadcast (ff:ff:ff:ff:ff:ff) agar diterima seluruh perangkat di jaringan lokal. Paket ini pada dasarnya menanyakan: “Siapa yang memiliki IP 192.168.1.10?” Dari hasil tersebut dapat disimpulkan bahwa ARP digunakan untuk menerjemahkan alamat IP menjadi alamat MAC sebelum perangkat dapat mengirim frame Ethernet ke tujuan yang benar di jaringan lokal.

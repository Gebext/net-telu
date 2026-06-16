# M Gibran Khalilullah - 103072400035 - IF0405

# MODUL 4 : DNS

## NsLookup

**NsLookup** merupakan utilitas yang digunakan untuk memperoleh informasi mengenai **DNS (Domain Name System)**. Informasi yang dapat diperoleh meliputi alamat IP suatu domain, DNS server yang digunakan, serta informasi mail server.

### Langkah-langkah Praktikum

1. Buka **Command Prompt (CMD)**.
2. Jalankan perintah berikut:

   **a.** `nslookup www.mit.edu`
   Digunakan untuk menampilkan alamat IP dari domain beserta DNS server default yang digunakan.

   **b.** `nslookup -type=NS mit.edu`
   Digunakan untuk menampilkan daftar DNS server yang bersifat otoritatif untuk domain **mit.edu**. Jika opsi `-type=NS` tidak digunakan, hanya informasi DNS standar yang akan ditampilkan.

   **c.** `nslookup www.aiit.or.kr bitsy.mit.edu`
   Digunakan untuk mengirim query ke DNS server tertentu, yaitu **bitsy.mit.edu**, bukan DNS server default.

### Pertanyaan

#### 1. Menentukan alamat IP server web di Asia

- **Perintah:** `nslookup www.nus.edu.sg`
- **Domain:** `www.nus.edu.sg`
- **Alamat IP:** `45.60.35.225`

#### 2. Menentukan DNS otoritatif universitas di Eropa

- **Perintah:** `nslookup -type=NS ox.ac.uk`
- **DNS Server:** `dns0.ox.ac.uk`, `dns1.ox.ac.uk`, `dns2.ox.ac.uk`, `auth4.dns.ox.ac.uk`, `auth5.dns.ox.ac.uk`, dan `auth6.dns.ox.ac.uk`.

#### 3. Menentukan mail server Yahoo menggunakan DNS tertentu

- **Perintah:** `nslookup -type=MX yahoo.com dns0.ox.ac.uk`
- **Hasil:** `*** auth0.dns.ox.ac.uk can't find yahoo.com: Query refused`

Permintaan tersebut gagal diproses karena server **dns0.ox.ac.uk** merupakan DNS otoritatif yang hanya melayani domain **ox.ac.uk**, sehingga query terhadap domain lain, seperti **yahoo.com**, ditolak.

---

## IPConfig

**IPConfig** merupakan perintah pada Command Prompt yang digunakan untuk melihat dan mengelola konfigurasi jaringan berbasis TCP/IP. Dengan perintah ini, pengguna dapat mengetahui alamat IP perangkat, DNS server yang digunakan, serta melihat dan menghapus cache DNS.

### Langkah-langkah Praktikum

1. Buka **Command Prompt (CMD)**.
2. Jalankan perintah `ipconfig /all` untuk menampilkan informasi jaringan seperti alamat IP, subnet mask, default gateway, DNS server, dan MAC address.
3. Jalankan perintah `ipconfig /displaydns` untuk melihat daftar cache DNS yang tersimpan pada sistem.
4. Jalankan perintah `ipconfig /flushdns` untuk menghapus cache DNS sehingga sistem akan melakukan pencarian ulang saat mengakses suatu domain.

---

# Tracing DNS dengan Wireshark

## A. Analisis DNS Request dan Response pada Akses Website (`www.ietf.org`)

### Langkah-langkah Praktikum

1. Buka **Command Prompt (CMD)** dan jalankan perintah `ipconfig` untuk mengetahui alamat IP perangkat.
2. Jalankan Wireshark dan pilih antarmuka jaringan yang aktif.
3. Gunakan filter:

   ```
   ip.addr == 10.218.0.23
   ```

4. Mulai proses capture.
5. Akses halaman:

   ```
   http://www.ietf.org/
   ```

6. Tambahkan filter:

   ```
   ip.addr == 10.218.0.23 && dns.qry.name.contains "ietf"
   ```

### Pertanyaan

#### 1. Apakah DNS menggunakan UDP atau TCP?

Berdasarkan hasil pengamatan, protokol DNS pada percobaan ini menggunakan **UDP**.

#### 2. Port tujuan pada DNS Request dan port sumber pada DNS Response

- **DNS Request**
  - Source Port (Client): `58200`
  - Destination Port (Server): `53`

- **DNS Response**
  - Source Port (Server): `53`
  - Destination Port (Client): `58200`

---

## B. Analisis DNS Menggunakan Perintah `nslookup` (`www.mit.edu`)

### Langkah-langkah Praktikum

1. Jalankan Wireshark dan aktifkan proses capture.
2. Buka CMD dan jalankan:

   ```
   nslookup www.mit.edu
   ```

3. Hentikan proses capture dan gunakan filter DNS.
4. Amati paket **Standard Query** dan **Standard Query Response**.

### Pertanyaan

#### 1. Port tujuan request dan port sumber response

- **DNS Request**
  - Destination Port: `53`

- **DNS Response**
  - Source Port: `53`

#### 2. Alamat IP tujuan request

Permintaan DNS dikirim ke alamat **fe80::1**, yaitu alamat IPv6 lokal yang berfungsi sebagai DNS server pada jaringan.

#### 3. Tipe dan Answers pada Request

Jenis DNS request yang digunakan adalah **A (Address Record)**. Karena paket ini merupakan permintaan, maka belum terdapat bagian jawaban (_answers_).

#### 4. Answers pada Response

Terdapat tiga jawaban pada DNS response:

1. `www.mit.edu` merupakan alias (**CNAME**) dari `www.mit.edu.edgekey.net`.
2. Alias tersebut mengarah kembali ke `e9566.dscb.akamaiedge.net`.
3. Alamat IP tujuan akhir (**A Record**) adalah `23.217.163.122`.

---

## C. Analisis DNS Record NS Menggunakan `nslookup` (`mit.edu`)

### Langkah-langkah Praktikum

1. Jalankan Wireshark dan mulai capture.
2. Jalankan perintah:

   ```
   nslookup -type=NS mit.edu
   ```

3. Hentikan capture dan gunakan filter DNS.
4. Amati paket request dan response.

### Pertanyaan

#### 1. Alamat IP tujuan request

Permintaan DNS dikirim ke alamat **fe80::1**, yaitu DNS server default pada jaringan.

#### 2. Tipe dan Answers pada Request

Jenis DNS request adalah **NS (Name Server)**. Paket request tidak memiliki bagian jawaban karena hanya berisi permintaan data.

#### 3. Answers pada Response

Pada DNS response diperoleh beberapa nama server milik MIT. Informasi yang ditampilkan berupa **NS Record**, sedangkan alamat IP server biasanya disajikan pada bagian **Additional Record**.

---

## D. Analisis DNS Menggunakan Server Tertentu (`www.aiit.or.kr bitsy.mit.edu`)

### Langkah-langkah Praktikum

1. Jalankan Wireshark dan aktifkan proses capture.
2. Jalankan perintah:

   ```
   nslookup www.aiit.or.kr bitsy.mit.edu
   ```

3. Hentikan capture dan gunakan filter DNS.
4. Amati paket Standard Query.

### Pertanyaan

#### 1. Alamat IP tujuan request

Permintaan DNS dikirim ke alamat IP **18.0.72.3**, yang merupakan server **bitsy.mit.edu** dan dipilih secara manual melalui perintah `nslookup`.

#### 2. Tipe dan Answers pada Request

Jenis DNS request yang digunakan adalah **A (Address Record)**. Karena paket tersebut hanya berupa permintaan, maka belum terdapat informasi jawaban.

#### 3. Answers pada Response

Berdasarkan hasil pada Command Prompt, muncul pesan **"DNS request timed out"**, yang menunjukkan bahwa server DNS tidak memberikan respons terhadap query yang dikirimkan.

Akibatnya, tidak terdapat paket **DNS Response** yang dapat dianalisis pada percobaan ini. Kondisi tersebut terjadi karena server **bitsy.mit.edu** tidak memberikan balasan sebelum batas waktu (_timeout_) tercapai.

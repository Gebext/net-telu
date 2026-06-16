## M. Gibran Khalilullah - 103072430014 - IF0405

# MODUL 3 : HTTP

## Basic HTTP GET

Proses ini bertujuan untuk mengamati komunikasi antara browser sebagai _client_ dan server menggunakan metode **HTTP GET**.

### Langkah-langkah

1. Buka aplikasi Wireshark.
2. Pilih antarmuka **Wi-Fi** dan mulai proses _capture packet_.
3. Jalankan proses _capture_.
4. Buka browser dan akses alamat:

   ```
   http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file1.html
   ```

5. Gunakan filter `http` untuk menampilkan paket HTTP.
6. Hentikan proses _capture_.

<img width="1365" height="694" alt="gambar 1" src="https://github.com/user-attachments/assets/c8f52fdd-f50a-434b-85b7-77f32b6d0470" />

### Hasil Pengamatan

Pada percobaan ini, browser mengirimkan **HTTP GET Request** ke server `gaia.cs.umass.edu` untuk meminta file HTML. Berdasarkan hasil _capture_ di Wireshark, server memberikan respons **HTTP/1.1 200 OK**, yang menandakan bahwa permintaan berhasil diproses dan file HTML berhasil dikirimkan ke browser.

---

## Web Not Found

Percobaan ini bertujuan untuk mengamati respons server ketika client meminta resource yang tidak tersedia.

### Langkah-langkah

1. Mulai proses _capture_.
2. Buka URL yang tidak tersedia pada server melalui browser.
3. Gunakan filter `http`.
4. Hentikan proses _capture_.

![Web Not Found](https://github.com/user-attachments/assets/12cfa1c8-b93d-4ab9-b4db-19b3ac86ef35)

### Hasil Pengamatan

Pada pengujian ini, browser mengirimkan **HTTP GET Request** ke alamat resource yang tidak valid. Hasil _capture_ menunjukkan bahwa server merespons dengan status **HTTP/1.1 404 Not Found**. Status tersebut menunjukkan bahwa server berhasil menerima permintaan dari client, namun file atau resource yang diminta tidak ditemukan.

---

## Retrieving Long Documents

Proses ini bertujuan untuk mengamati pengambilan dokumen HTML dengan ukuran yang lebih besar.

### Langkah-langkah

1. Mulai proses _capture_.
2. Buka browser dan akses:

   ```
   http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file3.html
   ```

3. Gunakan filter `http`.
4. Hentikan proses _capture_.

![Retrieving Long Documents](https://github.com/user-attachments/assets/f25ebfb0-880e-4624-a19f-57c514dc05fd)

### Hasil Pengamatan

Browser mengirimkan **HTTP GET Request** untuk meminta dokumen HTML berukuran lebih besar. Server kemudian memberikan respons **HTTP/1.1 200 OK**, yang menandakan bahwa permintaan berhasil diproses. Dokumen HTML yang diterima memiliki isi yang lebih panjang dibandingkan percobaan sebelumnya dan berhasil ditampilkan oleh browser.

---

## HTML Documents dengan Embedded Objects

Percobaan ini bertujuan untuk mengamati proses pengambilan objek tambahan yang terdapat pada halaman HTML, seperti gambar.

### Langkah-langkah

1. Mulai proses _capture_.
2. Buka browser dan akses:

   ```
   http://gaia.cs.umass.edu/wireshark-labs/HTTP-wireshark-file4.html
   ```

3. Gunakan filter `http`.
4. Hentikan proses _capture_.

<img width="1365" height="178" alt="565139600-05df837e-eab1-4dde-8235-dde254e2172d" src="https://github.com/user-attachments/assets/d7c21be1-9413-44da-83e0-179df1612a9f" />

### Hasil Pengamatan

Pada percobaan ini, browser tidak hanya mengirim satu **HTTP GET Request** untuk mengambil file HTML utama, tetapi juga mengirim beberapa request tambahan untuk mengambil objek yang disisipkan pada halaman web. Setiap gambar atau objek lainnya memiliki URL tersendiri sehingga memerlukan request terpisah. Setelah server memberikan respons **HTTP 200 OK**, browser berhasil menampilkan seluruh objek tersebut pada halaman web.

---

## HTTP Authentication

Proses ini bertujuan untuk mengamati mekanisme autentikasi HTTP antara browser dan server.

### Langkah-langkah

1. Mulai proses _capture_.
2. Buka browser dan akses:

   ```
   http://gaia.cs.umass.edu/wireshark-labs/protected_pages/HTTP-wireshark-file5.html
   ```

3. Masukkan kredensial berikut:
   - **Username:** `wireshark-students`
   - **Password:** `network`

4. Gunakan filter `http`.
5. Hentikan proses _capture_.

![HTTP Authentication]()

### Hasil Pengamatan

Saat halaman yang dilindungi pertama kali diakses, server memberikan respons **HTTP 401 Unauthorized**, yang menunjukkan bahwa autentikasi diperlukan untuk mengakses resource tersebut. Browser kemudian menampilkan form login kepada pengguna. Setelah username dan password dimasukkan, browser mengirimkan kembali HTTP request yang telah dilengkapi dengan header **Authorization**. Jika data autentikasi yang diberikan benar, server akan mengizinkan akses ke halaman yang diminta.

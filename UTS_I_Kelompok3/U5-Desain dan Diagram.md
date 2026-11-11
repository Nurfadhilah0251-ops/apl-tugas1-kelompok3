Desain Arsitektur

Bagian ini terdiri dari tiga diagram: diagram konteks, diagram arsitektur yang menerapkan pola, dan diagram UML.
Ketiganya menggambarkan rancangan konseptual layanan tugas SPADA UMI-Kalam.

5.1 Diagram konteks
Diagram konteks menunjukkan hubungan antara sistem dengan pihak-pihak yang berinteraksi dengannya.

<img width="827" height="364" alt="image" src="https://github.com/user-attachments/assets/c45bdf87-cf64-439f-9c63-18003f49d141" />

Penjelasan:

1.	Mahasiswa menggunakan sistem untuk melihat dan mengumpulkan tugas.

2.	Dosen menggunakan sistem untuk memberikan tugas dan memeriksa hasilnya.

3.	Admin SPADA mengelola akun dan hak akses pengguna.

4.	Tim pengelola TI melakukan pemantauan dan pemeliharaan layanan.

5.2 Diagram arsitektur yang menerapkan pola

Diagram berikut menggabungkan Layered Architecture dan Event-Driven Architecture. Layered Architecture digunakan untuk mengatur tanggung jawab aplikasi, sedangkan Event-Driven Architecture digunakan untuk menjalankan pemeriksaan kemiripan secara asynchronous.

<img width="661" height="1089" alt="image" src="https://github.com/user-attachments/assets/3cda57e5-1ab7-4c1b-96f4-b966d9183441" />

Penjelasan:
1.	Presentation Layer menyediakan tampilan untuk dosen dan mahasiswa.
2.	Business Logic Layer mengelola login, pembuatan tugas, pengumpulan, dan tenggat waktu.
3.	Setelah dokumen berhasil disimpan, Submission Service mengirimkan event ke Message Queue.
4.	Similarity Service mengambil permintaan dari antrean dan menjalankan pemeriksaan kemiripan.
5.	Data Access Layer menghubungkan layanan dengan database.
6.	Data Layer menyimpan informasi tugas, pengguna, hasil pengumpulan, dan dokumen.

Dengan rancangan tersebut, proses pemeriksaan kemiripan tidak harus menunggu proses pengumpulan selesai untuk memberikan konfirmasi kepada mahasiswa.

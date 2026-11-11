Pengertian Pola Arsitektur

Pola arsitektur adalah pendekatan penyusunan komponen sistem untuk menyelesaikan permasalahan tertentu. Berikut dua pola dari kategori berbeda yang dapat diterapkan pada layanan tugas SPADA UMI-Kalam.

4.1 Pola Layered Architecture

<img width="664" height="439" alt="image" src="https://github.com/user-attachments/assets/6129d29b-ca6c-4f9e-be94-ac1c9841d69b" />

Alasan pemilihan:

Pola Layered Architecture membagi sistem menjadi beberapa lapisan berdasarkan tanggung jawabnya. Pola ini sesuai untuk layanan tugas karena sistem memiliki proses antarmuka pengguna, pengolahan aturan tugas, dan pengelolaan data.

Kelebihan:

•	Struktur sistem lebih terorganisasi.

•	Mempermudah pengembangan dan pemeliharaan.

•	Setiap lapisan memiliki tanggung jawab yang jelas.

Kekurangan:

•	Komunikasi harus melewati lapisan tertentu sehingga dapat menambah waktu pemrosesan.

•	Perubahan pada lapisan tertentu dapat memengaruhi lapisan lainnya jika ketergantungannya terlalu kuat.

Penerapan pada layanan:

1.	Presentation Layer: tampilan dosen dan mahasiswa.
2.	Business Logic Layer: proses pembuatan tugas, pengumpulan, tenggat, dan pemeriksaan hak akses.
3.	Data Access Layer: pengelolaan komunikasi dengan database.
4.	Database Layer: penyimpanan data pengguna, tugas, tenggat, dan hasil pengumpulan.

4.2 Pola Event-Driven Architecture

<img width="693" height="459" alt="image" src="https://github.com/user-attachments/assets/0804f4f1-2e38-4d0b-a588-643151202832" />

Alasan pemilihan:

Pola Event-Driven Architecture menggunakan peristiwa (event) untuk menghubungkan proses dalam sistem. Ketika mahasiswa berhasil mengumpulkan tugas, sistem menghasilkan peristiwa bahwa tugas telah dikumpulkan. Peristiwa tersebut dapat digunakan untuk memulai proses pemeriksaan kemiripan dan mengirim notifikasi.

Kelebihan:

•	Proses yang membutuhkan waktu lama dapat dijalankan secara terpisah.

•	Mengurangi ketergantungan langsung antar layanan.

•	Membantu menangani lonjakan permintaan melalui antrean.

Kekurangan:

•	Pengelolaan alur proses menjadi lebih kompleks.

•	Hasil proses tidak selalu tersedia secara langsung.

•	Membutuhkan mekanisme pemantauan dan penanganan event yang gagal.

Penerapan pada layanan:

Ketika mahasiswa mengunggah tugas, sistem menyimpan dokumen terlebih dahulu. Selanjutnya sistem mengirim event TugasDikumpulkan ke message queue. Layanan pemeriksaan kemiripan mengambil event tersebut dan memproses dokumen tanpa menghambat mahasiswa yang sedang mengumpulkan tugas.

4.3 Perbedaan kedua pola
|  Aspek | Layered Architecture | Event-Driven Architecture |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- || :--- | :--- |
| Fokus | Pembagian tanggung jawab sistem | Komunikasi berdasarkan peristiwa |
| Tujuan | Membuat struktur sistem terorganisasi | Memisahkan proses dan mengurangi ketergantungan langsung |
| Penerapan | Antarmuka, logika bisnis, akses data, database | Pengumpulan tugas, antrean, pemeriksaan kemiripan, notifikasi |
| Masalah yang Dibantu | Kompleksitas struktur aplikasi | Lonjakan proses dan pekerjaan yang membutuhkan waktu lama |

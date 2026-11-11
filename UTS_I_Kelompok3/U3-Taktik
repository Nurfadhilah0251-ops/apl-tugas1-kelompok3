Pengertian Taktik Arsitektur
Taktik merupakan cara yang digunakan untuk mencapai atribut kualitas yang telah ditentukan. 
Setiap karakteristik memiliki minimal satu taktik beserta cara kerja dan biaya yang dibutuhkan.

3.1 Taktik kinerja: Asynchronous Processing dan Message Queue
Cara kerja:
1.	Mahasiswa mengunggah dokumen tugas.
2.	Sistem memvalidasi dan menyimpan dokumen.
3.	Setelah dokumen berhasil disimpan, sistem mengirim permintaan pemeriksaan kemiripan ke message queue.
4.	Layanan pemeriksaan kemiripan mengambil permintaan dari antrean dan memprosesnya secara terpisah.
5.	Hasil pemeriksaan disimpan ke database dan dapat dilihat oleh dosen.

Harga yang dibayar:
•	Membutuhkan infrastruktur tambahan berupa message queue.
•	Menambah kompleksitas komunikasi antar layanan.
•	Hasil pemeriksaan kemiripan tidak langsung tersedia karena diproses secara asynchronous.

3.2 Taktik keamanan: Authentication dan Authorization
Cara kerja:
1.	Pengguna melakukan login menggunakan akun SPADA.
2.	Sistem memverifikasi identitas pengguna.
3.	Sistem memeriksa peran pengguna, seperti dosen, mahasiswa, atau admin.
4.	Sistem memberikan akses sesuai hak masing-masing peran.
5.	Setiap permintaan untuk melihat atau mengubah dokumen diperiksa kembali oleh server.

Harga yang dibayar:
•	Membutuhkan pengelolaan autentikasi dan hak akses.
•	Menambah proses pemeriksaan pada setiap permintaan.
•	Membutuhkan pemeliharaan aturan akses agar tidak terjadi kesalahan pemberian izin.

3.3 Taktik ketersediaan: Redundancy dan Retry Mechanism
Cara kerja:
1.	Permintaan pemeriksaan kemiripan disimpan dalam antrean.
2.	Jika layanan pemeriksaan mengalami gangguan, permintaan tidak langsung dihapus.
3.	Sistem mencoba mengirimkan ulang permintaan setelah layanan pulih.
4.	Jika proses gagal berulang kali, permintaan dapat dipindahkan ke antrean khusus untuk pemeriksaan lebih lanjut.
5.	Dokumen yang telah berhasil dikumpulkan tetap tersimpan di penyimpanan file.

Harga yang dibayar:
•	Membutuhkan penyimpanan dan pengelolaan antrean tambahan.
•	Membutuhkan mekanisme percobaan ulang dan pemantauan layanan.
•	Dapat meningkatkan penggunaan sumber daya server dan biaya infrastruktur.

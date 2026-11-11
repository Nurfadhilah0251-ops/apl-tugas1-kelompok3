# U1. Konteks dan ASR (Architectural Significant Requirements)

## 1.1 Ringkasan Layanan
Layanan tugas pada platform SPADA UMI-Kalam di lingkungan Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI) merupakan salah satu layanan inti di bawah subsistem Assignment & Assessment. Layanan ini dirancang untuk mendigitalkan dan mengoptimalkan seluruh siklus pengelolaan penugasan akademik secara daring.   

## 2.2 Masalah Utama Layanan dan Bukti Lapangan
* **Masalah Utama:**
  
Berdasarkan hasil wawancara dengan responden dan pengamatan langsung, ditemukan kendala utama dalam pengelolaan Layanan Tugas pada platform SPADA UMI-Kalam. Permasalahan utama meliputi lambatnya respons layanan hingga berpotensi terjadi request timeout, serta kegagalan atau lamanya proses pengunggahan berkas tugas mahasiswa (seperti laporan praktikum atau file .zip), terutama pada dokumen berukuran besar saat mendekati batas akhir pengumpulan (peak load deadline). Peningkatan jumlah pengguna secara bersamaan juga menyebabkan layanan sulit diakses dan memperlambat proses similarity check (pemeriksaan plagiarisme) yang berjalan secara sinkron.

Selain itu, pencatatan tenggat waktu (deadline) dan rekapitulasi pengumpulan tugas terkadang kurang terkelola dengan baik pada saat lonjakan trafik, sehingga riwayat pengumpulan tugas mahasiswa sulit dipantau secara real-time.

Beberapa temuan tersebut diperoleh dari pengalaman pengguna serta wawancara dengan responden di lingkungan FIKOM UMI sebagai berikut:
* **Bukti Lapangan (Berdasarkan Wawancara Responden):**
  **R1 (Mahasiswa FIKOM UMI):** "Pernah pas mau kumpul laporan praktikum jam 10 malam, mutar terus halamannya sampai 15 menit, pas ditekan submit malah error 'Gateway Timeout', padahal file saya cuma 8 MB."
  **R2 (Mahasiswa FIKOM UMI):** "Seringkali notifikasi tugas masuk telat atau tidak muncul, jadi kami tidak tahu persis kalau ada perubahan deadline mendadak dari dosen."
  **R3 (Dosen Pengampu di FIKOM UMI):** "Ketika memeriksa tugas masuk secara bersamaan setelah deadline, sistem terasa berat saat memuat dokumen mahasiswa dalam jumlah banyak, ditambah proses cek plagiat yang sering membuat antrean sistem lama."

## 1.3 Stekholder Utama



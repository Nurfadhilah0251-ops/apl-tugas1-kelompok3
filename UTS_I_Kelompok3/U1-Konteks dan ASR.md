# U1. Konteks dan ASR (Architectural Significant Requirements)

## 1.1 Ringkasan Layanan
Layanan tugas pada platform SPADA UMI-Kalam di lingkungan Fakultas Ilmu Komputer Universitas Muslim Indonesia (FIKOM UMI) merupakan salah satu layanan inti di bawah subsistem Assignment & Assessment. Layanan ini dirancang untuk mendigitalkan dan mengoptimalkan seluruh siklus pengelolaan penugasan akademik secara daring.   

## 2.2 Masalah Utama Layanan dan Bukti Lapangan
* **Masalah Utama:**
  
Berdasarkan hasil wawancara dengan responden dan pengamatan langsung, ditemukan kendala utama dalam pengelolaan Layanan Tugas pada platform SPADA UMI-Kalam. Permasalahan utama meliputi lambatnya respons layanan hingga berpotensi terjadi request timeout, serta kegagalan atau lamanya proses pengunggahan berkas tugas mahasiswa (seperti laporan praktikum atau file .zip), terutama pada dokumen berukuran besar saat mendekati batas akhir pengumpulan (peak load deadline). Peningkatan jumlah pengguna secara bersamaan juga menyebabkan layanan sulit diakses dan memperlambat proses similarity check (pemeriksaan plagiarisme) yang berjalan secara sinkron.

Selain itu, pencatatan tenggat waktu (deadline) dan rekapitulasi pengumpulan tugas terkadang kurang terkelola dengan baik pada saat lonjakan trafik, sehingga riwayat pengumpulan tugas mahasiswa sulit dipantau secara real-time.

Beberapa temuan tersebut diperoleh dari pengalaman pengguna serta wawancara dengan responden di lingkungan FIKOM UMI sebagai berikut:
* **Bukti Lapangan (Berdasarkan Wawancara Responden):**
* **R1 (Mahasiswa FIKOM UMI):** "Pernah pas mau kumpul laporan praktikum jam 10 malam, mutar terus halamannya sampai 15 menit, pas ditekan submit malah error 'Gateway Timeout', padahal file saya cuma 8 MB."
* **R2 (Mahasiswa FIKOM UMI):** "Seringkali notifikasi tugas masuk telat atau tidak muncul, jadi kami tidak tahu persis kalau ada perubahan deadline mendadak dari dosen."
* **R3 (Dosen Pengampu di FIKOM UMI):** "Ketika memeriksa tugas masuk secara bersamaan setelah deadline, sistem terasa berat saat memuat dokumen mahasiswa dalam jumlah banyak, ditambah proses cek plagiat yang sering membuat antrean sistem lama."

## 1.3 Stekholder Utama
Pihak-pihak yang memiliki peran dalam pengelolaan Layanan Tugas pada subsistem Assignment & Assessment di Universitas Muslim Indonesia (UMI) adalah sebagai berikut:
* **1. Mahasiswa (Pengguna Akhir):** Mengakses modul penugasan, mengunggah berkas tugas format PDF atau .zip (hingga 25 MB), memantau tenggat waktu (deadline), serta menerima ulasan dan nilai tugas. 
* **2. Dosen Pembimbing & Penguji (Pengguna Akhir):** Membuat dan mempublikasikan penugasan, menetapkan batas waktu, memantau pengumpulan tugas mahasiswa, menjalankan pemeriksaan kemiripan (similarity check), serta memberikan nilai dan umpan balik. 
* **3. Staf Administrasi Akademik (Tim Operasional):** Mengelola data rekapitulasi nilai akhir dan memastikan keterintegrasian data penilaian dengan sistem pelaporan pusat universitas.

## 1.4 Kebutuhan Signifikan Arsitektur (ASR)
Berdasarkan hasil analisis dan wawancara, terdapat tiga kebutuhan signifikan secara arsitektural yang perlu diperhatikan dalam perancangan Layanan Tugas pada subsistem Assignment & Assessment, yaitu:

* **1. Performance Efficiency (Efisiensi Kinerja):** Pada periode peak load mendekati batas akhir pengumpulan tugas (deadline), sistem harus mampu menangani hingga 500 pengguna secara bersamaan dengan target waktu muat halaman dan unggah berkas (<25 MB) rata-rata kurang dari 3 detik.

* **2. Integrity & Auditability (Integritas & Audit):** Setiap aktivitas penting, seperti pengunggahan berkas tugas, penetapan batas waktu, hasil similarity check (pemeriksaan kemiripan), hingga penginputan nilai, harus tersimpan secara permanen dan memiliki rekam jejak (tamper-proof audit trail) yang dapat ditelusuri.

* **3. Security & Confidentiality (Keamanan & Kerahasiaan):** Berkas tugas dan rekapitulasi nilai mahasiswa bersifat rahasia, terlindungi dengan baik, dan hanya dapat diakses oleh mahasiswa bersangkutan serta dosen pengampu melalui mekanisme kontrol akses berbasis peran (RBAC) dan secure signed URLs.

## 1.5 Keterkaitan Quality Drivers dengan ASR
Quality Drivers (karakteristik pendorong) dipilih berdasarkan kebutuhan utama Layanan Tugas. Hubungan antara karakteristik pendorong dan ASR dapat diuraikan sebagai berikut:
* **1. Performance Efficiency:** Berkaitan langsung dengan ASR 1, yaitu memastikan layanan tetap responsif dan cepat meskipun diakses oleh 500 pengguna secara bersamaan saat mendekati batas akhir pengumpulan (peak load deadline).

* **2. Security & Integrity:** Berkaitan langsung dengan ASR 2, yaitu menjaga kerahasiaan berkas tugas mahasiswa, mencegah akses tidak sah, serta memastikan setiap aktivitas penting dan rekap nilai tercatat dalam audit trail.

* **3. Maintainability:** Berkaitan langsung dengan ASR 3, yaitu memudahkan pengelolaan, pemeliharaan, dan pembaruan aturan bisnis (seperti penyesuaian bobot nilai atau parameter penilaian) tanpa merusak bagian subsistem lainnya.

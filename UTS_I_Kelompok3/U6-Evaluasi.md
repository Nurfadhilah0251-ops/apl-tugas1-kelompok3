# U6. Evaluasi Arsitektur (ATAM & Utility Tree)

Bab ini menyajikan evaluasi kualitas arsitektur perangkat lunak menggunakan metode Architecture Tradeoff Analysis Method (ATAM) dan Utility Tree (Pohon Utilitas) untuk subsistem Layanan Tugas pada platform SPADA UMI-Kalam (Assignment & Assessment). Evaluasi ini melibatkan analisis mendalam terhadap atribut kualitas prioritas guna memastikan sistem mampu mengatasi permasalahan beban puncak (peak load) serta memenuhi ekspektasi seluruh stakeholder utama di lingkungan FIKOM UMI.

---

## 6.1 Utility Tree (Pohon Utilitas)
*Utility Tree* digunakan untuk menerjemahkan kebutuhan kualitas bisnis dan operasional akademik ke dalam skenario spesifik yang dapat diukur secara arsitektural.

| Atribut Kualitas | Skenario Stimulus | Respon yang Diharapkan | Taktik Arsitektur yang Diterapkan |
| :--- | :--- | :--- | :--- |
| **1. Performance Efficiency** | Lonjakan 500 mahasiswa melakukan pengumpulan berkas tugas format PDF/.zip (25 MB) secara serentak 30 menit menjelang batas akhir (deadline). | Sistem tetap responsif, antrean pengumpulan tertampung tanpa server crash, dan waktu tanggap rata-rata di bawah 3 detik. | • *Message Broker (RabbitMQ/Redis)*<br>• *Background Worker (Asynchronous)*<br>• *Cloud Object Storage* |
| **2. Security & Integrity** | Upaya akses tidak sah, pencurian berkas, atau manipulasi data rekapitulasi nilai ujian oleh pihak luar atau mahasiswa lain. | Seluruh komunikasi API terenkripsi, sesi pengguna diverifikasi secara ketat, dan integritas data nilai serta berkas tugas terlindungi. | • *JWT Authentication (JSON Web Token)*<br>• *Role-Based Access Control (RBAC)* |
| **3. Maintainability** | Pembaruan aturan validasi tugas, penyesuaian parameter similarity check, atau rubrik penilaian oleh pengembang. | Modifikasi kode dapat dilakukan secara cepat tanpa merusak modul lain atau memicu *ripple effect*. | • *Layered Architecture*<br>• *Single Responsibility Principle (SRP)* |

---

## 6.2 Analisis Metode ATAM (*Architecture Tradeoff Analysis Method*)

### 1. Titik Sensitivitas (Sensitivity Points)
**Penggunaan Message Broker pada Pengumpulan Tugas:** Menjadi titik sensitif utama terhadap atribut Performance Efficiency. Jika konfigurasi antrean (queue) tidak dioptimalkan, penumpukan data (bottleneck) dapat terjadi pada worker.

**Pemisahan Lapisan (Layered Architecture):** Menjadi titik sensitif terhadap Maintainability. Keputusan memisahkan Business Logic Layer dari Presentation Layer memastikan perubahan logika akademik tidak memerlukan perombakan pada antarmuka pengguna.

### 2. Titik Pertukaran (Tradeoff Points
* **Kompleksitas Keamanan vs. Kinerja Sistem:**
* **Pertukaran:** Penerapan verifikasi token berlapis (JWT & Session Check) pada setiap permintaan unggah berkas besar (25 MB) menambah sedikit overhead komputasi jaringan.
* **Solusi:** Kompleksitas ini diterima demi menjamin tingkat keamanan dan kerahasiaan dokumen tugas akademik (Security & Integrity).
* **Asinkronisitas Pesan vs. Konsistensi Data Langsung:**
* **Pertukaran:** Penggunaan Message Broker membuat status pengumpulan tugas mahasiswa tidak langsung ditulis ke basis data utama pada detik yang sama (eventual consistency).
* **Solusi:** Sistem memberikan notifikasi status "Dalam Antrean (Queued)" kepada pengguna untuk menjaga transparansi pengalaman pengguna (UX).

### 3. Risiko dan Non-Risiko (Risks & Non-Risks)
* **Risiko (Risks):** Ketergantungan penuh pada layanan pihak ketiga atau message broker eksternal (seperti Redis/RabbitMQ). Jika layanan broker tersebut mengalami gangguan (outage), proses pengumpulan tugas dan antrean pemeriksaan kemiripan dapat tertunda sementara. Selain itu, penumpukan file sementara (temporary files) di direktori unggahan dapat menghabiskan kapasitas penyimpanan jika mekanisme pembersihan otomatis gagal.

* **Non-Risiko (Non-Risks):** Desain modular (split module) pada subsistem pengumpulan tugas terbukti aman dan tidak menimbulkan dampak negatif terhadap modul penilaian maupun modul perkuliahan lain yang berjalan secara paralel di platform SPADA UMI-Kalam.



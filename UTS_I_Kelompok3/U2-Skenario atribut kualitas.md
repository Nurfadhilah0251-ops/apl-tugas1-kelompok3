# U2. Skenario Atribut Kualitas

Bagian ini merinci tiga skenario atribut kualitas berdasarkan karakteristik pendorong utama (Performance Efficiency, Security, dan Maintainability). Masing-masing skenario diuraikan ke dalam 6 komponen ATAM (Architecture Tradeoff Analysis Method), di mana Skenario 1 dirancang khusus untuk menjawab masalah utama terkait lonjakan trafik dan kendala unggah berkas tugas.

---

## Skenario 1: Performance Efficiency (Menjawab Masalah Utama)

* **1. Stimulus (Stimulus):** Mengakses modul penugasan dan mengunggah berkas tugas format PDF atau .zip berukuran besar (hingga 25 MB) secara serentak dalam rentang 30 menit menjelang batas akhir pengumpulan (deadline).

* **2. Artefak (Artifact):** Modul Pengumpulan Tugas (Assignment & Assessment), API Gateway, dan Asynchronous Message Queue.

* **3. Lingkungan (Environment):** Kondisi beban puncak (peak traffic load) dengan 500 pengguna konkuren mengakses sistem secara bersamaan.

* **4. Respon (Response):** Sistem menampung permintaan unggah dan pemindaian kemiripan ke dalam antrean terpusat (message queue) dan memprosesnya secara asinkron di latar belakang (background worker) tanpa mengalami crash atau gateway timeout.

* **5. Ukuran Respon (Response Measure):** Waktu tanggap (latency) antarmuka dan proses unggah berkas tetap stabil dengan rata-rata di bawah 3 detik per permintaan. Tingkat kegagalan sistem (error rate) sebesar 0% (seluruh unggahan tugas berhasil diproses dan tercatat di sistem).

## Skenario 2: Security & Integrity (Keamanan & Integritas Data)
* **1 Sumber (Source):** Pihak eksternal.

* **2. Stimulus (Stimulus):** Mencoba melakukan akses ilegal atau modifikasi tidak sah terhadap berkas tugas dan lembar rekapitulasi nilai mahasiswa lain melalui manipulasi URL atau parameter sistem.

* **2. Artefak (Artifact):** Modul Otentikasi, Role-Based Access Control (RBAC), dan Audit Logging Service.

* **3. Lingkungan (Environment):** Kondisi operasional harian sistem saat proses penilaian dan pengunduhan berkas tugas berlangsung.

* **4. Respon (Response):** Sistem mendeteksi pelanggaran hak akses, menolak permintaan tersebut secara otomatis, dan mencatat seluruh percobaan akses ilegal ke dalam tamper-proof audit trail.

* **5. Ukuran Respon (Response Measure):** Persentase pencegahan akses ilegal mencapai 100% (0 kebocoran data rahasia tugas dan nilai). Seluruh aktivitas modifikasi data tercatat secara permanen di audit log dengan waktu deteksi pelanggaran < 1 detik.

## Skenario 3: Maintainability (Kemudahan Pemeliharaan)
* **1. Sumber (Source):** Tim Pengembang 

* **2. Stimulus (Stimulus):** Permintaan perubahan aturan bisnis, penyesuaian parameter similarity check, atau pembaruan rubrik penilaian tugas dari pihak fakultas.

* **3. Artefak (Artifact):** Lapisan Logika Bisnis (Business Logic Layer) dan Modul Penilaian pada arsitektur perangkat lunak.

* **4. Lingkungan (Environment):** Tahap pemeliharaan sistem (maintenance phase) di luar jam sibuk perkuliahan.

* **5. Respon (Response):** Tim pengembang melakukan modifikasi kode pada modul terkait tanpa merusak atau memengaruhi modul layanan lainnya (low coupling).

* **6. Ukuran Respon (Response Measure):** Waktu total yang dibutuhkan untuk implementasi, pengujian, dan penerapan perubahan aturan bisnis selesai dalam waktu < 2 hari kerja. Tingkat keberhasilan pengujian ulang (regression testing) mencapai 100% tanpa introduksi bug baru pada subsistem lain.

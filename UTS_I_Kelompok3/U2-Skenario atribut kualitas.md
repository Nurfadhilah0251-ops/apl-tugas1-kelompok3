# U2. Skenario Atribut Kualitas

Bagian ini merinci tiga skenario atribut kualitas berdasarkan karakteristik pendorong utama (Performance Efficiency, Security, dan Maintainability). Masing-masing skenario diuraikan ke dalam 6 komponen ATAM (Architecture Tradeoff Analysis Method), di mana Skenario 1 dirancang khusus untuk menjawab masalah utama terkait lonjakan trafik dan kendala unggah berkas tugas.

---

## Skenario 1: Performance Efficiency (Menjawab Masalah Utama)

* **1. Stimulus (Stimulus):** Mengakses modul penugasan dan mengunggah berkas tugas format PDF atau .zip berukuran besar (hingga 25 MB) secara serentak dalam rentang 30 menit menjelang batas akhir pengumpulan (deadline).

* **2. Artefak (Artifact):** Modul Pengumpulan Tugas (Assignment & Assessment), API Gateway, dan Asynchronous Message Queue.

* **3. Lingkungan (Environment):** Kondisi beban puncak (peak traffic load) dengan 500 pengguna konkuren mengakses sistem secara bersamaan.

* **4. Respon (Response):** Sistem menampung permintaan unggah dan pemindaian kemiripan ke dalam antrean terpusat (message queue) dan memprosesnya secara asinkron di latar belakang (background worker) tanpa mengalami crash atau gateway timeout.

* **5. Ukuran Respon (Response Measure):** Waktu tanggap (latency) antarmuka dan proses unggah berkas tetap stabil dengan rata-rata di bawah 3 detik per permintaan. Tingkat kegagalan sistem (error rate) sebesar 0% (seluruh unggahan tugas berhasil diproses dan tercatat di sistem).

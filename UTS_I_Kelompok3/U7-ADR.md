# U7. Architecture Decision Records (ADR)

Dokumen Architectural Decision Record (ADR) ini mencatat keputusan-keputusan arsitektur penting yang ditetapkan dalam perancangan Layanan Tugas pada subsistem Assignment & Assessment Universitas Muslim Indonesia (UMI). Setiap ADR memuat konteks permasalahan, keputusan yang dipilih, serta konsekuensi teknis yang ditimbulkan berdasarkan kebutuhan dan hasil evaluasi arsitektur.

---

## ADR-001: Penggunaan Antrean Pesan Asinkron untuk Pengunggahan Berkas Tugas
* **Title (Judul):** Penggunaan Antrean Pesan Asinkron untuk Pengunggahan Berkas Tugas

* **Status:** Accepted (Diterima)

* **Context (Konteks):** Saat mendekati batas akhir pengumpulan (deadline), ratusan mahasiswa mengunggah laporan atau tugas besar secara serentak, menyebabkan antarmuka mengalami freezing dan timeout akibat pemrosesan sinkron.

* **Decision (Keputusan):** Memisahkan proses penerimaan berkas dengan proses pemindaian kemiripan (*similarity check*) menggunakan asynchronous message queue (antrean pesan).

* **Consequences (Konsekuensi):**
* **Positif:** Antarmuka pengguna tetap responsif dan latensi unggah terjaga di bawah 3 detik.
* **Negatif:** Memerlukan tambahan infrastruktur message broker dan pengelolaan worker di sisi server.

* **Compliance (Kepatuhan):** Ditinjau melalui peninjauan kode berkala pada setiap akhir iterasi pengembangan.
---

## ADR-002: Standarisasi Format Berkas Penilaian Berbasis PDF
* **Title (Judul):** Standarisasi Format Berkas Penilaian Berbasis PDF

* **Status:** Accepted (Diterima)

* **Context (Konteks):** Keragaman format berkas tugas dari mahasiswa (seperti .docx, .zip, .rar) menyulitkan proses pratinjau langsung di dalam peramban web LMS SPADA UMI-Kalam.

* **Decision (Keputusan):** Mewajibkan format berkas utama yang dikumpulkan mahasiswa dibatasi hanya pada format dokumen PDF (.pdf).

* **Consequences (Konsekuensi):**
* **Positif:** Memungkinkan fitur built-in PDF viewer berfungsi optimal tanpa perlu mengunduh file secara manual.
* **Negatif:** Mengharuskan mahasiswa melakukan konversi format mandiri sebelum mengunggah tugas.

* **Compliance (Kepatuhan):** Divalidasi secara otomatis melalui validasi ekstensi file di sisi klien (client-side validation).

---


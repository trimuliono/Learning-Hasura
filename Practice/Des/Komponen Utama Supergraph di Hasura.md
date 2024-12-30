# Komponen Utama Supergraph di Hasura

---

## **GraphQL API sebagai Inti Supergraph**

- **Peran Utama GraphQL:**
  GraphQL API menjadi dasar dari Supergraph Hasura, menghubungkan aplikasi dengan sumber data secara efisien.
- **Query Data yang Efisien:**
  GraphQL memungkinkan aplikasi meminta data sesuai kebutuhan, mengurangi over-fetching dan under-fetching.
- **Akses Data Terpusat:**
  GraphQL API menyatukan akses ke berbagai sumber data, seperti database dan API, sehingga alur kerja lebih sederhana.

---

## **Metadata Engine, Caching, dan Subsystem**

- **Metadata Engine:**
  Menyimpan dan mengatur informasi tentang koneksi antar sumber data, memastikan akses data yang konsisten.
- **Caching:**
  - Mengurangi latensi dengan menyimpan data yang sering diakses.
  - Meningkatkan skalabilitas saat beban pengguna tinggi.
- **Subsystems:**
  - **Native Data Connector (NDC):** Menerjemahkan permintaan agar sesuai dengan berbagai sumber data.
  - **Runtime Engine:** Memproses query GraphQL secara efisien dengan memisahkan operasi build-time dan runtime.
  - **Builds System:** Memungkinkan pembaruan tanpa mengganggu layanan yang sedang berjalan.
  - **CLI (Command-Line Interface):** Alat yang memungkinkan pengelolaan proyek melalui perintah sederhana, membantu otomatisasi.
  - **Hasura Console:** Dashboard interaktif untuk mengelola, memonitor, dan memvisualisasikan data secara langsung.

---

## **Manfaat Komponen Utama**

- **Skalabilitas:**
  Metadata Engine dan caching mendukung operasi berskala besar dengan penundaan minimal.
- **Fleksibilitas:**
  Native Data Connector mendukung berbagai jenis sumber data, memudahkan adopsi Supergraph.
- **Performa Tinggi:**
  GraphQL API yang dioptimalkan memastikan pengiriman data cepat dan andal.

---

## **Kesimpulan**

- Komponen utama Supergraph (GraphQL API, Metadata Engine, Caching, Subsystems) memberikan jaringan pengiriman data yang tangguh, skalabel, dan efisien.
- Mengintegrasikan dataset yang kompleks dengan mudah, mempertahankan kinerja tinggi, dan fleksibilitas untuk aplikasi modern.


## Author

**Rafika Az Zahra Kusumastuti**

Dashboard Analytics - Telkom

Mahasiswa Teknologi Informasi, Institut Teknologi Sepuluh Nopember (ITS)

# Analisis Kesenjangan Digital Indonesia Tahun 2024

Repositori ini berisi proyek analisis data mengenai **akses internet rumah tangga di Indonesia** berdasarkan dataset resmi berjudul:

**“Persentase Rumah Tangga yang Pernah Mengakses Internet dalam 3 Bulan Terakhir Menurut Provinsi dan Klasifikasi Daerah, 2024.”**

Proyek ini menggunakan **Google BigQuery** untuk eksplorasi dan transformasi data serta **Looker Studio** untuk pembuatan dashboard interaktif yang mem visualisasikan tingkat akses internet antar provinsi dan kategori wilayah (Kota vs Desa) di Indonesia.

Analisis berfokus pada:
- pemerataan akses digital,
- kesenjangan antara wilayah kota dan desa,
- identifikasi provinsi dengan akses terbaik dan terburuk, serta\
- rekomendasi kebijakan berbasis data.

---

## Tujuan Proyek

* Membersihkan dan mengolah dataset menjadi **tabel analisis** yang siap digunakan untuk reporting.
* Mengidentifikasi **tingkat akses internet nasional** berdasarkan provinsi.
* Mengukur **kesenjangan digital (digital gap)** antara wilayah perkotaan dan perdesaan.
* Menyediakan **dashboard interaktif** untuk kebutuhan analisis dan visualisasi pemerataan digital.

---

## Struktur Repository

```
DIGITAL-GAP-INTERNET-ACCESS-2024/
│
├── internet_access_analysis.sql
│       └─ Query BigQuery: pembersihan data, transformasi, dan pembuatan metrik digital gap
│
├── Persentase Rumah Tangga Mengakses Internet 2024.csv
│       └─ Dataset utama yang digunakan dalam analisis
│
└── Data Mart - Internet Access 2024.xlsx
        └─ Output tabel analisis (sample data hasil query)
```

---

## Dataset yang Digunakan

Dataset berasal dari publikasi resmi pemerintah mengenai survei akses internet rumah tangga tahun 2024.

Kolom dalam dataset (`Data_Akses_Provinsi_cleaned`):

| Kolom                         | Deskripsi                                                              |
| ----------------------------- | ---------------------------------------------------------------------- |
| **Provinsi**                  | Nama provinsi di Indonesia                                             |
| **Kota**        | Persentase rumah tangga yang mengakses internet di wilayah perkotaan                                                           |
| **Desa**        | Persentase rumah tangga yang mengakses internet di wilayah perdesaan                                                           |
| **Total**        | Persentase keseluruhan per provinsi                                                           |
| **(ditambahkan) Gap** | Selisih perkotaan − perdesaan sebagai indikator digital divide |

Dataset ini digunakan sebagai dasar untuk analisis kesenjangan digital antar wilayah.

---

## SQL / Transformasi Data

Transformasi data dilakukan melalui BigQuery, mencakup:

* pembersihan data,
* normalisasi nama provinsi,
* penggabungan kategori wilayah,
* pembuatan metrik digital gap,
* perhitungan ranking akses internet antar provinsi.

Contoh transformasi:

* Menghitung gap:

  ```
  gap = perkotaan - perdesaan
  ```
* Menghitung peringkat:

  ```
  RANK() OVER (ORDER BY total DESC)
  ```

---
Dataset sudah membentuk tabel analitis `Data_Akses_Provinsi_cleaned` yang digunakan sebagai sumber dashboard.

## Dashboard Looker Studio

Dashboard interaktif dibuat menggunakan **Looker Studio** dan mencakup visualisasi:

| Komponen Dashboard                       | Visualisasi      |
| ---------------------------------------- | ---------------- |
| Filter Provinsi & Klasifikasi Daerah     | Dropdown         |
| Rata-rata Akses Kota, Desa, dan Nasional        | KPI              |
| Peta Sebaran Akses Internet              | Choropleth Map   |
| Perbandingan Kota vs Desa per Provinsi   | Bar Chart        |
| Digital Gap Ranking   | Bar Chart        |
| Tren dan Distribusi Akses                | Bar & Line Chart |
| Provinsi dengan Gap Tertinggi/Terendah | Table  |

Dashboard:
[https://lookerstudio.google.com/reporting/c2e91f45-aa3c-415c-850a-abf9e3b872de/page/C3IhF/edit]

---

## Temuan Utama Analisis

#### 1. Kesenjangan akses internet masih sangat terasa antara kota dan desa.
* Hampir semua provinsi menunjukkan gap positif (akses kota > desa).
* Beberapa provinsi memiliki gap sangat tinggi (>20%), terutama di kawasan timur.

#### 2. Provinsi dengan akses internet tertinggi:
(berdasarkan kolom total)
* DKI Jakarta - 98.18%
* Kep. Riau - 97.57%
* Riau - 94.16%
* Kalimantan Timur - 95.45%
* Bali, Banten, Jawa Barat, Jawa Tengah juga berada di kelompok tinggi.
Provinsi dengan urbanisasi tinggi memiliki infrastruktur digital lebih merata dan stabil.

#### 3. Provinsi dengan akses internet terendah:
* Papua Pegunungan - 12.15%
* Papua Tengah - 36.08%
* Papua Selatan - 65.71%
* Papua - 81.99%
Masih terdapat ketimpangan tajam antara Indonesia barat dan timur.

#### 4. Wilayah dengan digital gap terbesar
Contoh provinsi dengan gap tinggi (perkiraan berdasarkan data):
* **Papua Selatan**: gap besar antara kota (90.76%) dan desa (51.7%)
* **Papua Tengah**: gap sangat tinggi (95.00% vs 19.14%)
* **Papua Pegunungan**: kota 54.5% vs desa 8.81%
Menunjukkan infrastruktur desa sangat tertinggal.

#### 5. Implikasi digital divide
Kesenjangan ini dapat berdampak pada:
* akses pendidikan berbasis internet,
* aktivitas ekonomi digital,
* pelayanan publik berbasis digital (health-tech, gov-tech),
* literasi digital masyarakat desa.

---

## Tools & Teknologi

| Tools              | Kegunaan                              |
| ------------------ | ------------------------------------- |
| Google BigQuery    | Data processing, SQL cleaning, perhitungan metrik |
| Looker Studio      | Dashboard interaktif                  |
| SQL                | ETL kecil dan transformasi            |
| Microsoft Excel    | Preprocessing dan validasi data       |
| Visual Studio Code | Pengelolaan file proyek & dokumentasi |
| GitHub             | Version control & publikasi proyek    |

---

## Cara Menjalankan Proyek

1. Import dataset ke BigQuery.
2. Jalankan `internet_access_analysis.sql` untuk membuat data mart.
3. Hubungkan BigQuery dengan Looker Studio.
4. Gunakan dashboard atau modifikasi visualisasi sesuai kebutuhan.
5. (Opsional) Tambahkan dataset tahun sebelumnya untuk analisis tren.

---

## Lisensi

Proyek ini bersifat open-source dan dapat digunakan untuk kebutuhan edukasi dan riset.

---

Silakan gunakan, modifikasi, atau mengembangkan analisis ini sesuai kebutuhan riset atau proyek Anda.

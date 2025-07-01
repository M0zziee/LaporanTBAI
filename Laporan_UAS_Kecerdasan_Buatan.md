
# Analisis Sentimen Ulasan Mahasiswa Telkom University Menggunakan Naive Bayes

## Anggota Kelompok:
- Naufal Kalam Marudi – 2306021  
- Muhammad Fathir Ramada – 2306009

---

## 1. Business Understanding

### Permasalahan Dunia Nyata
Dalam era digital, mahasiswa sering menyampaikan pendapat mereka terhadap institusi melalui platform ulasan. Namun, volume ulasan yang besar membuat pihak universitas kesulitan memahami sentimen umum mahasiswa secara manual.

### Tujuan Proyek
Membangun model klasifikasi sentimen berdasarkan ulasan yang diberikan mahasiswa untuk mengidentifikasi persepsi mereka terhadap berbagai aspek universitas.

### Pengguna Sistem
Pihak manajemen kampus, tim kualitas layanan akademik, serta unit pengembangan kampus.

### Manfaat Implementasi AI
- Otomatisasi analisis opini mahasiswa
- Deteksi dini terhadap potensi masalah pelayanan
- Pengambilan keputusan berbasis data

---

## 2. Data Understanding

### Sumber Data
Dataset diperoleh dari ulasan mahasiswa Telkom University (file: `TelU_reviews.csv`), disusun secara manual.

### Deskripsi Fitur
| Nama Fitur | Deskripsi |
|------------|-----------|
| `review`   | Teks ulasan dari mahasiswa |
| `rating`   | Nilai penilaian dari 1 (buruk) hingga 5 (sangat baik) |
| `page`     | Halaman/platform tempat review diposting |

### Ukuran dan Format Data
- Total data: ± 1000 entri
- Format: CSV
- Tipe data: campuran teks dan numerik
- Target klasifikasi: **rating** (1–5), dikategorikan sebagai label sentimen

---

## 3. Exploratory Data Analysis (EDA)

### Visualisasi Distribusi Rating
![Screenshot 2025-07-01 181529](https://github.com/user-attachments/assets/474a1cb5-5825-469f-b2b4-854c095c7916)

Sebagian besar ulasan memiliki rating **5**, menunjukkan dominasi sentimen positif yang signifikan.

### Korelasi antar Fitur
![Screenshot 2025-07-01 181535](https://github.com/user-attachments/assets/7021dfea-0f86-4270-b943-de1bf604c421)

Tingkat korelasi antara fitur numerik (`page` dan `rating`) sangat rendah (0.24), menunjukkan independensi antar fitur.

### Ketidakseimbangan Kelas
Distribusi rating sangat tidak seimbang; rating 5 mendominasi secara signifikan dibanding rating lainnya.

### Insight Awal
- Sebagian besar mahasiswa memberikan review sangat positif.
- Perlu penanganan imbalance class untuk model yang lebih adil.

---

## 4. Data Preparation
- **Pembersihan**: Menghapus nilai null dan duplikasi.
- **Encoding**: Label target (`rating`) diproses sebagai label klasifikasi.
- **Text Preprocessing**: Tokenisasi, stopword removal, dan TF-IDF Vectorization pada kolom `review`.
- **Split Data**: Data dibagi menjadi 80% data latih dan 20% data uji.

---

## 5. Modeling

### Algoritma yang Digunakan
**Naive Bayes (MultinomialNB)** dipilih karena:
- Cocok untuk klasifikasi teks
- Cepat dan efisien dalam performa
- Umum digunakan dalam sentiment analysis

### Implementasi Model
Model dilatih menggunakan TF-IDF dari review sebagai fitur masukan dan rating sebagai label target.

---

## 6. Evaluation

### Confusion Matrix
![Screenshot 2025-07-01 181546](https://github.com/user-attachments/assets/6d16062f-8219-4221-bdd4-c73bdf585e05)
![Screenshot 2025-07-01 181552](https://github.com/user-attachments/assets/67b7ec48-e08b-4c82-9b6f-fbdf06e9f4b1)


### Metrik Evaluasi
- **Akurasi**: 86.53%
- **Precision**: Tinggi hanya untuk rating 5, rendah pada kelas minoritas
- **Recall**: Buruk pada kelas rendah (1–3), karena model bias terhadap kelas mayoritas
- **F1-score**: Tinggi hanya pada rating 5, sangat rendah lainnya

### Penjelasan Kinerja
Model mendominasi prediksi pada kelas rating 5. Hal ini disebabkan oleh distribusi data yang sangat tidak seimbang, sehingga model mengalami overfitting terhadap kelas tersebut.

---

## 7. Kesimpulan dan Rekomendasi

### Ringkasan
- Model Naive Bayes mampu mengklasifikasi sentimen ulasan mahasiswa dengan **akurasi 86.53%**, tetapi performanya sangat tergantung pada distribusi data.

### Pencapaian Tujuan
Tujuan membangun model klasifikasi sentimen tercapai secara teknis, namun belum optimal dari sisi generalisasi.

### Kelebihan dan Keterbatasan

**Kelebihan:**
- Implementasi sederhana dan efisien
- Cocok untuk teks

**Keterbatasan:**
- Sangat bergantung pada distribusi kelas
- Tidak bisa menangani ketidakseimbangan data dengan baik

### Rekomendasi
- Gunakan **resampling (SMOTE, undersampling)** untuk seimbangkan kelas
- Coba algoritma lain: SVM, Random Forest, Logistic Regression
- Gunakan lebih banyak data review yang bervariasi

---

## 8. Referensi
1. Apriliansyah, R. D. R., Astuti, R., Prihartono, W., & Hamonangan, R. (2025). Penerapan Algoritma Naive Bayes untuk Analisis Sentimen Pengunjung di Pantai Kejawanan. *Jurnal Informatika dan Teknik Elektro Terapan (JITET)*, 13(1). https://doi.org/10.23960/jitet.v13i1.5774

2. Hajaroh, H., Suprapti, T., & Narasati, R. (2024). Implementasi Algoritma Naive Bayes untuk Analisis Sentimen Ulasan Produk Makanan dan Minuman di Tokopedia. *Jurnal Mahasiswa Teknik Informatika (JATI)*, 8(1).

3. Arifqi, T., Suarna, N., & Prihartono, W. (2024). Penggunaan Naive Bayes dalam Menganalisis Sentimen Ulasan Aplikasi McDonald’s di Indonesia. *Jurnal Mahasiswa Teknik Informatika (JATI)*, 8(2).

4. Adeli, A., & Neshat, M. (2010). A Fuzzy Expert System for Heart Disease Diagnosis. *International MultiConference of Engineers and Computer Scientists (IMECS 2010)*, 2, 134–139. https://www.researchgate.net/publication/44260568

5. Cahyaningrum, Y. (2023). Penerapan Artificial Intelligence Menggunakan Fuzzy Logic dalam Dunia Pendidikan. *Jurnal Amplifier*, 13(2). https://doi.org/10.33369/jamplifier.v13i2.30757

---

## 9. Lampiran (Opsional)
- Dataset: `TelU_reviews.csv`
- Notebook: `TBAI.ipynb`
- Grafik visualisasi tersedia di folder proyek

# 📊 Analisis Similarity Paket Pengadaan Internet

### _“Nama Sama, Anggaran Bisa Beda 99%?”_

---

## 📌 Deskripsi Proyek

Proyek ini bertujuan untuk mengidentifikasi kemiripan antar paket pengadaan menggunakan pendekatan **similarity berbasis teks** dan **weighted column scoring**.

Fokus utama:

- Menentukan apakah dua paket pengadaan **mirip atau tidak**
- Mengidentifikasi **anomali** seperti:
    - Nama mirip tapi metode berbeda
    - Nama sama tapi anggaran jauh berbeda
    - Similarity tinggi tapi tidak diklasifikasikan mirip

---

## 🎯 Tujuan

1. Mengukur kemiripan nama paket menggunakan **TF-IDF + Cosine Similarity**
2. Melakukan **pelabelan manual (semi-supervised)** untuk validasi
3. Mengklasifikasikan pasangan paket menggunakan **Weighted Scoring**
4. Mengidentifikasi **anomali dalam data pengadaan**

---

## 📂 Struktur Repository

```
├── UTS_TID_DarisIrfan.ipynb
├── tid-internet-filter.csv
└── README.md
```

---

## ⚙️ Metodologi

### 1. Data Filtering

Data difilter berdasarkan kata kunci:

```
"internet"
```

---

### 2. Text Preprocessing

Melakukan normalisasi teks:

- Lowercase
- Menghapus tahun (contoh: 2026)
- Menghapus kata umum (stopwords)

---

### 3. Similarity (Nama Paket)

Menggunakan:

- **TF-IDF Vectorizer**
- **Cosine Similarity**

```python
similarity = cosine_similarity(tfidf_matrix)
```

---

### 4. Labeling (Semi-Manual)

- Similarity ≥ 0.8 → kandidat mirip
- Dilakukan pengecekan manual
- Label:
    - `1` = mirip
    - `0` = tidak mirip

---

### 5. Weighted Column Scoring

Menggabungkan 3 kolom:

| Kolom            | Bobot |
| ---------------- | ----- |
| Nama Paket       | 0.7   |
| Uraian Pekerjaan | 0.2   |
| Metode Pengadaan | 0.1   |

#### Formula:

```
weighted_score =
(0.7 × similarity_paket) +
(0.2 × similarity_uraian) +
(0.1 × similarity_metode)
```

---

### 6. Klasifikasi

```python
prediksi = weighted_score >= 0.75
```

---

### 7. Evaluasi Model

Menggunakan:

- Precision
- Recall
- F1-score

Contoh hasil:

```
Precision: 0.95
Recall:    0.30
Accuracy:  0.51
```

📌 Interpretasi:

- Model sangat akurat saat memprediksi "mirip"
- Namun masih banyak kasus mirip yang tidak terdeteksi

---

## 🚨 Analisis Anomali

Anomali didefinisikan sebagai:

```python
(persen_selisih > 0.5) OR (metode_A != metode_B)
```

### Contoh Temuan:

#### 1. Anomali Anggaran

- Nama sama
- Metode sama
- Selisih anggaran hingga **99%**

#### 2. Model vs Realitas

- Similarity tinggi
- Model memprediksi tidak mirip

#### 3. Metode Berbeda

- Nama sangat mirip
- Metode pengadaan berbeda

---

## 📊 Insight Utama

> “Nama paket yang mirip tidak selalu berarti paket sama.
> Uraian pekerjaan, metode pengadaan, dan anggaran dapat mempengaruhi hasil klasifikasi.”

---

## 🧠 Teknologi yang Digunakan

- Python
- Pandas
- Scikit-learn
- TF-IDF Vectorizer
- Cosine Similarity

---

## 📌 Cara Menjalankan

1. Clone repository:

```
git clone https://github.com/username/repo-name.git
```

2. Install dependencies:

```
pip install pandas numpy scikit-learn
```

3. Jalankan notebook:

```
notebooks/analysis.ipynb
```

---

## 📸 Output

- Dataset similarity
- Hasil klasifikasi
- Dataset anomali
- Infografis analisis

---

## 👨‍💻 Author

Nama: [Isi Nama Kamu]
Program: S2 Sistem Informasi
Universitas: [Isi Kampus]

---

## 📢 Catatan

Proyek ini dibuat sebagai bagian dari tugas:
**Integrasi Data & Analisis Pengadaan (PBJ)**

---

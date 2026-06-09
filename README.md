# Klasifikasi Tumor Otak Menggunakan K-Means dan Modified K-Nearest Neighbor dengan Paralelisasi

## Deskripsi Proyek

Proyek ini merupakan implementasi sistem klasifikasi citra tumor otak menggunakan kombinasi algoritma **K-Means Clustering** dan **Modified K-Nearest Neighbor (MKNN)**. Sistem dikembangkan untuk mengidentifikasi kelas tumor berdasarkan fitur centroid yang diekstraksi dari citra hasil preprocessing.

Untuk meningkatkan performa komputasi, proses ekstraksi fitur dan klasifikasi dijalankan secara paralel menggunakan **Joblib Parallel Processing**.

Proyek ini dikembangkan sebagai tugas akhir mata kuliah **Konsep Dasar Kecerdasan Artificial**.

---

## Dataset

Dataset yang digunakan adalah dataset citra **Brain Tumor MRI** yang terdiri dari beberapa kategori tumor.

Dataset dibagi menjadi:

* Training Set : 90%
* Testing Set : 10%

---

## Alur Sistem

### 1. Preprocessing

Tahapan preprocessing dilakukan pada setiap citra:

1. Membaca citra
2. Konversi ke grayscale
3. Resize menjadi 256 × 256 piksel
4. Flatten citra menjadi vektor 1 dimensi
5. Konversi tipe data menjadi Float32

Output:

* Flattened image
* Resized image

---

### 2. Ekstraksi Fitur Menggunakan K-Means

Setelah preprocessing, dilakukan clustering menggunakan algoritma K-Means.

Tahapan:

1. Inisialisasi centroid
2. Menghitung jarak ke centroid terdekat
3. Assignment cluster
4. Update centroid
5. Iterasi hingga konvergen

Output:

* Centroid citra
* Label cluster

Centroid yang dihasilkan digunakan sebagai representasi fitur citra.

---

### 3. Klasifikasi Menggunakan Modified KNN

Modified KNN digunakan untuk melakukan klasifikasi berdasarkan centroid hasil ekstraksi fitur.

Tahapan:

1. Menghitung jarak centroid data uji terhadap seluruh centroid data latih
2. Menyimpan seluruh jarak ke dalam distance array
3. Mengurutkan jarak secara ascending
4. Mengambil K tetangga terdekat
5. Menghitung bobot menggunakan persamaan:

[
w(x)=1/(x + e)
]

dengan:

[
e = 1.10^-6
]

6. Menjumlahkan bobot untuk setiap kelas
7. Memilih kelas dengan total bobot terbesar

Output:

* Label prediksi

---

## Paralelisasi

Proyek ini memanfaatkan pemrosesan paralel untuk mempercepat komputasi.

### Parallel Centroid Extraction

Dilakukan pada:

* Data Training
* Data Testing

Setiap citra diproses secara independen sehingga cocok untuk pendekatan data parallelism.

### Parallel Classification

Proses klasifikasi Modified KNN pada data uji dijalankan secara paralel untuk mempercepat proses prediksi.

---

## Arsitektur Sistem

```text
Dataset
   │
   ▼
Split Dataset (90/10)
   │
   ├── Train Data
   │      │
   │      ▼
   │  Preprocessing
   │      │
   │      ▼
   │    K-Means
   │      │
   │      ▼
   │ Save Train Centroids
   │
   └── Test Data
          │
          ▼
      Preprocessing
          │
          ▼
        K-Means
          │
          ▼
     Modified KNN
          │
          ▼
      Prediction
          │
          ▼
      Evaluation
```

---

## Evaluasi

Model dievaluasi menggunakan metrik:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix

---

## Teknologi yang Digunakan

* Python
* NumPy
* OpenCV
* Scikit-Learn
* Joblib
* Matplotlib
* Pandas

---

## Cara Menjalankan

### Clone Repository

```bash
git clone <repository-url>
cd <repository-name>
```

### Install Dependensi

```bash
pip install -r requirements.txt
```

### Jalankan Notebook

```bash
jupyter notebook
```

Buka file notebook proyek dan jalankan seluruh sel secara berurutan.

---

## Struktur Proyek

```text
project/
│
├── docs/
│   └── Deteksi Tumor Otak dengan Segmentasi K-Means dan Klasifikasi Menggunakan Algoritma K-Nearest Neighbor yang dimodifikasi.pdf
│
├── notebook/
│   └── notebook.ipynb
│
├── image/
│   └── kmeans_pipeline.png
│   └── knn_pipeline.png
│   └── overall_pipeline.png
│   └── preprocess_pipeline.png
│   └── training_pipeline.png
│
├── README.md
│
└── requirements.txt
```

---

## Penulis

- Silvia (25032014006)
- Christofarel Rumana Putra (25032014007)
- Putri Aulia Rahmah (25032014052)

Program Studi Kecerdasan Artifisial

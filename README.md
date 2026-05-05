# UTS Machine Learning - Wine Quality Prediction 

Repositori ini berisi alur penyelesaian untuk Ujian Tengah Semester (UTS) mata kuliah Machine Learning. Proyek ini bertujuan untuk membangun model klasifikasi pembelajaran mesin yang mampu memprediksi kualitas anggur (skala 0-10) berdasarkan fitur-fitur kimiawinya.

## Informasi Penulis
* **Nama**: Keisya Gandien Kustantya
* **NIM**: 230400016

## Deskripsi Dataset
Dataset yang digunakan adalah **Wine Quality Dataset**, yang berisi sekumpulan atribut kimiawi dari sampel anggur merah dan putih.
* **Fitur Utama**: `fixed acidity`, `volatile acidity`, `citric acid`, `residual sugar`, `chlorides`, `free sulfur dioxide`, `total sulfur dioxide`, `density`, `pH`, `sulphates`, `alcohol`.
* **Target Variabel**: `quality` (skala penilaian kualitas anggur).

## Struktur Repositori
* `data_training.csv` : Dataset yang memiliki label `quality`, digunakan untuk melatih dan mengevaluasi model.
* `data_testing.csv` : Dataset uji (tanpa label `quality`) yang akan diprediksi.
* `notebook_analisis.ipynb` : Jupyter Notebook / Google Colab yang memuat seluruh proses pembersihan data, *Exploratory Data Analysis* (EDA), pemodelan, hingga evaluasi grafis.
* `hasilprediksi_978.csv` : File hasil keluaran akhir berupa prediksi kualitas untuk `data_testing.csv` yang HANYA memuat kolom `Id` dan `quality`.

## Metodologi & Alur Kerja (*Workflow*)
Proyek ini dikerjakan dengan pendekatan data sains yang terstruktur:
1. **Pembersihan Data (*Data Cleaning*)**:
   * Penanganan *missing values* menggunakan metode pengisian Median untuk menghindari bias dari *outlier*.
   * Penghapusan baris data duplikat agar model belajar dari variasi fitur yang unik.
2. **Penanganan Data Tidak Seimbang (*Imbalanced Data*)**:
   * Penggunaan teknik **SMOTE (*Synthetic Minority Over-sampling Technique*)** untuk menyeimbangkan kelas target `quality` yang sangat timpang pada observasi kualitas ekstrem (rendah/tinggi).
3. **Persiapan Pemodelan**:
   * *Data Splitting* dengan rasio **80:20** (Training:Validation) menggunakan `random_state=42` untuk reproduksibilitas.
   * *Feature Scaling* menggunakan **StandardScaler** untuk menyetarakan skala antar-fitur.
4. **Pemodelan & Komparasi (*Benchmarking*)**:
   * Membandingkan performa dari 3 algoritma klasifikasi yang berbeda: **Random Forest**, **K-Nearest Neighbors (KNN)**, dan **Support Vector Machine (SVM)**.
5. **Optimasi Hyperparameter**:
   * Menggunakan **GridSearchCV** untuk mencari kombinasi parameter terbaik pada model pemenang.

## Hasil Evaluasi
Berdasarkan komparasi, **Random Forest** terpilih sebagai model terbaik untuk dataset ini. Setelah dilakukan *Hyperparameter Tuning*, model ini mencapai performa evaluasi sebagai berikut pada data validasi:

* **Akurasi**: 86.44%
* **Macro Average F1-Score**: 0.86
* **Parameter Terbaik**: `{'max_depth': 20, 'min_samples_leaf': 1, 'min_samples_split': 2, 'n_estimators': 200}`

Analisis metrik **F1-Score** membuktikan bahwa model mampu memprediksi seluruh kelas secara seimbang tanpa memihak hanya pada kelas mayoritas, sementara visualisasi **Confusion Matrix** (tersedia di Notebook) mengonfirmasi tingkat ketepatan klasifikasi pada setiap level kualitas anggur.

## Cara Menjalankan (*How to Run*)
1. *Clone* repositori ini ke komputer lokal Anda.
2. Pastikan Anda memiliki *environment* Python 3.x dan pustaka yang dibutuhkan (`pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `imbalanced-learn`).
3. Buka file `.ipynb` menggunakan Jupyter Notebook, Jupyter Lab, atau Google Colab.
4. Jalankan *cell* secara berurutan (*Run All*) untuk mereproduksi hasil analisis.

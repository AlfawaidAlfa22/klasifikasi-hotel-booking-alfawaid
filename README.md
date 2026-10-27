# 🏨 Klasifikasi Pembatalan Pemesanan Hotel (Hotel Booking Demand)

Tugas Praktikum Machine Learning - Universitas Pamulang

![Python](https://img.shields.io/badge/Python-3.x-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-Decision%20Tree-orange)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626)

Proyek ini membangun model *Machine Learning* menggunakan algoritma **Decision Tree** untuk memprediksi apakah sebuah pemesanan hotel akan **dibatalkan atau tidak**. Prediksi seperti ini membantu pihak hotel dalam mengelola ketersediaan kamar dan mengurangi kerugian akibat pembatalan.

---

## 📌 Latar Belakang

Pembatalan pemesanan merupakan salah satu masalah utama di industri perhotelan karena kamar yang sudah dipesan tetapi dibatalkan dapat menyebabkan hilangnya pendapatan. Dengan memanfaatkan data historis pemesanan, hotel dapat memprediksi pemesanan mana yang berpotensi dibatalkan dan menyiapkan strategi sejak awal.

## 🎯 Tujuan

- Memprediksi status pembatalan pemesanan hotel (`is_canceled`).
- Menerapkan algoritma klasifikasi **Decision Tree**.
- Mengukur performa model menggunakan akurasi, precision, recall, dan f1-score.

## 📊 Dataset

| Keterangan | Nilai |
|---|---|
| Nama dataset | Hotel Booking Demand |
| File | `hotel_bookings.csv` |
| Jumlah data | 119.390 baris |
| Jumlah kolom | 32 kolom |
| Target | `is_canceled` (1 = dibatalkan, 0 = tidak dibatalkan) |
| Proporsi target | ±63% tidak dibatalkan, ±37% dibatalkan |

Dataset berisi data pemesanan dua jenis hotel, yaitu *City Hotel* dan *Resort Hotel*.

### Fitur yang Digunakan

| Fitur | Keterangan |
|---|---|
| `hotel` | Jenis hotel (City Hotel / Resort Hotel) |
| `lead_time` | Jarak hari antara pemesanan dan tanggal kedatangan |
| `stays_in_weekend_nights` | Jumlah malam menginap di akhir pekan |
| `stays_in_week_nights` | Jumlah malam menginap di hari kerja |
| `adults` | Jumlah tamu dewasa |
| `children` | Jumlah tamu anak-anak |
| `is_repeated_guest` | Apakah tamu pernah menginap sebelumnya |
| `previous_cancellations` | Jumlah pembatalan sebelumnya |
| `booking_changes` | Jumlah perubahan pada pemesanan |
| `adr` | Rata-rata tarif harian (*Average Daily Rate*) |

## 🔄 Alur Proyek

1. **Data Loading**: Memuat dataset `hotel_bookings.csv` dengan `pandas`.
2. **Data Cleaning**: Mengisi nilai kosong pada kolom `children`, `country`, `agent`, dan `company`.
3. **Data Preprocessing**: Mengubah data kategorikal menjadi numerik menggunakan *Label Encoding*.
4. **Pembagian Data**: Data dibagi menjadi 80% data latih dan 20% data uji (`random_state=42`).
5. **Modeling**: Melatih model `DecisionTreeClassifier`.
6. **Evaluation**: Menguji model menggunakan akurasi dan `classification_report`.

## 📈 Hasil

Akurasi model **Decision Tree** pada data uji: **77,89%**

| Kelas | Precision | Recall | F1-score |
|---|---|---|---|
| 0 (tidak dibatalkan) | 0,82 | 0,82 | 0,82 |
| 1 (dibatalkan) | 0,71 | 0,71 | 0,71 |

Model lebih akurat mengenali pemesanan yang **tidak dibatalkan** dibanding yang dibatalkan. Hal ini wajar karena jumlah data kelas "tidak dibatalkan" lebih banyak.

## 🛠️ Teknologi yang Digunakan

- Python 3
- Pandas
- Scikit-learn
- Jupyter Notebook

## 📁 Struktur Repositori

```
klasifikasi-hotel-booking-alfawaid/
├── hotel booking demand.ipynb   # Notebook klasifikasi (Decision Tree)
├── hotel_booking_regresi.ipynb  # Notebook regresi ADR
├── hotel_bookings.csv           # Dataset
└── README.md                    # Dokumentasi proyek
```

## ▶️ Cara Menjalankan

1. Clone repositori ini:
   ```bash
   git clone https://github.com/AlfawaidAlfa22/klasifikasi-hotel-booking-alfawaid.git
   cd klasifikasi-hotel-booking-alfawaid
   ```
2. Install library yang dibutuhkan:
   ```bash
   pip install pandas scikit-learn jupyter
   ```
3. Jalankan Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
4. Buka `hotel booking demand.ipynb`, lalu jalankan semua sel secara berurutan dari atas.

## 💡 Kesimpulan

Model Decision Tree mampu memprediksi pembatalan pemesanan hotel dengan akurasi sekitar 78%. Hasil ini sudah cukup baik sebagai model dasar (*baseline*), namun masih dapat ditingkatkan, misalnya dengan:

- membatasi kedalaman pohon (*hyperparameter tuning*) untuk mengurangi overfitting,
- menambah fitur kategorikal seperti `deposit_type` dan `market_segment`,
- mencoba algoritma lain seperti Random Forest.

## 📉 Bagian 2: Regresi Tarif Harian (ADR)

Selain klasifikasi pembatalan, proyek ini dilengkapi notebook regresi `hotel_booking_regresi.ipynb` untuk memprediksi **ADR (Average Daily Rate)**. Lima algoritma dibandingkan: Linear Regression, Ridge (L2), Lasso (L1), Random Forest, dan Gradient Boosting.

**Langkah:** data dengan ADR ≤ 0 atau > 500 dibuang sebagai outlier, kategori diubah dengan One-Hot Encoding, data dibagi 80:20 (`random_state=42`), lalu model dievaluasi dengan MAE, MSE, RMSE, dan R².

| Model | MAE | RMSE | R² uji | R² latih |
|---|---|---|---|---|
| Random Forest | 11,65 | 20,20 | 0,815 | 0,917 |
| Gradient Boosting | 16,71 | 23,81 | 0,743 | 0,753 |
| Linear Regression | 23,93 | 32,48 | 0,522 | 0,525 |
| Ridge (L2) | 23,93 | 32,48 | 0,522 | 0,525 |
| Lasso (L1) | 23,93 | 32,48 | 0,522 | 0,525 |

**Kesimpulan singkat:** Random Forest terbaik. Model berbasis pohon jauh mengungguli model linear sehingga hubungan fitur dan ADR bersifat non-linear. Regularisasi Ridge/Lasso tidak memberi peningkatan pada data ini. Gradient Boosting masih dapat ditingkatkan dengan tuning hyperparameter.

**Cara membaca metrik:** MAE, MSE, dan RMSE semakin kecil semakin baik (bergantung pada skala target, tidak harus di bawah 1). R² maksimal 1, semakin mendekati 1 semakin baik, dan bisa negatif jika model lebih buruk dari menebak rata-rata.

## 📚 Referensi

- Antonio, N., de Almeida, A., & Nunes, L. (2019). Hotel booking demand datasets. *Data in Brief, 22*, 41-49. https://doi.org/10.1016/j.dib.2018.11.126
- Oliveira, F. B., et al. (2024). Machine learning and time series analysis to forecast hotel room prices. *BRACIS 2024*. https://sol.sbc.org.br/index.php/bracis/article/view/33638
- Binesh, F., & Belarmino, A. M. (2024). Forecasting hotel room prices when entering turbulent times: A game-theoretic artificial neural network model. *Int. J. Contemporary Hospitality Management*. https://doi.org/10.1108/IJCHM-10-2022-1233
- Quayesam, D. L. (2024). A comparison of machine learning algorithms for predicting sea surface temperature in the Great Barrier Reef region. arXiv:2411.15202.
- Aljuboori, A. A. (2024). Enhancing accuracy in predicting continuous values through regression. *University of Bahrain Scientific Journals*.
- Mao, M. (2024). A comparative study of random forest regression for predicting house prices using gradient boosting. *DAI 2023*, Atlantis Press. https://doi.org/10.2991/978-94-6463-370-2_63
- Pedregosa, F., et al. (2011). Scikit-learn: Machine learning in Python. *JMLR, 12*, 2825-2830.

## 🤖 Catatan Pengembangan

Notebook regresi, kesimpulan, dan pembaruan dokumentasi ini disusun dengan bantuan Claude (Anthropic) dan diperbarui melalui GitHub.

## 👤 Penulis

**Alfawaid** - [@AlfawaidAlfa22](https://github.com/AlfawaidAlfa22)

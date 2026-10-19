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
├── hotel booking demand.ipynb   # Notebook utama (kode + komentar)
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

## 👤 Penulis

**Alfawaid** - [@AlfawaidAlfa22](https://github.com/AlfawaidAlfa22)

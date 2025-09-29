# Analisis Dataset Coffee Shop ☕

# File Raw CSV
[Uploading data coffe shop CSV.csv…]()

# File Ipynb colab.google
[Uploading ydata_coffeshop.ipynb…]()

# Pendahuluan

Dataset ini berisi transaksi dari sebuah coffee shop. Terdiri dari kolom seperti Transaction ID, Item, Quantity, Price Per Unit, Total Spent, Payment Method, Location, dan Transaction Date.
Tujuan analisis adalah memahami kondisi awal dataset, mendeteksi masalah seperti missing values, duplikat, dan outlier, lalu melakukan proses cleaning sehingga dataset siap digunakan untuk analisis lebih lanjut.

# Tujuan Analisis

Mengetahui struktur dan isi awal dataset.

Melakukan profiling untuk melihat kualitas data.

Membersihkan data: konversi tipe data, perbaikan missing values, hapus duplikat.

Membuat laporan perbandingan sebelum dan sesudah cleaning dengan bantuan ydata-profiling.

# Data Awal Coffee Shop

Jumlah baris: 10.000

Jumlah kolom: 8

Kolom: Transaction ID, Item, Quantity, Price Per Unit, Total Spent, Payment Method, Location, Transaction Date.

# LINK COLLAB BESERTA YDATA
https://colab.research.google.com/drive/1VU0mHaVQXuw2ziwVq_MNX3_vz62sOFMn?usp=sharing 

# 1. Import Library

Menggunakan pandas untuk pengolahan data dan ydata-profiling untuk profiling otomatis.

import pandas as pd
from ydata_profiling import ProfileReport

# 2. Load Dataset Coffee Shop
df = pd.read_csv("data_coffe_shop.csv")

# 3. Profiling Awal (Sebelum Cleaning)

Membuat laporan kondisi awal dataset, untuk mengetahui missing values, tipe data, distribusi, korelasi, dll.

profile_before = ProfileReport(df, title="Coffee Shop Profiling - Sebelum Cleaning", explorative=True)
profile_before.to_notebook_iframe()
profile_before.to_file("coffee_shop_before_cleaning.html")

---

<img width="1416" height="606" alt="image" src="https://github.com/user-attachments/assets/299ad869-1d26-4e73-890b-c078e7c80c34" />
<img width="1284" height="400" alt="image" src="https://github.com/user-attachments/assets/30c2562a-f5a7-45f6-8bdf-a7f7a7bb1a40" />
<img width="1282" height="399" alt="image" src="https://github.com/user-attachments/assets/eb82b1ad-5e3a-42f4-924e-455bae7324f3" />
<img width="1279" height="473" alt="image" src="https://github.com/user-attachments/assets/3dbe03c9-4d5d-4c3a-b6ac-beffa956e8b0" />
<img width="1266" height="466" alt="image" src="https://github.com/user-attachments/assets/a49e2188-5be8-4d39-bb99-5a799db2d4b2" />
<img width="1276" height="358" alt="image" src="https://github.com/user-attachments/assets/1e47f980-0e44-49ce-b42a-361c93c0aec5" />
<img width="1277" height="366" alt="image" src="https://github.com/user-attachments/assets/e04dc6a3-bdfc-47c0-8d46-fb812af1bcda" />


# 4. Cleaning Data

Konversi kolom Quantity, Price Per Unit, Total Spent ke numeric.

Hapus duplikat.

Isi missing values dengan median (numerik) atau modus (kategorikal).

for col in ["Quantity", "Price Per Unit", "Total Spent"]:
    df[col] = pd.to_numeric(df[col], errors="coerce")

df = df.drop_duplicates()

for col in df.columns:
    if df[col].dtype in ["int64", "float64"]:
        df[col] = df[col].fillna(df[col].median())
    else:
        df[col] = df[col].fillna(df[col].mode()[0])

# 5. Profiling Setelah Cleaning

Membuat laporan kondisi dataset setelah diperbaiki, sehingga bisa dibandingkan dengan versi awal.

profile_after = ProfileReport(df, title="Coffee Shop Profiling - Sesudah Cleaning", explorative=True)
profile_after.to_notebook_iframe()
profile_after.to_file("coffee_shop_after_cleaning.html")

---



# Kesimpulan

Dataset awal mengandung missing values pada beberapa kolom (Item, Quantity, Price Per Unit, Total Spent, Payment Method, Location, Transaction Date).

Tidak ditemukan duplikat signifikan, tetapi tetap dilakukan pengecekan.

Setelah dilakukan cleaning, dataset menjadi lebih konsisten dan siap untuk tahap analisis eksploratif atau model machine learning.

Dua laporan ydata-profiling (before & after cleaning) bisa digunakan sebagai pembanding kualitas data.

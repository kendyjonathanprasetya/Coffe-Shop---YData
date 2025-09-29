 # Analisis Dataset Coffee Shop ☕
---

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
1. Ringkasan Dataset

Menampilkan overview dataset: jumlah baris, jumlah kolom, tipe data, jumlah nilai unik, duplikat, serta persentase missing values.
<img width="1290" height="575" alt="image" src="https://github.com/user-attachments/assets/96434c80-5b0e-4a18-9965-8e7a850cca4f" />

---
2. Data Quality Alerts

Berisi peringatan otomatis dari YData terkait kualitas data, misalnya nilai kosong, distribusi aneh, atau kolom dengan nilai konstan.
<img width="1196" height="355" alt="image" src="https://github.com/user-attachments/assets/2a2fe576-69fc-49b3-91cf-d94addf46f2d" />

---
3. Tipe Variabel

Klasifikasi kolom berdasarkan tipe datanya: numerik, kategorikal, atau datetime. Membantu mengecek apakah data sudah dikenali sesuai formatnya.
<img width="1206" height="364" alt="image" src="https://github.com/user-attachments/assets/e1fa2de4-8762-43d1-8a2b-e07c4f2bd2a6" />

---
4. Missing Values

Visualisasi jumlah nilai kosong di tiap kolom. Dari sini bisa ditentukan strategi cleaning, misalnya drop atau imputasi dengan median/modus.
<img width="1208" height="368" alt="image" src="https://github.com/user-attachments/assets/4cec09b7-26a1-43ee-be3d-491536d109a3" />

---
5. Korelasi Antar Variabel

Heatmap korelasi antar variabel numerik. Nilai mendekati +1 atau -1 menunjukkan hubungan yang kuat.
<img width="1199" height="360" alt="image" src="https://github.com/user-attachments/assets/b684d232-a310-48a7-94e8-f4eea0524c4d" />

---
6. Distribusi Data

Distribusi tiap kolom numerik. Membantu mendeteksi pola, skewness, maupun outlier pada data.
<img width="1207" height="370" alt="image" src="https://github.com/user-attachments/assets/3d385e95-4bae-45e0-80c6-81cbb64b1817" />

---
7. Contoh Isi Dataset

Menampilkan beberapa baris data mentah agar bisa dicek langsung format nilai, penulisan item, dan konsistensi data.
<img width="1202" height="375" alt="image" src="https://github.com/user-attachments/assets/9bccc88c-7d84-4493-a030-b15bb4f72ec4" />

---

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

---

<img width="600" height="384" alt="image" src="https://github.com/user-attachments/assets/08db6557-c9c9-4bda-b257-2fb0f7ca91f5" />

---

# 5. Profiling Setelah Cleaning

Membuat laporan kondisi dataset setelah diperbaiki, sehingga bisa dibandingkan dengan versi awal.

profile_after = ProfileReport(df, title="Coffee Shop Profiling - Sesudah Cleaning", explorative=True)
profile_after.to_notebook_iframe()
profile_after.to_file("coffee_shop_after_cleaning.html")

---
1. Ringkasan Dataset (Setelah Cleaning)

Menampilkan kondisi dataset yang sudah diperbaiki: jumlah baris tetap, jumlah kolom, tipe data yang lebih konsisten, serta missing values yang sudah ditangani.
<img width="1416" height="606" alt="image" src="https://github.com/user-attachments/assets/299ad869-1d26-4e73-890b-c078e7c80c34" />

---
2. Data Quality Alerts (Setelah Cleaning)

Peringatan kualitas data jauh berkurang. Kolom yang sebelumnya bermasalah (missing besar, distribusi aneh) sudah diperbaiki.
<img width="1284" height="400" alt="image" src="https://github.com/user-attachments/assets/30c2562a-f5a7-45f6-8bdf-a7f7a7bb1a40" />

---
3. Tipe Variabel (Setelah Cleaning)

Setelah cleaning, kolom numerik sudah dikenali sebagai numerik (Quantity, Price Per Unit, Total Spent). Kolom kategorikal dan datetime juga sudah sesuai.
<img width="1282" height="399" alt="image" src="https://github.com/user-attachments/assets/eb82b1ad-5e3a-42f4-924e-455bae7324f3" />

---
4. Missing Values (Setelah Cleaning)

Grafik missing values menunjukkan hampir semua kolom sudah terisi (tidak ada missing signifikan lagi). Artinya proses imputasi berhasil.
<img width="1279" height="473" alt="image" src="https://github.com/user-attachments/assets/3dbe03c9-4d5d-4c3a-b6ac-beffa956e8b0" />

---
5. Korelasi Antar Variabel (Setelah Cleaning)

Heatmap korelasi terlihat lebih jelas dan bisa dipakai untuk analisis lebih lanjut. Outlier atau missing sebelumnya tidak lagi mengganggu korelasi antar variabel numerik.
<img width="1266" height="466" alt="image" src="https://github.com/user-attachments/assets/a49e2188-5be8-4d39-bb99-5a799db2d4b2" />

---
6. Distribusi Data (Setelah Cleaning)

Distribusi numerik (Quantity, Price Per Unit, Total Spent) terlihat lebih rapi. Outlier sudah berkurang, sehingga grafik lebih representatif.
<img width="1276" height="358" alt="image" src="https://github.com/user-attachments/assets/1e47f980-0e44-49ce-b42a-361c93c0aec5" />

---
7. Contoh Isi Dataset (Setelah Cleaning)

Beberapa baris contoh data setelah diperbaiki. Nilai kosong sudah terisi, tipe data sudah konsisten, sehingga dataset siap dipakai untuk analisis atau modeling.
<img width="1277" height="366" alt="image" src="https://github.com/user-attachments/assets/e04dc6a3-bdfc-47c0-8d46-fb812af1bcda" />

---

# Kesimpulan

Dataset awal mengandung missing values pada beberapa kolom (Item, Quantity, Price Per Unit, Total Spent, Payment Method, Location, Transaction Date).

Tidak ditemukan duplikat signifikan, tetapi tetap dilakukan pengecekan.

Setelah dilakukan cleaning, dataset menjadi lebih konsisten dan siap untuk tahap analisis eksploratif atau model machine learning.

Dua laporan ydata-profiling (before & after cleaning) bisa digunakan sebagai pembanding kualitas data.

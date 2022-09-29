# Laporan Proyek Machine Learning Predictive Analytics - Odi Elsamas


## Project Overview
Stroke adalah kondisi yang terjadi ketika pasokan darah ke otak mengalami gangguan atau berkurang akibat penyumbatan (stroke iskemik) atau pecahnya pembuluh darah (stroke hemoragik). Tanpa pasokan darah, otak tidak akan mendapatkan asupan oksigen dan nutrisi, sehingga sel-sel pada sebagian area otak akan mati. Kondisi ini menyebabkan bagian tubuh yang dikendalikan oleh area otak yang rusak tidak dapat berfungsi dengan baik.

Stroke merupakan kondisi gawat darurat yang perlu ditangani secepatnya, karena sel otak dapat mati hanya dalam hitungan menit. Tindakan penanganan yang cepat dan tepat dapat meminimalkan tingkat kerusakan otak dan mencegah kemungkinan munculnya komplikasi.

Dari latar belakang tersebut saya membuat proyek machine learning ini yang nantinya dapat digunakan untuk melakukan klasifikasi pasien terkena stroke.

## Business Understanding
Dari latar belakang tersebut, masalah yang nantinya akan diselesaikan pada proyek ini adalah:

#### Problem Statement
Menjelaskan pernyataan masalah:
- Dengan data yang dimiliki, fitur apa yang paling berpengaruh untuk memprediksi penyakit stroke.

#### Goals
Mengembangkan model machine learning yang bisa memprediksi klasifikasi penyakit stroke dengan fitur-fitur yang ada.


## Data Understanding
Data yang digunakan pada dataset ini adalah stroke dataset yang di unduh dari [Stroke Predict Dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset). Pada tahap pengerjaan, dataset ini tidak perlu menambahkan data lain. Selain itu terdapat data pada atribut yang bernilai null sehingga perlu melakukan proses data cleaning.

Dataset ini memiliki 5110 data prediksi stroke yang berjumlah 12 kolom atribut dengan 1 target class yaitu stroke. Data pada atribut tersebut yang nantinya digunakan dalam menemukan pola pada data.

Variabel-variabel pada Stroke Prediction dataset adalah sebagai berikut:
- id : merupakan pengenal unik.
- gender : merupakan jenis kelamin pasien yaitu pria dan wanita.
- age : merupakan umur pasien.
- hypertention : merupakan tekanan darah, 0 jika pasien tidak memiliki hipertensi, 1 jika pasien memiliki hipertensi.
- heart_disease : merupakan penyakit jantung, 0 jika pasien tidak memiliki penyakit jantung, 1 jika pasien memiliki penyakit jantung.
- ever_married : merupakan status pernikahan, terdapat ya atau tidak
- work_type : merupakan status, seperti anak-anak, pernah dan tidak pernah bekerja, swasta, wiraswasta.
- Residence_type : merupakan tempat tinggal, terdapat pedesaan dan perkotaan.
- avg_glucose_level : merupakan rata-rata kadar glukosa dalam darah.
- bmi : merupakan indeks masa tubuh.
- smoking_status : merupakan riwayat seperti merokok, tidak pernah merokok, sebelumnya merokok, tidak diketahui.
-  stroke : merupakan penanda, 1 jika pasien mengalami stroke atau 0 jika tidak.

## Data Preparation
Pada bagian ini terdapat beberapa teknik yang diterapkan yang dilakukan untuk persiapan data diantaranya yaitu:

#### Menangani Missing Value
Tahap ini mengecek apakah ada nilai null pada data, setelah di cek ternyata terdapat 201 data yang kosong. Dari gambar box plot terdapat data outlier dimana dapat mempengaruhi nilai mean, solusinya yaitu mengganti nilai null dengan median.

#### Encoding Fitur Kategori
Pada tahap ini yaitu mengubah fitur kategori agar menjadi angka/numerik yang digunakan untuk untuk mendapatkan fitur baru yang sesuai sehingga dapat mewakili variabel kategori. Fitur tersebut adalah gender, ever_merried, work_type, Residence_type dan smoking status.
#### Splitting Data
Pada tahap ini dataset dibagi menjadi data latih (train) dan data uji (test). Data latih digunakan untuk men-training data dan data uji digunakan untuk validasi apakah model telah akurat atau belum. Proposi yang digunakan yaitu 80:20.
#### Reduksi dimensi dengan PCA
Pada tahap ini dilakukan mengurangi jumlah fitur dengan mempertahankan informasi pada data.
- Gunakan n_component = 1, karena kali ini, jumlah komponen kita hanya satu.
- Fit model dengan data masukan.
- Tambahkan fitur baru ke dataset dengan nama 'fitur' dan lakukan proses transformasi.
- Drop kolom 'age', 'bmi'.

#### Standarisasi
Pada tahap ini dilakukan untuk menghindari kebocoran informasi pada data uji, kita hanya akan menerapkan fitur standarisasi pada data latih. Kemudian, pada tahap evaluasi, kita akan melakukan standarisasi pada data uji. Hasil dari tabel menunjukkan, sekarang nilai mean = 0 dan standar deviasi = 1

## Modeling
Pada tahapan model development, model yang digunakan yaitu K-Nearest Neighbor, Random Forest, dan Boosting. Proses modeling yang saya lakukan pada data ini adalah dengan menggabungkan tiga algoritma machine learning kemudian dicari performa yang paling baik dari ketiga algoritma machine learning tersebut.

#### K-Nearest Neighbor
Pada model algoritama ini menggunakan k = 10 tetangga dan metric Euclidean untuk mengukur jarak antara titik.

#### Random Forest
Pada model algoritma ini terdapat beberapa parameter yang di isi dengan nilai :

*   n_estimators = 50 untuk jumlah trees (pohon) di forest
*   max_depth = 16 untuk membagi setiap node ke dalam jumlah pengamatan
*   random_state = 55 untuk mengontrol random number generator 
*   n_jobs = -1  untuk mengontrol thread atau proses yang berjalan secara paralel

#### Boosting
Pada model algoritma ini terdapat beberapa parameter yang di isi dengan nilai :

*   learning_rate = 0.05 bobot yang diterapkan pada setiap regressor di masing-masing proses iterasi
*   random_state = 55 untuk mengontrol random number generator yang digunakan

Berikut hasil dari ketiga model:

 ![result Model](https://github.com/odielsamas/Sistem-Rekomendasi-Tempat-Wisata/blob/main/model_result.png?raw=true)
 
 Dari gambar bar char di atas dari ketiga model algoritma yang saya pakai, bahwa K-Nearest Neighbor lah yang memiliki nilai error yang paling kecil.


## Evaluation
Pada evaluasi metrix model machine learning ini, metrix yang digunakan yaitu mean squared error (mse). MSE pada dasarnya mengukur kesalahan kuadrat rata-rata dari prediksi kita. Untuk setiap poin, dia menghitung selisih kuadrat antara prediksi dan target kemudian merata-rata nilai-nilai itu. makin tinggi nilai ini, makin buruk modelnya. Nilai MSE tidak pernah negatif, karena kita menguadratkan kesalahan prediksi individu sebelum menjumlahkannya, tetapi akan menjadi nol untuk model yang sempurna.

Dari gambar, terlihat bahwa, model K-Nearest Neighbor (KNN) memberikan nilai eror yang paling kecil. Sedangkan model dengan algoritma Boosting memiliki eror yang paling besar (berdasarkan grafik, angkanya di atas 8)

REFERENCES 
[1] Nia Permatasari, "Perbandingan Stroke Non Hemoragik dengan Gangguan Motorik
Pasien Memiliki Faktor Resiko Diabetes Melitus dan Hipertensi", 2020.

---Ini adalah bagian akhir laporan---

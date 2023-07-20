# Laporan Proyek Machine Learning - M. Irfan Gustian

## Kelautan

Kepiting merupakan salah satu komoditi laut yang memiliki nilai cukup tinggi, tingginya harga dari kepiting tidak lain disebabkan oleh permintaan pasar yang tinggi juga. Kepiting menjadi primadona bagi masyarakat dikarenakan rasanya yang enak. Oleh karena itulah bisnis peternakan kepiting menjadi peluang usaha yang cukup menjanjikan. /n
Peternakan kepiting ini tentunya juga memiliki tantangan-tantangan tersendiri, salah satunya adalah dalam menentukan masa panen, masa panen ini menjadi salah satu hal penting perlu diperhatikan karena pertumbuhan kepiting akan melambat setelah melewati usia tertentu, sehingga penting untuk menentukan masa panen terbaik agar biaya peternakan menjadi efisien dan tentunya meningkatkan keuntungan. Pada project ini akan dibangun sebuah model yang mampu membantu pengguna untuk memprediksi umur kepiting berdasarkan dari fitur-fitur seperti berat, tinggi, jenis kelamin dan lain lain.

## Business Understanding



### Problem Statements

Berdasarkan permasalah dan kondisi yang telah dijelaskan sebelumnya, perusahaan akan mengembangkan sebuah sistem prediksi umur kepiting dengan menjawab permasalahan berikut:
- Dari berbagai fitur yang terdapat pada dataset, fitur mana yang memiliki pengaruh paling besar terhadap umur kepiting?
- Perkiraan umur kepiting dengan ukuran dan karakteristik tertentu?

### Goals

Untuk menjawab pertanyaan diatas, Saya akan membuat predictive modelling dengan tujuan sebagai berikut:
- Mengetahui fitur mana yang memiliki korelasi tinggi dengan umur kepiting
- Membuat model machine learning yang mampu memprediksi umur kepiting berdasarkan fitur-fitur yang diberikan

## Data Understanding
Data yang digunakan adalah data mengenai kepiting yang diambil dari website kaggle, data ini terdiri dari 3894 baris data dengan 9 buah fitur/kolom, dengann targetnya adalah umur kepiting. Sumber: [Kaggle](https://www.kaggle.com/datasets/sidhus/crab-age-prediction).

### Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- Sex : jenis kelamin dari kepiting.
- Length : panjang dari kepiting dalam inchi.
- Diameter : diamter dari cangkang kepiting dalam inchi.
- Height : tinggi dari kepiting dalam inchi
- Weight : Berat dari kepiting dalam ounces
- Shucked Weight : berat kepiting tanda cangkang dalam ounces.
- Viscera Weight : Berat yang membungkus organ abdominal di dalam tubuh kepiting dalam ounces.
- Shell Weiight : berat cangkang kepiting dalam ounces.
- Age : Umur kepiting.

![download](https://github.com/IrfanGustian/ML/assets/62733996/1a6c56c7-1884-4ee8-a566-1f655b7d4c76)


## Data Preparation
Terdapat beberapa teknik yang digunakan di dalam proses data preparation ini. Yang pertama adala mengecek apakah terdapat nilai null di dalam dataset, dari 3893 baris data dan 9 kolom tidak terdapat data dengan nilai null sehingga tidak ada tindakan yang dilakukan untuk mengatasi nilai null.
Selanjutnya adalah melihat apakah terdapat nilai 0 di dalam dataset yang digunakan, setelah dilakukan pengecekan didapatkan bahwa nilai min pada fitur height adalah 0, ini berarti terdapat nilai 0 pada fitur height yang perlu diperbaiki karena tinggi kepiting tidak mungkin 0. Baris yang terdapat nilai nol di drop.
Selanjutnya adalah melakukan pembersihan outliars dengan teknik IQR, setelah dilakukan pembersihan outliar jumlah data menjadi 3526.
Pada dataset juga diterapkan teknik PCA untuk mereduksi jumlah fitur yang digunakan.
Sebelum masuh untuk pelatihan, dataset terlebih dahulu dipepcah menjadi data latih dan data test.

## Modeling
Model yang digunakan dalam proses modelling ini ada 3 jenis, yaitu Boosting, KNN, dan Random Forest.
Parameter yang digunakan untuk Boosting yaitu learning_rate = 0.05, random_state=55.
Parameter yang digunakan untuk KNN yaitu n_neighbors = 10.
Parameter yang digunakan unuk RandomForest yaitu n_estimators=50, max_depth=16, random_state=55, n_jobs=-1.
Dari ketiga model diatas, model yang mampu memberikan performa terbaik adalah random forest, oleh karena itu model akhir yang digunakan adalah random forest.

## Evaluation
Metrik yang digunakan untuk evaluasi adalah MSE(mean squared error). Nilai mse akan dihitung untuk setiap model yang digunakan. Darih hasil perhitungan MSE yang dilakukan, didapatkan hasil sebagai berikut:
- Boosting : train= 0.003231,	test = 0.003537
- KNN : train = 0.002891	test = 0.003883
- RF : train 0.001192	test = 0.004164

Selanjutnya juga dilakukan pengujian untuk 1 buah data dengan nilai target asli 7 dengan hasil sebagai berikut:
- Boosting : 7.4
- KNN : 6.6
- RF : 7

Dari Ketiga hasil diatas, dapat dilihat bahwa RF mampu memberikan akurasi untuk data test paling baik dan hasil prediksi paling tepat, oleh karena itulah model RF yang digunakan.

Untuk Menjawab fitur mana yang paling berpengaruh terhadap target atau Age, maka digunakanlah correlation matrix. Dari hasil perhitungan ini didapatkan bahwa fitur Shell Weight, Height dan Diameter lah yang memiliki korelasi terbesar terhadap umur kepiting dengan nilai korelasi berturut-turut 0.62, 0.61 dan 0.6


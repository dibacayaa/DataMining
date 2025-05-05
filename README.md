# DataMining
Laporan Analisis Kode
1. Deskripsi Umum
Kode ini adalah skrip Python yang dibuat secara otomatis dari Google Colab. Tujuan utamanya adalah:
Mengunduh dataset laporan kecelakaan di Nashville (Januari 2018 - April 2025) dari Kaggle.
Melakukan praproses data.
Melatih model klasifikasi menggunakan Decision Tree untuk memprediksi apakah suatu kecelakaan termasuk kategori Hit and Run.
Menampilkan visualisasi pohon keputusan dan mencetak akurasi model.

2. Struktur dan Alur Kode
Import Library
kagglehub: Untuk mengunduh dataset dari Kaggle.
os: Untuk menangani operasi file dan folder.
pandas: Untuk manipulasi data.
sklearn.model_selection: Untuk membagi dataset.
sklearn.tree: Untuk membangun dan memvisualisasi model Decision Tree.
matplotlib.pyplot: Untuk visualisasi grafik.
Unduh Dataset
```
python
path = kagglehub.dataset_download("justinwilcher/nashville-accident-reports-jan-2018-apl-2025")
```
Periksa Isi Folder Dataset
```
python
for filename in os.listdir(dataset_folder):
    print(filename)
```
Baca Dataset
```
python
df = pd.read_csv(file_path)
```
Menampilkan:
Lima baris pertama.
Nama-nama kolom.
Praproses Data
Menghapus baris dengan nilai kosong pada kolom berikut:
'Number of Motor Vehicles'
'Zip Code'
'Number of Injuries'
'Accident Number'
'Hit and Run'
Pisahkan Fitur dan Label
Fitur (x): 'Number of Motor Vehicles', 'Zip Code', 'Number of Injuries', 'Accident Number'
Label (y): 'Hit and Run'
Split Data
Membagi dataset menjadi data latih (80%) dan data uji (20%).
Latih Model Decision Tree
```
python
dtree = DecisionTreeClassifier(max_depth=3)
dtree.fit(x_train, y_train)
```
Model menggunakan pohon keputusan dengan kedalaman maksimum 3.
Evaluasi Model
Menghitung akurasi pada data uji:
```
python
accuracy = dtree.score(x_test, y_test)
```
Visualisasi Pohon Keputusan
```
python
plot_tree(dtree, filled=True)
plt.show()
```
3. Catatan Teknis
Tidak ada penanganan terhadap data kategorikal jika muncul dalam dataset.
Tidak ada standarisasi atau normalisasi fitur numerik.
Tidak ada cross-validation, hanya single train-test split.
Zip Code dan Accident Number digunakan sebagai fitur numerik, padahal mungkin lebih tepat diperlakukan sebagai kategori.
Tidak ada laporan metrik selain akurasi (misalnya precision, recall, F1-score).
Visualisasi pohon keputusan dibuat cukup besar (figsize=(30, 20)).

4. Rekomendasi Perbaikan
Tambahkan analisis eksplorasi data (EDA) sebelum pemodelan.
Periksa distribusi data dan lakukan encoding pada variabel kategorikal.
Pertimbangkan feature engineering untuk meningkatkan performa model.
Tambahkan metrik evaluasi lain selain akurasi.
Lakukan hyperparameter tuning dan/atau cross-validation.

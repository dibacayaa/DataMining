# DataMining
📄 Laporan Analisis Kode
1. Tujuan Kode
Kode ini digunakan untuk:
•	Mengunduh dataset laporan kecelakaan di Nashville dari Kaggle.
•	Melakukan preprocessing data.
•	Membangun dan mengevaluasi model klasifikasi pohon keputusan (Decision Tree) untuk memprediksi apakah suatu kecelakaan adalah “Hit and Run” (tabrak lari).

2. Detail Langkah-langkah Kode
a. Import Library
•	kagglehub → untuk mengunduh dataset dari Kaggle.
•	os → untuk mengakses file dan folder.
•	pandas → untuk manipulasi data.
•	sklearn.model_selection → untuk membagi data menjadi train/test.
•	sklearn.tree → untuk membuat dan memvisualisasikan Decision Tree.
•	matplotlib.pyplot → untuk menampilkan grafik pohon keputusan.
b. Unduh Dataset
path = kagglehub.dataset_download("justinwilcher/nashville-accident-reports-jan-2018-apl-2025")
Dataset “Nashville Accident Reports Jan 2018 - Apr 2025” diunduh dari Kaggle.
c. Cek isi folder dataset
for filename in os.listdir(dataset_folder):
    print(filename)
Menampilkan nama-nama file dalam folder dataset untuk memastikan file CSV yang akan diproses.
d. Baca dataset
df = pd.read_csv(file_path)
Dataset CSV dibaca ke dalam DataFrame pandas.

e. Tampilkan data awal
print(df.head())
print(df.columns)
Menampilkan 5 baris pertama dan daftar nama kolom.
f. Bersihkan data (data cleaning)
df = df.dropna(subset=['Number of Motor Vehicles', 'Zip Code', 'Number of Injuries','Accident Number','Hit and Run'])
Menghapus baris yang memiliki nilai kosong (NA) di kolom penting.
g. Persiapkan fitur dan target
x = df[['Number of Motor Vehicles','Zip Code','Number of Injuries','Accident Number']]
y = df['Hit and Run']
•	x = variabel input (fitur).
•	y = target yang diprediksi.
h. Split data
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.2, random_state=42)
Membagi data menjadi:
•	80% data pelatihan.
•	20% data pengujian.

i. Buat dan latih model
dtree = DecisionTreeClassifier(max_depth=3)
dtree.fit(x_train, y_train)
Model Decision Tree dibuat dengan kedalaman maksimal 3 untuk mencegah overfitting.
j. Evaluasi model
accuracy = dtree.score(x_test, y_test)
print(f"Akurasi model: {accuracy*100:.2f}%")
Menghitung dan menampilkan akurasi model pada data pengujian.
k. Visualisasi pohon keputusan
plt.figure(figsize=(30, 20))
plot_tree(dtree, filled=True)
plt.show()
Menampilkan diagram pohon keputusan secara visual.
📊 Ringkasan Output
•	Menampilkan nama file di folder dataset.
•	Menampilkan 5 baris pertama data.
•	Menampilkan daftar kolom.
•	Menampilkan akurasi model dalam persentase.
•	Menampilkan visual pohon keputusan.
⚠️ Catatan & Potensi Perbaikan
✅ Dataset hanya difilter berdasarkan NA, tidak ada eksplorasi atau analisis lebih dalam.
✅ Tidak ada proses encoding untuk data kategorikal (kalau ada).
✅ Model hanya memakai 4 fitur sederhana; mungkin perlu fitur tambahan atau teknik feature engineering.
✅ Tidak ada metrik evaluasi lain seperti confusion matrix, precision, recall, atau F1-score.
✅ Tidak ada penyimpanan model atau hasil visualisasi.

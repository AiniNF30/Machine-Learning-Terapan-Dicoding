# Machine Learning Terapan - Aini Nurpadilah

## Domain Proyek

![wisata](https://user-images.githubusercontent.com/90955264/221451450-1fa788f7-e846-4d6a-9be9-7188153083e2.png)

informasi tentang kunjungan wisatawan ke beberapa destinasi wisata utama di Indonesia. Dataset ini dikumpulkan oleh Kementerian Pariwisata dan Ekonomi Kreatif Indonesia, dan kemudian dibagikan di platform Kaggle untuk digunakan oleh para pengembang data dan ilmuwan.

Latar belakang dari proyek ini adalah untuk memberikan informasi tentang tren kunjungan wisatawan ke Indonesia, khususnya ke beberapa destinasi wisata utama di negara ini. Data ini meliputi jumlah kunjungan wisatawan ke berbagai destinasi wisata di Indonesia, asal negara pengunjung, jenis wisata yang dilakukan, serta jumlah pengeluaran wisatawan selama berkunjung di Indonesia. Informasi ini dapat membantu pengembang pariwisata dan pemerintah dalam merencanakan pengembangan pariwisata di Indonesia serta meningkatkan pelayanan bagi para wisatawan.


## Business Understanding

### Problem Statements
* Destinasi wisata mana yang paling banyak dikunjungi dan diminati oleh wisatawan di Indonesia?
* Bagaimana tren kunjungan wisatawan ke Indonesia dalam beberapa tahun terakhir?

### Goals
Tujuan utamanya adalah :
* Dengan mengetahui destinasi wisata yang paling banyak dikunjungi dan jenis wisata yang paling diminati, dapat membantu dalam perencanaan promosi dan pengembangan infrastruktur wisata yang lebih baik dan sesuai dengan kebutuhan wisatawan. 
* analisis tren kunjungan wisatawan dalam beberapa tahun terakhir dapat memberikan gambaran tentang perubahan perilaku dan kebutuhan wisatawan, sehingga dapat membantu dalam pengembangan strategi pemasaran yang lebih efektif dan mengikuti perkembangan tren wisatawan.

### Solution Statement.
Beberapa langkah yang dapat dilakukan dalam proses analisis data adalah:

  1. Melakukan eksplorasi data dan cleaning data untuk memastikan kualitas dan  integritas data.
  2. Melakukan analisis deskriptif untuk mengetahui distribusi data dan     karakteristik setiap variabel dalam dataset.
  3. Melakukan analisis korelasi untuk mengetahui hubungan antara variabel-variabel dalam dataset.
  4. Melakukan analisis sentimen terhadap data rating pengunjung terhadap tempat wisata.
  5. Membuat model rekomendasi tempat wisata berdasarkan data user dan rating pengunjung.


## Data Undestanding
Dataset yang digunakan adalah [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination)
Dataset ini merupakan dataset yang memuat beberapa tempat wisata di 5 kota besar di Indonesia yaitu Jakarta, Yogyakarta, Semarang, Bandung, Surabaya. 
Dataset Kaggle "Indonesia Tourism Destination" terdiri dari tiga file data, yaitu:

#### tourism__with__id.csv

  - Place_Id: id unik untuk setiap tempat wisata
  - Place_Name: nama tempat wisata
  - Description: deskripsi singkat tentang tempat wisata
  - Category: kategori tempat wisata (misalnya wisata alam, wisata sejarah,    wisata budaya)
  - City: kota tempat wisata tersebut berada
  - Price: harga tiket masuk ke tempat wisata dalam rupiah
  - Rating: rating tempat wisata dalam skala 1-5
  - Time_Minutes: waktu yang diperlukan untuk mengunjungi tempat wisata dalam menit
  - Coordinate: koordinat tempat wisata dalam format latitude dan longitude
  - Lat: nilai latitude tempat wisata
  
#### user.csv

File ini berisi data dummy pengguna yang akan digunakan untuk membuat fitur rekomendasi berdasarkan pengguna. Terdapat 3 variabel dalam file ini, yaitu:

  - User_Id: id unik untuk setiap pengguna
  - Location: kota asal pengguna
  - Age: usia pengguna
  - tourism_rating.csv

File ini berisi informasi tentang rating yang diberikan oleh pengguna pada setiap tempat wisata yang dikunjungi. Terdapat 3 variabel dalam file ini, yaitu:

  - User_Id: id unik untuk setiap pengguna
  - Place_Id: id unik untuk setiap tempat wisata
  - Place_Ratings: rating yang diberikan oleh pengguna pada tempat wisata tersebut dalam skala 1-5


## Data Preparation
Teknik yang digunakan pada tahapan Data Preparation adalah vektorisasi fungsi CountVectorizer dari library scikit-learn. CountVectorizer digunakan untuk mengubah teks yang diberikan menjadi vektor berdasarkan frekuensi (jumlah) setiap kata yang muncul di seluruh teks.

CountVectorizer membuat matriks di mana setiap kata unik diwakili oleh kolom matriks, dan setiap sampel teks dari dokumen adalah baris dalam matriks. Nilai setiap sel tidak lain adalah jumlah kata dalam sampel teks tertentu.

Pada proses vektorisasi ini, digunakan metode sebagai berikut.

    1. fit metode berfungsi untuk melakukan perhitungan idf pada data
    2. get_feature berfungsi untuk melakukan mapping array dari fitur index integer ke fitur nama
    3. fit_transform berfungsi untuk mempelajari kosa kata dan Inverse Document Frequency (IDF) dengan memberikan nilai return berupa document-term matrix
    4. todense berfungsi untuk mengubah vektor tf-idf dalam bentuk matriks
    
## Modeling

#### content-based filtering

Model machine learning yang digunakan pada sistem rekomendasi ini adalah model content-based filtering dengan simlarty measure yang digunakan adalah Cosine Similarity.

Model content-based filtering ini bekerja dengan mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Metode ini bekerja dengan menyarankan item serupa yang pernah disukai sebelumnya atau sedang dilihat sekarang kepada pengguna berdasrakan kategori tertentu dari item yang dinilai oleh pengguna dengan menggunakan similarity tertentu.

Sedangkan cosine similarity adalah salah satu teknik mengukur kesamaan yang bekerja dengan mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama dengan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity.

untuk memperoleh rekomendasi destinasi wisata , gunakan fungsi model.predict() dari library Keras dengan menerapkan kode berikut.
ini adalah 10 rekomendasi wisata 

| No|Name| Category  | Decription  |City   | City_Category|
|---|----|---|---|---|---|
| 1.  | Atlantis Water Adventure  | Taman Hiburan  | Atlantis Water Adventure atau dikenal dengan A...	  |  Jakarta |Jakarta Taman Hiburan  |
| 2.  | Museum Bank Indonesia	 |   Budaya| Museum Bank Indonesia adalah sebuah museum di ...  |  Jakarta | Jakarta budaya |
| 3.  | Pintoe Langit Dahromo  | Cagar Alam  | Pintu Langit Dahromo ini menyediakan berbagai ...  | Yogyakarta  | Yogyakarta Cagar Alam |
| 4.  | Wisata Agro Edukatif Istana Susu Cibugary  |  Taman Hiburan |  Kawasan Wisata Agro Edukatif Istana Susu “Cibu...	 |  Jakarta | Jakarta Taman Hiburan |
| 5.  | Sumur Gumuling  |   Taman Hiburan |  Sumur Gumuling adalah salah satu tempat untuk ... | Yogyakarta  |Yogyakarta Taman Hiburan  |
| 6.  | Pasar Taman Puring  |  Pusat Perbelanjaan | Taman Puring bukanlah taman secara harfiah. Se...  |   Jakarta | Jakarta Pusat Perbelanjaan |
| 7.  | Masjid Istiqlal  | Tempat Ibadah  |Masjid Istiqlal (arti harfiah: Masjid Merdeka)...| Jakarta  |  Jakarta Tempat Ibadah|
| 8.  | Pantai Baron |  Bahari  | Pantai Baron adalah salah satu objek wisata be... |  Yogyakarta  |Yogyakarta Bahari | 
| 9.  | Taman Spathodea  |  Taman Hiburan  | Objek Wisata Taman Spathodea di Jagakarsa DKI ...  |  Jakarta | Jakarta Taman Hiburan |
| 10. | Monumen Nasional  |Budaya   |Monumen Nasional atau yang populer disingkat d...| Jakarta  | Jakarta Budaya |



Model machine learning yang digunakan pada sistem rekomendasi ini adalah model content-based filtering dengan similarity measure yang digunakan adalah Cosine Similarity.

#### collaborative filtering.
<img width="429" alt="Screenshot 2023-02-27 at 21 06 11" src="https://user-images.githubusercontent.com/90955264/221584699-4a94bd88-ead7-4709-8152-0863b5bcfa73.png">

Pada tahap awal, dilakukan penggabungan antara data wisata dan data rating menjadi satu data frame dengan menggunakan fungsi merge pada library pandas. Selanjutnya, dilakukan pembuatan model content-based filtering dengan algoritma Cosine Similarity. Proses ini melibatkan perhitungan similarity antara data wisata dengan data rating yang dimiliki oleh user, sehingga model dapat merekomendasikan wisata yang mirip dengan preferensi wisatawan berdasarkan kesamaan fitur.

<img width="746" alt="Screenshot 2023-02-27 at 18 08 59" src="https://user-images.githubusercontent.com/90955264/221548466-94823d54-3a34-4889-b111-ade89cd5f91b.png">


Pada proses di atas, dilakukan proses pembuatan user-item matrix yang akan digunakan sebagai acuan dalam proses rekomendasi. Kemudian, NaN values pada user-item matrix diubah menjadi 0. Selanjutnya, dilakukan perhitungan Cosine Similarity matrix antara data wisata dan data rating yang dimiliki oleh user.

Setelah mendapatkan Cosine Similarity matrix, langkah selanjutnya adalah membuat fungsi untuk melakukan proses rekomendasi berdasarkan input dari user. Pada sistem rekomendasi ini, fungsi rekomendasi yang dibuat akan menghasilkan 5 rekomendasi wisata yang paling sesuai dengan preferensi yang dimiliki oleh user.

<img width="1246" alt="Screenshot 2023-02-27 at 17 08 51" src="https://user-images.githubusercontent.com/90955264/221535037-7f77527e-c04e-47b1-998b-7c03b7120435.png">

Pada fungsi rekomendasi di atas, dilakukan proses pencarian similarity scores antara user yang sedang login dengan user lainnya pada Cosine Similarity matrix. Kemudian, similarity scores diurutkan dari yang terbesar hingga terkecil, dan diambil 5 user dengan similarity scores terbesar sel.

## Evaluation


### 1.  hasil Evaluasi untuk Content Based Filtering
disini saya merekomendasikan wisata Air Mancur Menari dan Trans Studio Bandung

<img width="821" alt="Screenshot 2023-02-27 at 20 58 22" src="https://user-images.githubusercontent.com/90955264/221583000-96c6adec-8baf-4e0e-9258-7d4a4c8b1e75.png">

<img width="807" alt="Screenshot 2023-02-27 at 20 58 28" src="https://user-images.githubusercontent.com/90955264/221583030-a45e8b9b-a829-4264-9d4f-deb623029ae4.png">

Berdasarkan hasil rekomendasi di atas, dapat disimpulkan bahwa Wisata Air Mancur Menari termasuk dalam kota Surabaya, sementara Wisata Trans Studio Bandung termasuk dalam kota Bandung. Dalam kedua kasus tersebut, kelima item yang direkomendasikan memiliki kategori yang sama dengan kota tersebut. Dengan demikian, sistem rekomendasi memiliki precision yang sangat baik, Artinya, precision sistem kita sebesar 5/5 atau sebesar 100% untuk kedua kasus tersebut.

### 2. hasil Evaluasi untuk Collaborative Filtering

Dalam proses evaluasi, akan disajikan informasi mengenai perbandingan mengenai model pertama dan kedua melalui dua metrik berikut:

Loss (Mean Squared Error Loss)
Mean Squared Erorr Loss berfungsi untuk menghitung rata-rata kuadrat kesalahan antara label dan prediksi. Dengan demikian semakin rendahnya nilai loss (mean squared error loss) maka semakin baik dan akurat model yang dibuat. Berikut adalah hasil perbandingan loss dan val_loss pada kedua model yang telah dibuat.

Metric yang digunakan pada sistem rekomendasi wisata dengan menggunakan accuracy precision. Precision adalah metrik yang membandingkan rasio prediksi benar atau positif dengan keseluruhan hasil yang diprediksi positif dengan rumus.

<img width="509" alt="Screenshot 2023-02-27 at 17 19 02" src="https://user-images.githubusercontent.com/90955264/221537298-0bba8751-d3dd-49ef-8387-f9a533a313d9.png">

Grafik loss dan val_loss menunjukkan bagaimana performa model machine learning dalam mengestimasi target output berdasarkan data input. Loss atau kerugian adalah selisih antara nilai prediksi yang dihasilkan oleh model dengan nilai sebenarnya pada dataset.

Pada grafik tersebut, terlihat bahwa loss dan val_loss bergerak turun (menurun) dari epoch ke epoch. Namun, terlihat juga bahwa val_loss memiliki fluktuasi yang lebih besar dibandingkan dengan loss.

Hal ini mungkin terjadi karena saat melatih model, model menjadi terlalu terfokus pada data training (loss) dan tidak mampu melakukan generalisasi dengan baik pada data yang belum pernah dilihat sebelumnya (val_loss). Oleh karena itu, fluktuasi val_loss menjadi lebih besar karena model cenderung overfitting.

Untuk meminimalkan fluktuasi val_loss, beberapa teknik seperti dropout, regularisasi, atau penambahan data dapat dilakukan untuk membantu model melakukan generalisasi dengan lebih baik pada data baru. Selain itu, pengaturan hyperparameter seperti learning rate dan jumlah epoch juga dapat mempengaruhi performa model pada data validasi.



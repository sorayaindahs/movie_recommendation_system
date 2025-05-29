# Laporan Proyek Machine Learning - Soraya Indah Setiani

## Project Overview

Kemudahan akses internet saat ini telah mengubah kebiasaan menonton acara TV dan film. Platform penyedia film seperti Netflix, HBO Max, dan Disney+ menawarkan fleksibilitas tinggi bagi pengguna untuk menikmati film kapan saja dan di berbagai perangkat. Setiap platform menyediakan berbagai film dengan jumlah yang sangat banyak. Pengguna platform yang ingin menonton film akan membutuhkan waktu yang cukup lama untuk memilih film dan film yang telah dipilih belum tentu memenuhi harapan atau keinginan penonton setelah menonton, sehingga waktu yang terbuang menjadi lebih banyak.

Banyaknya pilihan film yang tersedia membuat keberadaan sistem rekomendasi menjadi sangat krusial untuk membantu pengguna menemukan konten yang sesuai dengan preferensi mereka. Berdasarkan sisi bisnis, sistem rekomendasi juga berperan penting dalam meningkatkan durasi aktivitas pengguna di platform yang pada gilirannya dapat meningkatkan pendapatan platform tersebut. Oleh karena itu, sistem rekomendasi menjadi fitur yang wajib dimiliki oleh platform penyedia film.

Referensi:

Arfisko, H. H., & Wibowo, A. T. (2022). Sistem rekomendasi film menggunakan metode hybrid collaborative filtering dan content-based filtering. e-Proceeding of Engineering, 9(3), 2149–2159. https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/18066

Purnomo, A. A., Pratiwi, N. F., & Wahyudi, R. A. (2023). Implementasi sistem rekomendasi menggunakan metode collaborative filtering pada platform streaming film. Jurnal Pengembangan Teknologi Informasi dan Ilmu Komputer, 7(2), 1093–1101. https://doi.org/10.25126/j-ptiik.2023719251.


## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang menyatakan bahwa kebutuhan sistem rekomendasi sangat krusial untuk pengguna dan platform yang digunakan, dapat dirumuskan beberapa problem statements berikut.

- Bagaimana sistem rekomendasi dapat membantu pengguna dalam menemukan film yang sesuai dengan preferensi mereka secara lebih efisien?

- Sistem rekomendasi apa yang paling efektif dalam menghasilkan rekomendasi film?

- Bagaimana pengaruh penerapan sistem rekomendasi terhadap peningkatan durasi penggunaan platform penyedia film oleh pengguna?

### Goals

- Menganalisis peran sistem rekomendasi dalam mempermudah pengguna menemukan film yang sesuai dengan minat dan preferensi mereka.

- Membangun sistem rekomendasi film yang efektif dan akurat, seperti menggunakan pendekatan content based filtering dan collaborative filtering.

- Melihat kemungkinan pengaruh penerapan sistem rekomendasi terhadap pengalaman pengguna dan potensi peningkatan keterlibatan pengguna pada platform penyedia film.

### Solution statements
- Membangun Model Sistem Rekomendasi Menggunakan Content Based Filtering.

Pendekatan content based filtering membantu pengguna menemukan film yang sesuai dengan preferensi masing-masing. Pendekatan ini bekerja dengan menganalisis karakteristik yang sebelumnya disukai oleh pengguna kemudian merekomendasikan film lain yang serupa. Pendekatan ini membuat pengguna akan mendapatkan rekomendasi film yang lebih relevan secara personal tanpa mempertimbangkan opini pengguna lain.

- Membangun Model Sistem Rekomendasi Menggunakan Collaborative Filtering.

Pendekatan collaborative filtering akan memanfaatkan pola perilaku pengguna dalam memberikan penilaian terhadap film. Sistem akan mencari kesamaan antara pengguna (user-based) atau antara item yang dinilai (item-based) untuk merekomendasikan film yang disukai oleh pengguna lain dengan pola yang serupa. Pendekatan ini mampu memberikan rekomendasi yang lebih bervariasi.

## Data Understanding

Data yang digunakan untuk membangun sistem rekomendasi film adalah dataset genre dan rating. Dataset genre berisidaftar film yang disediakan dan dataset rating berisi penilaian pengguna pada film tersebut. 

Dataset diperoleh dari tautan berikut:

https://www.kaggle.com/code/mehmetisik/user-based-collaborative-filtering/input

Dataset genre.csv akan berguna untuk membangun model sistem rekomendasi content based filtering dan dataset rating.csv akan berguna untuk membangun sistem rekomendasi collaborative filtering.


### Data Loading
**Dataset genre**

    | movieId | Title                               | Genres                                      |
    |---------|-------------------------------------|---------------------------------------------|
    | 1       | Toy Story (1995)                    | Adventure\|Animation\|Children\|Comedy\|Fantasy |
    | 2       | Jumanji (1995)                      | Adventure\|Children\|Fantasy                |
    | 3       | Grumpier Old Men (1995)             | Comedy\|Romance                             |
    | 4       | Waiting to Exhale (1995)            | Comedy\|Drama\|Romance                      |
    | 5       | Father of the Bride Part II (1995)  | Comedy                                      |
    | ...     | ...                                 | ...                                         |
    | 131254  | Kein Bund für's Leben (2007)        | Comedy                                      |
    | 131256  | Feuer, Eis & Dosenbier (2002)       | Comedy                                      |
    | 131258  | The Pirates (2014)                  | Adventure                                   |
    | 131260  | Rentun Ruusu (2001)                 | *(no genres listed)*                        |
    | 131262  | Innocence (2014)                    | Adventure\|Fantasy\|Horror                  |
27278 rows × 3 columns

**Dataset rating**

    | Index   | userId | movieId | rating | timestamp           |
    |---------|--------|---------|--------|---------------------|
    | 0       | 1      | 2       | 3.5    | 2005-04-02 23:53:47 |
    | 1       | 1      | 29      | 3.5    | 2005-04-02 23:31:16 |
    | 2       | 1      | 32      | 3.5    | 2005-04-02 23:33:39 |
    | 3       | 1      | 47      | 3.5    | 2005-04-02 23:32:07 |
    | 4       | 1      | 50      | 3.5    | 2005-04-02 23:29:40 |
    | ...     | ...    | ...     | ...    | ...                 |
    | 1048570 | 7120   | 168     | 5.0    | 2007-04-02 19:44:21 |
    | 1048571 | 7120   | 253     | 4.0    | 2007-04-02 19:30:25 |
    | 1048572 | 7120   | 260     | 5.0    | 2007-04-02 19:27:15 |
    | 1048573 | 7120   | 261     | 4.0    | 2007-04-02 19:49:36 |
    | 1048574 | 7120   | 266     | 3.5    | 2007-04-02 19:34:14 |
    1048575 rows × 4 columns


### Deskripsi Variabel

    | #   | Column   | Non-Null Count | Dtype  |
    |-----|----------|----------------|--------|
    | 0   | movieId  | 27278 non-null | int64  |
    | 1   | title    | 27278 non-null | object |
    | 2   | genres   | 27278 non-null | object |
    dtypes: int64(1), object(2)
    
Dataset genre 

Dataset genre erdiri dari **27278 baris** dan **3 kolom** dengan keterangan sebagai berikut.
- movieId: ID movie (int64)
- title: judul movie (object)
- genres: Kategori movie (object)

Setiap kolom memiliki jumlah baris yang sama, yaitu 27278.

Dataset rating

    | #   | Column     | Non-Null Count    | Dtype   |
    |-----|------------|-------------------|---------|
    | 0   | userId     | 1048575 non-null  | int64   |
    | 1   | movieId    | 1048575 non-null  | int64   |
    | 2   | rating     | 1048575 non-null  | float64 |
    | 3   | timestamp  | 1048575 non-null  | object  |
    dtypes: float64(1), int64(2), object(1)
    
Dataset rating terdiri dari **1048575 baris** dan **4 kolom** dengan keterangan sebagai berikut.

- userId: ID pengguna yang memberi rating (int64)
- movieId: ID movie (int64)
- rating: Penilaian dari user untuk movie (float64)
- timestamp: Waktu saat rating diberikan, dalam format waktu dan tanggal (object)

Setiap kolom memiliki jumlah baris yang sama, yaitu 1048575.

### **Univariate Exploratory Data Analysis**

#### **Identifikasi Missing Value dan Outlier di Setiap Kolom**.
Tahap ini akan mengidentifikasi nilai yang hilang pada setiap kolom dan nilai-nilai yang tidak relevan.


##### **Kolom movieId**
Berdasarkan identifikasi yang telah dilakukan, diperoleh informasi bahwa:
- Terdapat 27278 movieId yang berarti platform menyediakan 27278 movie untuk pengguna.
- Tidak terdapat missing value pada kolom movieId.

##### **Kolom title**
Berdasarkan identifikasi yang telah dilakukan, diperoleh informasi bahwa:
- Terdapat 27262 title yang berarti platform menyediakan 27262 judul movie untuk pengguna.
- Tidak terdapat missing value pada kolom title.
- Perbedaan jumlah movieId (27278) dan jumlah title (27262) bukan disebabkan oleh missing value kemungkinan besar karena adanya kesamaan judul film dengan movieId berbeda. Bisa jadi karena perbedaan versi atau adanya remake. Berikut identifikasi judul film yang sama dengan movieId berbeda.
  
      | title                                 | count  |
      |---------------------------------------|--------|
      | Blackout (2007)                       | 2      |
      | Girl, The (2012)                      | 2      |
      | Clear History (2013)                  | 2      |
      | Aladdin (1992)                        | 2      |
      | Chaos (2005)                          | 2      |
      | Beneath (2013)                        | 2      |
      | Offside (2006)                        | 2      |
      | Hamlet (2000)                         | 2      |
      | 20,000 Leagues Under the Sea (1997)   | 2      |
      | Casanova (2005)                       | 2      |
      | Emma (1996)                           | 2      |
      | Paradise (2013)                       | 2      |
      | Darling (2007)                        | 2      |
      | Men with Guns (1997)                  | 2      |
      | Johnny Express (2014)                 | 2      |
      | War of the Worlds (2005)              | 2      |
  
- Terdapat 16 film dengan judul film yang sama dan movieId berbeda. Hal ini masuk akal jika terdapat 27278 movideId dan 27262 title.

##### **Kolom genres**
Berdasarkan identifikasi yang telah dilakukan, diperoleh informasi bahwa:
- Identifikasi menunjukkan 0 missing value.
- Terdapat 24 genre, yaitu 

            ['(no genres listed)', 'Action', 'Adventure', 'Animation', 'Children', 'Comedy', 'Crime', 'Documentary', 'Drama', 'Fantasy', 'Film-Noir', 'Horror', 'IMAX', 'Musical', 'Mystery', 'Romance', 'Sci-Fi', 'Thriller', 'War', 'Western']

- Terdapat 246 movie  yang tidak tertulis genre (no genres listed). Hal ini tidak perlu dilakukan penanganan, seperti missing value karena akan menghapus banyak informasi. Meskipun akan sedikit mengganggu pada sistem rekomendasi content based, hal ini tidak terlalu bermasalah untuk penerapan collaborative filtering.

##### **Kolom userId**
Berdasarkan identifikasi yang telah dilakukan, diperoleh informasi bahwa tidak terdapat missing value pada kolom userId dan terdapat 7120 users yang memberi rating pada movie.

##### **Kolom rating**
Berdasarkan identifikasi yang telah dilakukan, diperoleh informasi bahwa tidak terdapat missing value dan outlier pada kolom rating karena semua nilai berada pada rentang penilaian, yaitu 0.5 sampai 5.

##### **Kolom timestamp**
Sebelum membangun model, perlu mengetahui kolom yang tidak akan digunakan dalam membangun sistem rekomendasi, seperti kolom timestamp. Kolom ini akan dihapus untuk mempermudah pemodelan. Penghapusan kolom timestamp akan dilakukan pada data preprocessing.

#### **Identifikasi Duplikasi Data**
Berdasarkan identifikasi, tidak terdapat duplikasi data yang perlu ditangani.

## Data Preparation - Content Based Filtering
Dataset yang digunakan dalam content based filtering adalah dataset genre saja tanpa digabung dengan rating. Sebelum membangun model, dataset genre_id yang telah siap dapat assign ke variabel data. Berikut contoh sampel:

    |        | movieId | title                                      | genres         |
    |--------|---------|--------------------------------------------|----------------|
    | 1214   | 1242    | Glory (1989)                               | Drama|War      |
    | 22279  | 107130  | Adventure in Space and Time, An (2013)     | Drama          |
    | 20753  | 101592  | Bird of the Air, A (Loop, The) (2011)      | Drama|Romance  |
    | 9761   | 31705   | Beautiful Boxer (2003)                     | Action|Drama   |
    | 11291  | 47935   | Overlord (1975)                            | Drama|War      |

### **TF-IDF Vectorizer**
Model sistem rekomendasi sederhana akan dibangun berdasarkan genre dari movie. Teknik TF-IDF Vectorizer akan digunakan pada sistem rekomendasi untuk menemukan representasi fitur penting dari setiap genre movie.
Tahapan yang dilakukan untuk TF-IDF Vectorizer adalah:
- Inisialisasi TfidfVectorizer
- Melakukan perhitungan idf pada data genres
- Mapping array dari fitur index integer ke fitur nama

            array(['action', 'adventure', 'animation', 'children', 'comedy', 'crime',
            'documentary', 'drama', 'fantasy', 'fi', 'film', 'genres',
            'horror', 'imax', 'listed', 'musical', 'mystery', 'no', 'noir',
            'romance', 'sci', 'thriller', 'war', 'western'], dtype=object)

- Melakukan fit lalu ditransformasikan ke bentuk matrix
- Melihat ukuran matrix TF-IDF

       (27278, 24)

Matriks berukuran (27278, 24). Nilai 1048575 merupakan ukuran data dan 24 merupakan matriks genre.

- Mengubah vektor tf-idf dalam bentuk matriks dengan fungsi todense() 
Matriks tf-idf untuk beberapa judul movie (title) dan genre movie (genres).

        matrix([[0.        , 0.41915098, 0.51826859, ..., 0.        , 0.        ,
                 0.        ],
                [0.        , 0.5153114 , 0.        , ..., 0.        , 0.        ,
                 0.        ],
                [0.        , 0.        , 0.        , ..., 0.        , 0.        ,
                 0.        ],
                ...,
                [0.        , 1.        , 0.        , ..., 0.        , 0.        ,
                 0.        ],
                [0.        , 0.        , 0.        , ..., 0.        , 0.        ,
                 0.        ],
                [0.        , 0.55512454, 0.        , ..., 0.        , 0.        ,
                 0.        ]])
- Membuat dataframe untuk melihat TF-IDF matrix dengan kolom berisi genre dan baris berisi title. Oleh karena beberapa movie tidak hanya memiliki 1 genre, tetapi beberapa genre yang relevan dengan movie tersebut, sehingga matrix tidak bernilai bulat 1.

      | title                                                       | western | comedy   | ... | imax | fantasy  | crime  |
      |-------------------------------------------------------------|---------|----------|-----|------|----------|--------|
      | Bloodbath at the House of Death (1984)                      | 0.0     | 0.546038 | ... | 0.0  | 0.000000 | 0.0    |
      | Tale of the Mummy (1998)                                    | 0.0     | 0.000000 | ... | 0.0  | 0.635364 | 0.0    |
      | Irreconcilable Differences (1984)                           | 0.0     | 0.544541 | ... | 0.0  | 0.000000 | 0.0    |
      | Stoned (2005)                                               | 0.0     | 0.000000 | ... | 0.0  | 0.000000 | 0.0    |
      | Merry Widow, The (1934)                                     | 0.0     | 0.389629 | ... | 0.0  | 0.000000 | 0.0    |
      | Fearful Symmetry: The Making of 'To Kill a Mockingbird'...  | 0.0     | 0.000000 | ... | 0.0  | 0.000000 | 0.0    |
      | Octane (2003)                                               | 0.0     | 0.000000 | ... | 0.0  | 0.000000 | 0.0    |
      | Amen. (2002)                                                | 0.0     | 0.000000 | ... | 0.0  | 0.000000 | 0.0    |
      | Best Exotic Marigold Hotel, The (2011)                      | 0.0     | 0.786067 | ... | 0.0  | 0.000000 | 0.0    |
      | Saving Lincoln (2013)                                       | 0.0     | 0.000000 | ... | 0.0  | 0.000000 | 0.0    |
      10 rows × 21 columns

### **Cosine Similarity**
Pada tahap sebelumnya, telah berhasil mengidentifikasi korelasi antara judul movie dengan genrenya. Selanjutnya, perlu menghitung derajat kesamaan (similarity degree) antar movie dengan teknik cosine similarity. Pembatasan data dilakukan agar proses dapat berjalan. Berikut matriks kesamaan setiap movie dalam 5 sampel kolom (axis = 1) dan 10 sampel baris (axis=0).

![image](https://github.com/user-attachments/assets/b1605b2a-b34e-43c5-ad54-a29fd10bcfe4)

## **Mendapatkan Rekomendasi - Content Based Filtering**
Menggunakan argpartition, sejumlah nilai k tertinggi dapat diambil dari similarity data (dalam kasus ini: dataframe cosine_sim_df). Kemudian,  data diambil dari bobot (tingkat kesamaan) tertinggi ke terendah. Data ini dimasukkan ke dalam variabel closest. Berikutnya, title yang dicari perlu dihapus agar tidak muncul dalam daftar rekomendasi.
Penjelasan parameter yang digunakan pada model, antara lain:
- title: berfungsi jadi dasar pencarian untuk rekomendasi.
- similarity_data berisi default cosine_sim_df, ini akan digunakan untuk mencari film mana yang paling mirip dengan title berdasarkan nilai cosine similarity.
- items: None, berarti judul hanya judul film yang akan ditampilkan, tanpa informasi tambahan dari fitur lain.
- k = 5 menunjukkan 5 rekomendasi film dengan kemiripan teratas.

Contoh hasil rekomendasi content based filtering:
```
movie_recommendations('Toy Story (1995)', items=data[['title', 'genres']], k=5)
```
    | title                                 | genres                                        |
    |---------------------------------------|-----------------------------------------------|
    | Toy Story 2 (1999)                    | Adventure|Animation|Children|Comedy|Fantasy   |
    | Antz (1998)                           | Adventure|Animation|Children|Comedy|Fantasy   |
    | The Magic Crystal (2011)             | Adventure|Animation|Children|Comedy|Fantasy   |
    | Toy Story Toons: Small Fry (2011)     | Adventure|Animation|Children|Comedy|Fantasy   |
    | Monsters, Inc. (2001)                | Adventure|Animation|Children|Comedy|Fantasy   |
    
Sistem memberikan 5 rekomendasi film yang memiliki kemiripan dengan film referensi tersebut berdasarkan genre menggunakan pendekatan content-based filtering. Contoh di atas, sistem akan merekomendasikan kepada pengguna  5 film dengan kemiripan genre dari preferensinya, yaitu Toy Story (1995).

**Kelebihan content based filtering berdasarkan cara kerja:**
- personalisasi tinggi karena sistem memberikan rekomendasi berdasarkan preferensi unik setiap pengguna.
- Tidak perlu menunggu data dari pengguna lain yang berinteraksi.

**Kelemahan content based filteringberdasarkan cara kerja:**
- Sistem cenderung merekomendasikan item yang sangat mirip, sehingga kurang bervariasi.
- Jika pengguna belum banyak berinteraksi, sistem sulit membangun profil preferensi.
- Tidak melihat apa yang populer atau disukai pengguna lain

## **Data Preparation-Collaborative Filtering**

### **Menghapus Kolom timestamp**
Kolom timestamp dihapus karena tidak akan digunakan dalam membangun model sistem rekomendasi.

### **Penggabungan Dataset**
Untuk membangun model collaborative filtering, perlu penggabungan dataset genre_df dan rating_df berdasarkan kolom movieId. Berikut hasil penggabungan 2 dataset yang diberi nama movie_df.

          | userId | movieId | rating | Title                                         | Genres                                       |
          |--------|---------|--------|-----------------------------------------------|----------------------------------------------|
          | 1      | 2       | 3.5    | Jumanji (1995)                                | Adventure\|Children\|Fantasy                 |
          | 1      | 29      | 3.5    | City of Lost Children, The (Cité des...)      | Adventure\|Drama\|Fantasy\|Mystery\|Sci-Fi   |
          | 1      | 32      | 3.5    | Twelve Monkeys (a.k.a. 12 Monkeys) (1995)     | Mystery\|Sci-Fi\|Thriller                    |
          | 1      | 47      | 3.5    | Seven (a.k.a. Se7en) (1995)                   | Mystery\|Thriller                            |
          | ...    | ...     | ...    | ...                                           | ...                                          |
          | 7120   | 253     | 4.0    | Interview with the Vampire...                 | Drama\|Horror                                |
          | 7120   | 260     | 5.0    | Star Wars: Episode IV - A New Hope (1977)     | Action\|Adventure\|Sci-Fi                    |
          | 7120   | 261     | 4.0    | Little Women (1994)                           | Drama                                        |
          | 7120   | 266     | 3.5    | Legends of the Fall (1994)                    | Drama\|Romance\|War\|Western                 |

### **Encode fitur userId dan movieId**
Sebelum melakukan encoding dataset rating_df assign ke rating

Encoding merupakan proses menyandikan fitur user dan placeID ke dalam indeks integer. Setelah itu, fitur userId dan movieId dipetakan ke dataframe yang berkaitan. Cek beberapa hal dalam data, seperti jumlah user, jumlah movie, dan mengubah nilai rating menjadi float64.
- Number of User: 7120
- Number of Movie: 14026
- Min Rating: 0.5 
- Max Rating: 5.0

### **Membagi Data untuk Training dan Validasi**
- Dataset diacak dengan parameter frac=1 yang berarti 100% dari baris data akan diambil secara acak. random_state=42 agar hasil pengacakan konsisten (angka 42 tidak terlalu berarti)
- Data train dan validasi dibagi dengan komposisi 80:20. Sebelum itu, perlu memetakan (mapping) data user dan movie menjadi satu value terlebih dahulu. Lalu, membuat rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training.

### **Proses Training**
Pada tahap training, model menghitung skor kecocokan antara pengguna dan movie dengan teknik embedding. Pertama, proses embedding terhadap data user dan movie. Selanjutnya, operasi perkalian dot product antara embedding user dan movie. Selain itu, dapat juga menambahkan bias untuk setiap user dan movie. Skor kecocokan ditetapkan dalam skala [0,1] dengan fungsi aktivasi sigmoid.

Selanjutnya, proses compile terhadap model. Model menggunakan Binary Crossentropy untuk menghitung loss function, Adam (Adaptive Moment Estimation) sebagai optimizer, dan root mean squared error (RMSE) sebagai metrics evaluation. 
- num_users merupakan jumlah users. Ini digunakan untuk membangun embedding layer user.
- num_movie merupakan jumlah movie. Ini digunakan untuk membangun embedding layer movie.
- 50 berarti setiap user dan movie akan diwakili oleh vektor berdimensi 50 yang dilatih.
- learning_rate=0.0001: Laju pembelajaran yang kecil, sehingga model akan belajar secara perlahan agar lebih stabil.
- metrics = [tf.keras.metrics.RootMeanSquaredError()].
RMSE digunakan untuk mengukur rata-rata kesalahan prediksi.

Setelah itu, dilakukan proses training dengan parameter berikut.
- learning_rate=0.0001: Laju pembelajaran yang kecil, sehingga model akan belajar secara perlahan agar lebih stabil.
- loss='mean_squared_error' untuk menghitung error.
- metrics=[tf.keras.metrics.RootMeanSquaredError()]: metrik evaluasi, yaitu RMSE yang digunakan untuk mengevaluasi prediksi rating.
- x_train: Input data training.
- y_train: Label target
- batch_size=256 artinya 256 sampeliterasi yang diproses sebelum perubahan weight.
- epoch = 30 artinya perulangan penuh terhadap seluruh dataset pelatihan sebanyak 30 kali.

### **Visualisasi Metrik**

![image](https://github.com/user-attachments/assets/38335f47-d73a-48ed-99fb-6f99221094d4)

Berdasarkan visualisasi metrik, terlihat bahwa:
- Baik pada data train maupun test, RMSE menurun secara stabil seiring bertambahnya epoch.
- Garis test dan train berdekatan hingga akhir epoch, sehingga tidak mengindikasikan overfitting.

Dapat disimpulkan bahwa model menunjukkan performa yang baik, stabil, dan tidak overfitting.

## **Mendapatkan Rekomendasi Movie**
Untuk mendapatkan rekomendasi movie, sampel user awalnya acak dan definisikan variabel movie_not_visited yang merupakan daftar movie yang belum pernah dikunjungi oleh pengguna.

Sebelumnya, pengguna telah memberi rating pada beberapa movie yang telah ditonton. Rating ini digunakan untuk membuat rekomendasi movie lain yang mungkin cocok dan belum pernah ditonton untuk pengguna.

Penjelasan singkat terkait parameter dan fungsi yang digunakan untuk mengambil rekomendasi:
- user_movie_array: array berisi pasangan [user_id, movie_id] yang akan dinilai oleh model.
- model.predict(...): menghasilkan prediksi rating untuk setiap pasangan tersebut.
- .flatten(): mengubah hasil prediksi dari bentuk 2D
- top_ratings_indices = ratings.argsort()[-10:][::-1] artiny mengambil 10 indeks tertinggi dari ratings (rekomendasi teratas)
- argsort(): Mengurutkan indeks dari rating terkecil ke terbesar.
- [::-1]: Membalik hasil agar urutan dari tertinggi ke terendah.
- movie_not_visited: daftar film yang belum pernah ditonton oleh user.
- movie_encoded_to_movie: dictionary untuk mengonversi movie_encoded_id ke movieId asli.

Contoh hasil rekomendasi collaborative filtering:

      Showing recommendations for users: 2177
      ===========================
      movie with high ratings from user
      --------------------------------
      Bullets Over Broadway (1994) : Comedy
      Casablanca (1942) : Drama|Romance
      Taxi Driver (1976) : Crime|Drama|Thriller
      Maltese Falcon, The (1941) : Film-Noir|Mystery
      Three Colors: Red (Trois couleurs: Rouge) (1994) : Drama
      --------------------------------
      Top 10 movie recommendation
      --------------------------------
      Usual Suspects, The (1995) : Crime|Mystery|Thriller
      Shawshank Redemption, The (1994) : Crime|Drama
      One Flew Over the Cuckoo's Nest (1975) : Drama
      Fight Club (1999) : Action|Crime|Drama|Thriller
      Godfather, The (1972) : Crime|Drama
      Godfather: Part II, The (1974) : Crime|Drama
      Schindler's List (1993) : Drama|War
      City of God (Cidade de Deus) (2002) : Action|Adventure|Crime|Drama|Thriller
      To Kill a Mockingbird (1962) : Drama
      12 Angry Men (1957) : Drama

Penjelasan hasil rekomendasi: 
Showing recommendations for users: 2177
- User ini adalah pengguna aktif dalam sistem rekomendasi.
- Rekomendasi dilakukan berdasarkan pola historis rating dan prediksi model terhadap film yang belum ditonton.
- Genre dominan yang yang direkomendasikan untuk pengguna 2177: Drama, Crime, Mystery, dan Thriller.

**Kelebihan Collaborative filtering berdasarkan cara kerja:**
- Tidak bergantung atribut item, seperti genre.
- Lebih variatif karena memberikan rekomendasi berdasarkan pola perilaku kolektif pengguna, bukan hanya berdasarkan kesamaan konten.
- Kualitas rekomendasi meningkat seiring bertambahnya data interaksi pengguna. 

Kelemahan Collaborative filtering berdasarkan cara kerja:
- Untuk item barusulit direkomendasikan karena belum ada yang memberi rating atau interaksi.
- Bisa dimanipulasi melalui fake ratings atau spam users, sehingga sering tidak akurat.

## **Evaluasi**
Berikut evaluasi dari pembuatan model sistem rekomendasi film jika dikaitkan dengan problem statements.

*Bagaimana sistem rekomendasi dapat membantu pengguna dalam menemukan film yang sesuai dengan preferensi mereka secara efisien?*

- Sistem rekomendasi film telah dibangun menggunakan pendekatan content-based dan collaborative filtering. Model ini akan membantu pengguna menemukan film berdasarkan preferensi secara cepat dan akurat.

*Sistem rekomendasi apa yang paling efektif dalam menghasilkan rekomendasi film?*
- Untuk pengguna dengan minat yang spesifik dan stabil, content based filtering cocok diimplementasikan karena mampu memberikan rekomendasi secara personal tanpa dipengaruhi pengguna lain.

- Untuk pengguna yang menyukai film berdasarkan tren, collaborative filtering cocok diimplementasikan karena model ini dipengaruhi dengan interaksi pengguna lain, misalnya film dengan rating tertinggi akan direkomendasikan.

*Bagaimana pengaruh penerapan sistem rekomendasi terhadap peningkatan durasi penggunaan platform penyedia film oleh pengguna?*

- Implementasi model sistem rekomendasi ini akan membantu pengguna menghemat waktu dan biaya dalam mencari film yang sesuai minat. Menurut sisi bisnis, platform akan lebih sering digunakan apabila pengguna merasa cocok dengan rekomendasi yang diberikan sesuai dengan preferensinya. Hal ini tentu saja meningkatkan durasi dan satisfaction pengguna dalam menggunakan platform penyedia film.

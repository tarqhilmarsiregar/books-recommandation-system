# Laporan Proyek Machine Learning - Tarq Hilmar Siregar

## Project Overview

Pada era digital, jumlah informasi yang tersedia bagi pengguna meningkat secara signifikan, termasuk dalam hal pemilihan buku yang sesuai dengan preferensi individu. Hal ini dapat menimbulkan tantangan dalam menemukan rekomendasi yang tepat dan relevan. Sistem rekomendasi dirancang untuk menyaring informasi yang melimpah tersebut guna memberikan pilihan yang lebih terarah kepada pengguna.

- Mengapa masalah tersebut harus diselesaikan? <br>
Peningkatan jumlah buku digital serta berkembangnya platform pembaca daring telah menyebabkan ketersediaan informasi menjadi sangat melimpah. Kondisi ini dapat mengakibatkan kesulitan bagi pengguna dalam menemukan buku yang sesuai dengan minat dan preferensi mereka, sehingga berpotensi menurunkan tingkat keterlibatan dan kepuasan pengguna. Oleh karena itu, diperlukan sistem rekomendasi yang efektif untuk meningkatkan pengalaman pengguna melalui penyajian pilihan buku yang lebih relevan dan personal.

- Bagaimana menyelesaikan permasalahan tersebut? <br>
Sistem rekomendasi buku yang efektif dapat dibangun dengan menggabungkan pendekatan Content-Based Filtering (CBF) dan Collaborative Filtering (CF). Pendekatan CBF menganalisis fitur-fitur dari buku, seperti genre dan penulis, serta preferensi pengguna sebelumnya untuk merekomendasikan buku serupa. Di sisi lain, pendekatan CF memanfaatkan interaksi pengguna, seperti pemberian rating, guna menemukan kesamaan antara pengguna atau buku. Pendekatan hybrid yang mengintegrasikan CBF dan CF telah terbukti efektif dalam meningkatkan akurasi rekomendasi serta mengatasi kelemahan dari masing-masing metode. Sebagai ilustrasi, penelitian oleh Remadnia et al. (2025) mengusulkan mekanisme rekomendasi e-book berbasis hybrid yang mengombinasikan filtering kolaboratif dan pendekatan berbasis konten guna mengatasi tantangan dalam sistem pembelajaran daring. Selain itu, pendekatan hybrid yang menggabungkan analisis sentimen dengan filtering kolaboratif juga menunjukkan peningkatan akurasi dalam sistem rekomendasi buku. Penelitian oleh Kumar dan Chawla (2023) mengembangkan sistem rekomendasi buku berbasis analisis sentimen hybrid dengan mengombinasikan teknik analisis sentimen dan filtering kolaboratif untuk meningkatkan kualitas rekomendasi (Taylor & Francis). Melalui penerapan pendekatan-pendekatan tersebut, sistem rekomendasi buku mampu memberikan saran yang lebih personal dan relevan kepada pengguna, sehingga dapat meningkatkan kepuasan dalam menemukan buku yang sesuai dengan minat dan preferensi masing-masing.

- Referensi <br>
Remadnia, O., Maazouzi, F., & Chefrour, D. (2025). Hybrid Book Recommendation System Using Collaborative Filtering and Embedding Based Deep Learning. Informatica, 49(8). <br>
Kumar, A., & Chawla, S. (2024). Hybrid sentiment analysis based book recommendation system. In Advances in Networks, Intelligence and Computing (pp. 146-155). CRC Press.


## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah:
- Berdasarkan data mengenai pengguna, bagaimana membuat sistem rekomendasi yang dipersonalisasi dengan teknik content-based filtering?
- Berdasarkan data rating yang dimiliki, bagaimana membuat sistem yang dapat merekomendasikan buku lain yang mungkin disukai dan belum pernah dibaca oleh pengguna?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Menghasilkan sejumlah rekomendasi buku yang dipersonalisasi untuk pengguna dengan teknik content-based filtering
- Menghasilkan sejumlah rekomendasi buku yang sesuai dengan preferensi pengguna dan belum pernah dibaca sebelumnya dengan teknik collaborative filtering.

- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Menggunakan pendekatan Content-Based Filtering untuk menghasilkan rekomendasi buku berdasarkan karakteristik buku yang pernah dibaca oleh pengguna, seperti author dan publisher. Algoritma yang digunakan yaitu TF-IDF (Term Frequency - Inverse Document Frequency) untuk menghitung bobot kata dari deskripsi buku atau menemukan representasi fitur penting dari buku. Kemudian, Cosine Similarity digunakan untuk mengukur kesamaan antara vektor buku untuk menemukan buku yang mirip
    - Menggunakan Collaborative Filtering untuk menghasilkan rekomendasi buku yang belum pernah dibaca pengguna berdasarkan preferensi pengguna lain dengan minat yang mirip. Algoritma yang digunakan yaitu User-User Collaborative Filtering untuk mengukur kesamaan antar pengguna berdasarkan rating buku

## Data Understanding
Proyek ini menggunakan dataset dengan topik rekomendasi buku yang tersedia secara publik di platform [Kaggle](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). Dataset ini berisi data buku buku (Books.csv), rating (Ratings.csv) dan pengguna (Users).

Detail Dataset:
1. File Books.csv berisi:
    - Jumlah Data (Baris): 271360 entri
    - Jumlah Fitur (Kolom): 8 fitur input
    - Format File: CSV (.csv)

2. File Ratings.csv berisi:
    - Jumlah Data (Baris): 1149780 entri
    - Jumlah Fitur (Kolom): 3 fitur input
    - Format File: CSV (.csv)

3. File Users.csv berisi:
    - Jumlah Data (Baris): 278858 entri
    - Jumlah Fitur (Kolom): 3 fitur input
    - Format File: CSV (.csv)

Kondisi Data: <br>
- Pada file **Books.csv** terdapat 8 fitur dengan tipe data object. Kemudian, terdapat beberapa kolom missing values seperti Book-Author, Publisher, dan Image-URL-L <br>
- Pada file **Ratings.csv** terdapat 3 fitur dengan User-ID (tipe data integer), ISBN (tipe data object), dan Book-Rating (tipe data integer). Kemudian, pada file ini tidak ditemukan adanya missing values <br>
- Pada file **Users.csv** terdapat 3 fitur dengan User-ID (tipe data integer), Location (tipe data object), dan Age (tipe data float). Kemudian, terdapat kolom missing values yakni kolom Age <br>

Variabel-variabel pada Books dataset adalah sebagai berikut: <br>
1. Books.csv
    - ISBN: ISBN buku
    - Book-Title: Judul buku
    - Book-Author: Penulis buku
    - Year-Of-Publication: Tahun publikasi buku
    - Publisher: Penerbit buku
    - Image-URL-S: Gambar ukuran kecil dari buku
    - Image-URL-M: Gambar ukuran sedang dari buku
    - Image-URL-L: Gambar ukuran besar dari buku

2. Ratings.csv
    - User-ID: ID unik pengguna
    - ISBN: ISBN buku
    - Book-Rating: Rating buku

3. Users.csv
    - User-ID: ID unik pengguna
    - Location: Lokasi pengguna
    - Age: Umur pengguna

1. Deskripsi variabel <br>
    Menampilkan jumlah data dan tipe data yang digunakan masing masing kolom
    ```python
    df_books.info()
    df_ratings.info()
    df_users.info()
    ```

2. Univariate Analysis <br>
    Menampilkan distribusi data masing masing kolom seperti ISBN, Book-Author, Publisher, User-ID, dan Book-Rating 
    ```python
    print('Banyak buku: ', len(df_books.ISBN.unique()))
    df_books['Book-Author'].value_counts()
    df_books['Publisher'].value_counts()
    df_ratings['User-ID'].value_counts()
    df_ratings['ISBN'].value_counts()
    df_ratings['Book-Rating'].value_counts()
    ```

## Data Preparation
Sebelum membangun sistem rekomendasi Content Based Filtering, dilakukan beberapa tahap persiapan data untuk memastikan bahwa data dalam kondisi optimal untuk digunakan lebih lanjut. Hal hal tersebut diantaranya:
1. Menggabungkan seluruh ISBN pada buku
2. Mengurutkan dan menghapus data yang sama pada books_all
3. Menggabungkan seluruh User ID
4. Mengurutkan dan menghapus data yang sama pada users_all
5. Menggabungkan dataframe buku, rating dan user
6. Mengatasi **missing values**
7. Mengurutkan buku berdasarkan ISBN kemudian menyimpan nya ke dalam variabel preparation
8. Menghapus data duplikat pada variabel preparation
9. Mengambil 8000 data secara acak
10. Mengonversi data ISBN, Book-Title, dan Book-Author ke dalam bentuk list
11. Membuat dictionary untuk variabel books_id, books_title, dan books_author yang telah dibuat sebelumnya
12. Ekstraksi Fitur dengan TF-IDF Vectorizer

Kemudian, sebelum membangun Collaborative Filtering, dilakukan beberapa tahap persiapan data untuk memastikan bahwa data dalam kondisi optimal untuk digunakan lebih lanjut. Hal hal tersebut diantaranya:
1. Menyandikan (encode) fitur user dan ISBN ke dalam indeks integer 
2. Memetakan User-ID dan ISBN ke dataframe yang berkaitan
3. Mengecek beberapa hal dalam data seperti jumlah user, jumlah buku, kemudian mengubah nilai rating menjadi float
4. Pembagian Data

Content Based Filtering:
1. Penggabungan seluruh ISBN pada buku ini dilakukan untuk menggabungkan seluruh ISBN dari dua data frame (df_books dan df_ratings) menggunakan NumPy sehingga memastikan bahwa semua ISBN dari dua sumber data berbeda terkumpul dalam satu array tanpa ada duplikasi per data frame
2. Mengurutkan dan menghapus data yang sama pada books_all ini dilakukan untuk mengurutkan dan menghapus duplikasi dari kumpulan ISBN pada variabel books_all sehingga hal ini memastikan bahwa ISBN yang tersimpan dalam books_all tidak ada yang berulang dan sudah diurutkan secara alfabetis atau numerik
3. Menggabungkan seluruh User ID dilakukan untuk menggabungkan seluruh User-ID dari dua data frame (df_ratings dan df_users) menggunakan NumPy sehingga memastikan bahwa semua User-ID dari dua sumber data terkumpul dalam satu array, tanpa ada duplikasi per data frame
4. Mengurutkan dan menghapus data yang sama pada users_all bertujuan untuk menghapus duplikasi dan mengurutkan seluruh User-ID yang sudah digabungkan sebelumnya dalam variabel users_all sehingga variabel users_all hanya berisi User-ID yang unik dan sudah terurut secara alfabetis atau numerik
5. Menggabungkan dataframe buku, rating dan user bertujuan untuk menggabungkan data buku dan rating berdasarkan ISBN. Kemudian, menggabungkan hasil tersebut dengan data pengguna berdasarkan User-ID sehingga Hasil akhir nya (books) akan berisi data buku, rating, dan pengguna yang terhubung satu sama lain
6. Penghapusan **missing values** dilakukan agar proses analisis lebih akurat dan tidak bias akibat data yang hilang
7. Pengurutan data buku berdasarkan ISBN dilakukan agar posisi data tersebut tersusun secara berurutan dan menyimpan nya ke variabel baru preparation
8. Penghapusan data duplikat dilakukan untuk mengurangi redudansi data, memperbaiki kualitas data sehingga bisa lebih mudah diolah dan diinterpretasi, serta mempercepat proses pemrosesan data dengan dataset yang lebih ringan
9. Pengambilan data acak sebanyak 8000 agar proses perhitungan cosine similarity pada google colab berjalan dengan lancar tanpa terjadinya ram crash dengan jumlah data yang besar
10. Mengonversi data dan membuatnya ke dalam dictionary untuk mengambil kolom kolom yang hanya akan digunakan dalam proses menemukan representasi fitur penting dari setiap book author di tahapan modeling
11. Ekstraksi Fitur dengan TF-IDF Vectorizer bertujuan untuk mengekstraksi kata unik dari data pada kolom book_author, menghitung IDF dari setiap kata, mendapatkan daftar kata sebagai fitur yang akan digunakan dalam model dan memberikan representasi teks dalam bentuk vektor TF-IDF yang siap digunakan untuk analisis teks atau pembuatan model machine learning

Collaborative Filtering:
1. Tahap encoding pada data preparation ini dilakukan untuk mempermudah proses komputasi dan analisis data seperti menghapus duplikasi data, mengelompokkan data, konversi ke format numerik 
2. Mapping User-ID dan ISBN dilakukan untuk mengonversi data ke dalam bentuk angka
3. Tahapan pengecekan jumlah user, jumlah buku dan mengubah tipe data rating menjadi float untuk memastikan keselarasan data, memahami distribusi rating, mengantisipasi error jika terjadi ketidaksesuaian pada jumlah user atau buku
4. Pembagian Data, tahap ini membagi data menjadi 80% data latih (training) dan 20% data validasi untuk keperluan pelatihan model sehingga dengan pembagian ini, model bisa belajar dari data training dan diuji pada data validasi untuk melihat performanya

## Modeling
Untuk menyelesaikan permasalahan sistem rekomendasi buku ini, dilakukan beberapa tahapan pemodelan secara sistematis. Dua algoritma atau pendekatan yang digunakan yaitu Content Based Filtering dan Collaborative Filtering. Berikut penjelasan tiap algoritma atau pendekatan yang digunakan:

1. Content-Based Filtering (CBF) adalah teknik yang digunakan dalam sistem rekomendasi untuk memberikan saran berdasarkan kesamaan konten dari item yang sudah disukai oleh pengguna. Dalam konteks rekomendasi buku, pendekatan ini bertujuan untuk menyarankan buku-buku baru yang memiliki karakteristik serupa dengan buku yang sudah dibaca oleh pengguna. Untuk mencapai tujuan ini, menggunakan teknik TF-IDF (Term Frequency-Inverse Document Frequency) dan Cosine Similarity. Pada dasarnya, CBF bekerja dengan menganalisis deskripsi, judul, atau atribut lain dari buku untuk menemukan kata-kata yang paling mencerminkan isi dari buku tersebut. Karena data ini berupa teks, maka dibutuhkan cara untuk mengonversinya menjadi bentuk numerik agar bisa dihitung oleh komputer. Di sinilah peran TF-IDF menjadi sangat penting. TF-IDF adalah teknik pemrosesan teks yang mengukur seberapa penting sebuah kata dalam suatu dokumen dibandingkan dengan seluruh koleksi dokumen. Teknik ini berguna untuk menangkap kata-kata yang sering muncul di suatu buku tetapi jarang muncul di buku lainnya, sehingga kata tersebut dianggap lebih representatif. Prosesnya dimulai dengan mengambil data dari kolom teks, dalam hal ini penulis buku. Data ini kemudian diproses oleh TF-IDF Vectorizer, yang akan mengonversi setiap kata menjadi vektor angka berdasarkan frekuensi dan relevansi kata tersebut. Hasil akhirnya adalah sebuah matriks vektor TF-IDF yang merepresentasikan setiap buku dalam bentuk numerik. Setelah semua buku dikonversi menjadi vektor, kita perlu menghitung tingkat kemiripan antar buku untuk memberikan rekomendasi. Dalam hal ini, kita menggunakan Cosine Similarity, sebuah teknik yang mengukur kemiripan dua vektor dengan melihat sudut di antara mereka. Cosine Similarity dinilai berdasarkan sudut antara dua vektor dalam ruang multidimensi. Jika sudut antara dua vektor sangat kecil (mendekati nol derajat), itu berarti kedua vektor tersebut hampir sejajar dan dianggap sangat mirip. Sebaliknya, jika sudutnya besar (mendekati 90 atau 180 derajat), maka kedua vektor tersebut dianggap tidak mirip. Cosine Similarity dihitung dengan cara membagi hasil perkalian dot product antara dua vektor dengan hasil kali norma dari kedua vektor tersebut. Nilai yang dihasilkan berkisar antara -1 hingga 1. Semakin mendekati nilai 1, artinya kedua buku memiliki konten yang sangat mirip, sedangkan nilai mendekati 0 menunjukkan tidak ada kemiripan. Dengan pendekatan ini, CBF tidak memerlukan data dari pengguna lain, melainkan hanya bergantung pada konten dari buku itu sendiri. Hal ini sangat berguna dalam situasi cold start, ketika pengguna baru belum memberikan banyak rating atau belum memiliki banyak riwayat interaksi. Namun, teknik ini juga memiliki kelemahan, yaitu kurang memperhatikan variasi preferensi pengguna. Jika seorang pengguna menyukai buku dari penulis buku yang berbeda-beda, rekomendasi CBF bisa menjadi kurang akurat karena hanya fokus pada kesamaan konten dari buku-buku yang pernah disukai sebelumnya. Secara keseluruhan, metode Content-Based Filtering dengan TF-IDF dan Cosine Similarity sangat berguna untuk menemukan buku dengan konten yang sejenis. Pendekatan ini mengutamakan teks sebagai sumber informasi utama dan berfokus pada pemetaan konten untuk menghasilkan rekomendasi yang lebih personal dan kontekstual.
    - Kelebihan:
        - Personalisasi berdasarkan minat didasarkan pada preferensi pengguna
        - Interpretasi mudah
    - Kekurangan:
        - Keterbatasan data, membutuhkan deskripsi dan fitur buku yang lengkap dan akurat
        - Terlalu fokus hanya pada buku yang mirip dengan yang sudah pernah dibaca
    - Top N Recommandation:
        ```python
        # Mendapatkan rekomendasi buku yang mirip dengan The age of innocence
        books_recommendations('The age of innocence')
        ```

        ```python
        +-------+--------------------------------------+---------------+
        | index |              book_title              |  book_author  |
        +=======+======================================+===============+
        | 0     | Souls Belated (Everyman S.)          | Edith Wharton |
        +-------+--------------------------------------+---------------+
        | 1     | The House of Mirth                   | Edith Wharton |
        +-------+--------------------------------------+---------------+
        | 2     | Country Diary of an Edwardian Lady   | Edith Holden  |
        +-------+--------------------------------------+---------------+
        | 3     | Vom GlÃ?Â¼ck mit der Natur zu leben. | Edith Holden  |
        +-------+--------------------------------------+---------------+
        | 4     | The Five Children and It             | Edith Nesbit  |
        +-------+--------------------------------------+---------------+
        ```

2. Collaborative Filtering (CF) adalah metode yang digunakan dalam sistem rekomendasi untuk memberikan saran berdasarkan pola interaksi pengguna lain yang memiliki preferensi serupa. Berbeda dengan pendekatan berbasis konten yang fokus pada atribut item itu sendiri, CF memanfaatkan data dari pengguna lain dengan asumsi bahwa jika dua pengguna menunjukkan pola perilaku yang mirip di masa lalu, mereka cenderung memiliki selera yang sama di masa depan. Dalam konteks rekomendasi buku, CF akan menganalisis riwayat rating dari berbagai pengguna dan mencari pola kesamaan di antara mereka. Jika ada pengguna lain yang memiliki preferensi serupa dengan pengguna saat ini, buku-buku yang disukai oleh pengguna lain tersebut akan direkomendasikan. Namun, CF menghadapi tantangan ketika data pengguna sangat besar dan bervariasi, sehingga teknik tradisional seperti matriks faktorisasi atau algoritma berbasis tetangga (neighbor-based) sering kali tidak cukup efisien. Oleh karena itu, pendekatan berbasis jaringan saraf, seperti Neural Collaborative Filtering (NCF), menjadi solusi yang lebih modern dan efektif. NCF menggunakan teknik deep learning untuk menangkap pola interaksi yang lebih kompleks dan non-linear antara pengguna dan item. Dalam model ini, teknik NCF diimplementasikan melalui jaringan saraf buatan menggunakan framework TensorFlow dan Keras. Model tersebut dinamakan RecommenderNet. Pada dasarnya, RecommenderNet adalah model yang dibuat untuk memetakan interaksi antara pengguna dan buku dalam ruang vektor laten. Vektor laten ini memungkinkan model untuk memahami hubungan non-linear antara pengguna dan buku, sehingga hasil rekomendasi menjadi lebih akurat dan personal. Arsitektur model RecommenderNet dibangun dengan menggunakan lapisan embedding. Lapisan embedding adalah komponen penting dalam model ini karena memungkinkan konversi ID pengguna dan ID buku menjadi representasi vektor berdimensi laten. Vektor ini pada dasarnya adalah bentuk numerik dari fitur pengguna dan buku yang telah dipelajari oleh model selama proses training. Dengan kata lain, embedding ini bertujuan untuk menangkap karakteristik dari masing-masing pengguna dan buku dalam dimensi laten yang lebih ringkas dan efisien. Selama proses inisialisasi model, lapisan embedding pengguna dan buku dibuat dengan menggunakan metode inisialisasi bobot He Normal, yang cocok untuk jaringan saraf dengan aktivasi non-linear. Selain itu, regularisasi L2 diterapkan untuk mencegah overfitting dengan menambahkan penalti terhadap bobot yang terlalu besar. Pada saat proses perhitungan, model akan mengambil vektor embedding dari pengguna dan buku yang diberikan sebagai input. Selain itu, terdapat pula bias pengguna dan bias buku yang diambil melalui lapisan embedding bias. Bias ini membantu model dalam menangkap perbedaan kecenderungan dari masing-masing pengguna dan buku. Untuk mengukur seberapa besar kesesuaian antara pengguna dan buku, model menghitung produk skalar atau dot product antara vektor embedding pengguna dan vektor embedding buku. Dot product ini akan menghasilkan skor yang menunjukkan tingkat kecocokan antara keduanya. Skor ini kemudian dijumlahkan dengan nilai bias dari pengguna dan buku untuk mendapatkan hasil akhir yang lebih akurat. Agar output model berada dalam rentang yang diharapkan, yaitu antara 0 dan 1, digunakan fungsi aktivasi sigmoid. Fungsi sigmoid ini memastikan bahwa hasil prediksi akan sesuai dengan format rating yang digunakan. Dalam tahap pelatihan model, digunakan algoritma optimisasi Adam yang mampu menangani gradien dengan lebih stabil dan cepat. Selain itu, loss function yang dipilih adalah binary crossentropy, yang cocok untuk permasalahan dengan output probabilistik. Model dilatih selama 25 epoch. Setiap iterasi pelatihan dilakukan dalam 12 batch. Setelah proses pelatihan selesai, model dapat digunakan untuk melakukan prediksi terhadap rating buku yang mungkin disukai oleh pengguna tertentu. Proses ini dilakukan dengan memberikan input berupa pasangan pengguna dan buku ke dalam model, dan output berupa prediksi rating akan diberikan. Dengan menggunakan pendekatan ini, model dapat secara dinamis merekomendasikan buku-buku baru kepada pengguna berdasarkan pola interaksi yang telah dipelajari sebelumnya. Kekuatan utama dari model RecommenderNet ini terletak pada fleksibilitasnya dalam menangkap hubungan non-linear antara pengguna dan buku, sehingga mampu memberikan rekomendasi yang lebih personal dan akurat. Namun, ada juga kelemahan yang perlu diperhatikan, yaitu data sparsity dan masalah cold start. Jika pengguna atau buku baru tidak memiliki cukup data interaksi, model akan kesulitan memberikan rekomendasi yang tepat. Meskipun begitu, dalam skenario di mana data pengguna dan interaksi yang cukup tersedia, model ini mampu memberikan rekomendasi buku yang relevan dan sesuai dengan preferensi pengguna.
    - Kelebihan:
        - Fleksibilitas, dapat menemukan buku baru yang tidak pernah atau belum dibaca pengguna
        - Tidak perlu atribut buku, hal ini didasarkan pada interaksi pengguna
    - Kekurangan:
        - Cold Start, kesulitan memberi rekomendasi untuk pengguna baru atau buku baru yang belum memiliki cukup interaksi
        - Scalability, proses komputasi menjadi berat jika jumlah pengguna dan item sangat besar
    - Top N Recommandation:
        ```python
        ....
        print('Showing recommendations for users: {}'.format(user_id))
        print('===' * 9)
        print('Books with high ratings from user')
        print('----' * 8)

        top_books_user = (
            books_visited_by_user.sort_values(
                by = 'rating',
                ascending=False
            )
            .head(5)
            .ISBN.values
        )
        ....
        ```

        ```python
        #Output
        Showing recommendations for users: 230522
        ===========================
        Books with high ratings from user
        --------------------------------
        Cheaper and Better: Homemade Alternatives to Storebought Goods : Nancy Birnes
        --------------------------------
        Top 10 books recommendation
        --------------------------------
        The Sword of Maiden's Tears (Book One of the Twelve Treasures) : Rosemary Edghill
        Treasure Island (Puffin Classics) : Robert Louis Stevenson
        Preparation for the Sat: Scholastic Assessment Test/New Test : Edward J. Deptula
        Royal Survivor: The Life of Charles II : Stephen Coote
        10 Relatos Fantasticos : Varios
        Rebelion en la Granja : George Orwell
        Aristotle's Poetics : S. H. Butcher
        Fox on the Box: Start to Read : Barbara Gregorich
        The New French Baker: Perfect Pastries and Beautiful Breads from Your Kitchen : Sheila Linderman
        Harry Potter and the Goblet of Fire : J. K. Rowling        
        ```

## Evaluation
Berdasarkan hal tersebut di atas, pada projek ini, terkhusus pada Collaborative Filtering akan memilih dan menggunakan metrik Root Mean Squared Error (RMSE). Berikut ini penjelasan terkait hal tersebut:

- Model rekomendasi buku dievaluasi menggunakan metrik RMSE pada data latih dan data uji selama 25 epoch. Hasil menunjukkan bahwa RMSE pada data latih menurun secara signifikan, sementara RMSE pada data uji juga menurun namun lebih lambat, terutama setelah epoch ke-15. Hal ini mengindikasikan adanya overfitting, di mana model semakin baik pada data latih namun kurang mampu menggeneralisasi pada data uji. Meskipun demikian, model masih dapat melakukan rekomendasi dengan baik.
![visualisasi hasil metrik train vs test](https://github.com/user-attachments/assets/6032f179-3f58-406f-a85a-e4ac41ec9f08)

- RMSE (Root Mean Squared Error) <br>
  ![Formula RMSE](https://github.com/user-attachments/assets/650138be-60d9-4298-b32c-480388e13b01)
  Formula ini digunakan untuk mengukur seberapa jauh prediksi dari nilai sebenarnya. Semakin kecil RMSE, semakin akurat modelnya. Cara kerja dari formula ini dimulai dengan menghitung selisih antara rating prediksi dengan rating aktual, kemudian hasil selisih dikuadratkan untuk menghilangkan negatif. Setelah itu, jumlahkan semua selisih kuadrat dan membagi nya dengan jumlah data. Terakhir, akar kuadrat kan sehingga mengembalikan hasil ke skala asli rating tersebut

# RKMN_Final_Project_Group_4
This repository created for accomplishing Data Science bootcamp's final project on Rakamin Batch 23.

SUMMARY FINAL PROJECT

STAGE 1: Exploratory Data Analysis (EDA)
INSIGHT-INSIGHT EDA DAN REKOMENDASI UNTUK DATA PRE-PROCESSING 
Insight Descriptive Statistics Pengamatan: 
Tampak beberapa kolom, yakni kolom childern, country, agent, dan company masih memiliki null/missing values (Non-Null Count < jumlah baris) 
Pada kolom company ditemukan jumlah null/missing values yang sangat banyak, dimana dari 119390 baris ditemukan jumlah baris yang non-null hanya 6797 
Pada kolom children, tipe data float64 kurang sesuai karena kolom tersebut menunjukkan jumlah anak (number of childern). Tipe data yang sesuai seharusnya int64
Pada kolom company dan agent, tipe data float64 juga kurang sesuai karena kolom tersebut menunjukkan ID. Tipe data yang lebih baik adalah object 
Pada kolom reservation_status_date bertipe object, seharusnya bertipe datetime 

Recomendation:
Hapus (drop) baris-baris dengan data yang hilang pada kolom children 
Untuk kolom country, baris yang kosong diisi dengan negara portugal (PRT) karena frekuensi data yang sering muncul adalah PRT (NB: Unknown country direplace jadi Null dulu).
Untuk kolom agent, diisi dengan agent ID yang sering muncul ( modus), yakni agent ID 9.0 
Untuk kolom company di drop karena jumlah data null 94% 
Mengubah tipe data float64 menjadi int64 pada kolom childern 
Mengubah tipe data float64 menjadi object pada agent 
Mengubah tipe data object menjadi datetime pada kolom reservation_status_date 2. Insight Univariate Analysis 
Berdasarkan visualisasi countplot, pada kolom hotel terlihat bahwa City Hotel memiliki jumlah cancellation tertinggi. 
Pada bagian boxplot, beberapa variable memiliki data yang cenderung miring ke kanan (skewness positif) dan beberapa cenderung miring ke kiri (skewness kiri). 
Beberapa variabel memiliki data outlier yang harus ditindaklanjut, seperti kolom lead_time, stays_in_weekend_nights, stays_in_week_nights, adults, children, babies, previous_cancellation, previous_boking_not_canceled, booking_changes, days_in_waiting_list, adr, required_car_parking_lot, total_of_special_request 
Bila dilihat secara visual pada Distplot, variabel arrival_date_week_number memiliki distribusi normal Recomendation: 
Pakai yeo-johnson atau box-cox untuk menormalkan distribusi data yang skewd baik skewd positive atau skewd negative 
Untuk feature transformation menggunakan Normalization dan Standardization 
Menerapkan label encoding untuk data kategori dengan 2 nilai value counts, one hot encoding untuk data bulan, dan Binary Encoding untuk data dengan nilai cardinality yang tinggi 3. Insight Multivariate 
Terlihat Target memiliki korelasi positif dengan fitur adr, days_in_waiting_list, previous_cancellations, children, adults, stays_in_weeks_nights, arrival_date_week_number, arrival_date_year, lead_time 
Tidak ada variabel yang berpotensi menyebabkan multicollinearity. stays_in_weeks_night dan stays_in_weekend_night memiliki nilai korelasi paling tinggi yaitu 0,5.

STAGE 2: Preprocessing Data
Data preprocessing adalah proses yang penting dilakukan guna mempermudah proses analisis data. Proses ini dapat menyeleksi data dari berbagai sumber dan menyeragamkan formatnya ke dalam satu set data.
Data Preprocessing yang dilakukan untuk memprediksi jumlah cancel hotel booking adalah:
Handling Outlier
Penghapusan outlier menggunakan metode drop dan IQR.
Handling outlier menggunakan IQR, pemilihan metode IQR karena dalam Z-score membutuhkan asumsi data yang normal, sedangkan outlier tidak. Hal tersebut diterapkan pada feature, lead_time, stays_in_weekend_nights,  stays_in_week_nights, adr
Handling outlier menggunakan cara drop dilakukan pada feature adults, booking_changes
 b. Feature Selection
Pada feature selection, dilakukan drop beberapa feature yang menurut kami kurang menggambarkan data yaitu name, phone-number, credit_card, email, company
 c. Pipeline
Handling Missing value dilakukan dengan cara Missing impute dan replace impute. 
Missing Impute menggunakan cara menggunakan KNNImputer (numerical) dan SimpleImputer (kategorikal).
Feature Extraction:
Pengubahan tipe data dari beberapa feature.
Pembuatan beberapa feature baru dari feature yang tersedia.
Beberapa feature diubah menjadi kategori dengan isi data 0 dan 1, seperti feature kids, yang membawa anak = 1 dan yang tidak membawa anak = 0.
Feature Transformation dilakukan pada feature lead_time, stays_in_weekend_nights, stays_in_week_nights, adults, 'booking_changes, adr

Feature Encoding
label_encoding = hotel, visitor_origin
one_hot_encoding = arrival_date_year, arrival_date_month, meal, market_segment, distribution_channel, reserved_room_type, Assigned_room_type, deposit_type, customer_type, reservation_status, reservation_status_year, reservation_status_month
binary_encoding = arrival_date_day_of_month, 'arrival_date_week_number, agent, 'reservation_status_day

STAGE 3: Modelling
Modelling

Poin A, B, C, D dan E terdapat pada file jupyter (ipynb).

Eksperimen apa saja yang telah dilakukan :
Eksperimen pemodelan dengan Logistic Regression, Decision Tree, Random Forest, XG Boost	


Metode yang digunakan :
Dalam experimen pemodelan kita menerapkan metode Cross Validation untuk menentukan model mana yang nantinya perlu pertimbangan lebih lanjut

Mengapa memilih dan mengimplementasikan algoritma tersebut :
Logistic regression: cukup simple dan komputasinya cukup cepat
Decision tree: cukup interpretatatif dan improvement-nya cenderung lebih baik
Random Forest dan XG Boost : prediksi model lebih akurat, lebih stabil, dan robust
	
Jelaskan masing-masing hasil dari eksperimen model yang telah dilakukan:
Logistic Regression : 
      Dari cross validation diperoleh hasil mean f1-score 0.7524301028416677 dan std f1-score : 0.004150028792704735
      Kemudian untuk F1-Score (Train Set): 0.75
Dari hasil eksperimen model logistic regresion tersebut, diperoleh perbandingan nilai f1-score antara hasil CV dengan data training, menunjukkan hasil yang cenderung underfit.

Random Forest :
      Dari cross validation diperoleh hasil mean f1-score : 0.9114919275679754
      dan std f1-score : 0.0015737384486831103
      Kemudian untuk F1-Score (Train Set): 1.00
Dari hasil eksperimen model Random Forest tersebut, diperoleh perbandingan nilai f1-score antara hasil CV dengan data training, tidak overfit maupun underfit.

Decision Tree:
      Dari cross validation diperoleh hasil mean f1-score :0.8781225208479825  
      dan std f1-score : 0.0010586277922633948
      Kemudian untuk F1-Score (Train Set): 1.00
Dari hasil eksperimen model Decision Tree tersebut, diperoleh perbandingan nilai f1-score antara hasil CV dengan data training, overfit

XGBoost :
      Dari cross validation diperoleh hasil mean f1 : 0.9648837101649479 dan std f1 : 0.0034788093875669913
      Kemudian untuk F1-Score (Train Set): 0.98
Dari hasil eksperimen model XGBoost tersebut, diperoleh perbandingan nilai f1-score antara hasil CV dengan data training, tidak overfit maupun underfit.

Dari hasil experimen tersebut diputuskan untuk memilih model Random Forest 
karena tidak undefit maupun overfit. Selain itu, nilai standar deviasi hasil CV pada algoritma Random Forest lebih rendah  jika dibandingkan dengan algoritma XGBoost. Maka dipilihlah algoritma Random Forest sebagai pemodelan.  

Alasan menggunakan metrics pada model tersebut :
Metrcis yang kita gunakan adalah F1-score yang merupakan perhitungan harmonic mean dari precision dan recall. Hal ini dikarenakan dalam pemodelan, yakni memprediksi pelanggan yang akan membatalkan booking hotel, kita angka false positif dan false negatif dapat diturunkan.

Hyperparameter yang digunakan dan pengaruhnya terhadap model :
Dilakukan hyperparameter tuning pada model algoritma Random Forest. Berikut beberapa hyperparameter yang kami gunakan beserta pengaruhnya terhadap model.
n_estimators: jumlah pohon di dalam hutan. Pohon yang dimaksud ialah decision tree. Semakin banyak pohon, semakin bagus performa model. Namun, lama waktu proses pemodelan menjadi lebih lama.
max_depth: jumlah maksimum dari tingkatan atau level setiap decision tree. Semakin tinggi nilai, semakin overfit model.
max_features: jumlah maksimum fitur yang dipertimbangkan kapan akan membagi node. Semakin tinggi nilainya, semakin berkurang kecepatan algoritma, namun performance model bisa lebih meningkat.
min_samples_leaf: jumlah minimal data point yang dibolehkan ada untuk setiap leaf node. Semakin banyak samples leaf, model akan semakin underfit. 
min_samples_split: jumlah minimal data points yang ditempatkan pada suatu node sebelum node dipisah. Semakin nilai ditingkat, setiap pohon di hutan akan menjadi lebih overfit.


Feature Importance

Dari grafik feature importance (tertera di file ipynb) yang di-generate dari model algoritma Random Forest, diperoleh beberapa fitur model yang memiliki skor tinggi. Tujuh (7) di antaranya dimulai dari yang tertinggi ialah Deposit Type: Non Refund, Deposit Type: No Deposit, visitor_origin, lead_time, total_of_special_requests_cat, previous_cancellation_cats, required_car_parking_spaces_cat.

Non Refund merupakan jenis deposit type yang memungkinkan dapat memengaruhi terjadinya booking cancellation. Hal ini sebenarnya merupakan kasus unik karena, berdasarkan EDA, diketahui meskipun non refund, hampir 100% mereka yang non refund malah melakukan cancelation booking. Hal ini sebenarnya dari segi revenue tidak menjadi masalah karena hotel telah mendapatkan pemasukan dari non refund deposit yang dilakukan pelanggan.
No Deposit merupakan jenis deposit type yang dimungkinkan paling memengaruhi terjadinya booking cancellation karena ketidakadaan deposit bisa jadi membuat pelanggan tidak berpikir dua kali atau lebih untuk melakukan pembatalan booking.
Dengan mengetahui fitur ini, diharapkan dapat diberlakukan kebijakan yang mampu mengendalikan No Deposit, misalnya yakni memberlakukan jenis deposit tertentu ketika akan melakukan booking.
visitor_origin merupakan fitur yang memisahkan antara pemesan lokal yakni warga Portugal dengan pemesan internasional. Diketahui (dari EDA juga) bahwa pemesan lokal memiliki tendensi untuk melakukan pembatalan booking daripada pemesan internasional. Hal ini bisa saja terjadi dengan asumsi bahwa warga lokal lebih mudah melakukan cancellation karena jarak hotel yang relatif dekat dari rumah mereka. Berbeda dengan pemesan internasional yang biasanya memiliki initerary yang mengikat untuk keperluan mendapatkan visa atau lebih berkomitmen untuk datang berlibur karena masalah waktu misal cuti.
Hal yang bisa dilakukan untuk mencegah ini ialah memberikan promo khusus bagi warga Portugal sehingga mengurungkan niat mereka untuk melakukan pembatalan booking. Contohnya dengan memberikan paket liburan khusus warga Portugal dengan deposit yang masih terjangkau.
lead_time diketahui juga menjadi fitur yang memicu dilakukannya cancellation booking. Diasumsikan bahwa dengan lead_time yang panjang, maka kecenderungan pelanggan untuk membatalkan booking juga semakin meningkat. 
Hal yang bisa dilakukan untuk mencegah terjadinya booking sewaktu-waktu yang bisa merugikan hotel (dalam kasus ini ialah booking jauh-jauh hari namun dilakukan cancel di waktu mendekati check-in) ialah memberikan jangka waktu tertentu bagi pemesan untuk melakukan cancellation tanpa penalti. Bilamana melebihi jangka waktu tersebut, maka pemesan akan dikenakan charge tertentu dari kartu kredit tersebut.
total_of_special_requests_cat, didasarkan pada EDA, diketahui bahwa pemesan yang melakukan permintaan khusus tertentu pada booking-nya cenderung tidak membatalkan booking-nya. Hal ini bisa saja terjadi karena special request membutuhkan biaya tambahan atau ada ketentuan khusus di mana special request bersifat mengikat, seperti menjadi risiko pribadi bagi pemesan.
Dengan memberikan strategi khusus misal memberikan penawaran-penawaran di awal pemesanan terkait service untuk permintaan khusus, diharapkan pelanggan akan melakukan special request dan kecenderungan untuk membatalkan pemesanan akan diurungkan.
previous_cancellation_cats, didasarkan pada EDA yang dilakukan, diketahui bahwa pemesan yang sebelumnya pernah melakukan cancellation cenderung akan melakukan booking cancellation lagi di waktu-waktu ke depannya. Hal ini bisa saja terjadi karena pemesan merasa bahwa tidak ada penalti atas melakukan hotel booking sewaktu-waktu lalu membatalkannya juga sewaktu-waktu.
Hal yang bisa dilakukan untuk mengatasi hal ini ialah memberikan jangka waktu tertentu bagi pemesan untuk melakukan cancellation tanpa penalti. Apabila melebihi jangka waktu terkait, maka pemesan akan dikenakan charge/penalti yang diambil dari kartu kredit pemesan. Tentunya dengan catatan sistem yang diberlakukan untuk pemesanan ialah menggunakan kartu kredit di awal.
required_car_parking_spaces_cat, didasarkan pada EDA, terlihat bahwa mereka yang tidak membutuhkan lahan parkir di hotel cenderung akan melakukan pembatalan pemesanan. Mirip dengan special request, dimungkinkan apabila membutuhkan lahan parkir hotel, maka akan dikenakan biaya khusus di awal atau ketentuan khusus yang mengikat bagi pemesan.
Mengetahui hal tersebut, hotel terkait dapat memberikan promo tertentu bagi mereka yang tertarik datang dengan rombongan mobil misalnya karya wisata atau acara institusi sehingga pemesan akan melakukan permintaan khusus terkait lahan parkir dan diharapkan kecenderungan untuk cancel booking akan menurun.

B. Feature selection dari feature importance, dan lakukan iterasi modeling dengan feature
yang dipilih

Usai dilakukan iterasi modeling menggunakan lima (5) feature utama dari feature importance, hasil keluaran dari model Random Forest berupa confusion matrix tidaklah jauh berbeda dengan confusion matrix sebelum dilakukan feature selection ulang. Hal ini mengindikasikan bahwa performa model sebelum dan sesudah dilakukan feature selection ulang tidaklah berbeda jauh, bahkan hanya dengan lima fitur utama, menjadikan model Random Forest setelah feature selection ulang dapat dikatakan cukup lebih baik dibanding model sebelumnya karena meskipun kompleksitas lebih kecil tapi performa model masih tergolong baik.

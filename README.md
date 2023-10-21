# Bank Churn Prediction - by Data Goddesses

<img src=assets/banner.png>

**👧🏻 Member of Data Goddesses :**
* Aleisya
* Alicia
* Deva
* Devi
* Fiorent
* Najmi

<!-- ## 🏦 Bussines Understanding  -->
### ⚙️ Problem Statement 
<p style='text-align: justify'>Tingkat churn pada Bank Saia mencapai 20.4%. Tingkat churn yang diterima atau ditetapkan bank pada umumnya kurang dari 5-10% per tahun. Hal tersebut mengindikasikan bahwa terdapat <strong>masalah mengenai tingginya tingkat churn</strong> pada Bank Saia. Masalah tersebut harus segera teratasi karena tingkat churn yang tinggi dapat berdampak pada penurunan revenue dan profit, bahkan dapat pengaruh buruk pada citra perusahaan. Oleh karena itu, diperlukan tindakan untuk menjaga nasabah yang telah ada dan menurunkan churn rate. </p>

### 🎯 Goals
<p style='text-align: justify'><b>Mengurangi tingkat churn atau churn rate</b> sehingga bank dapat mempertahankan nasabah yang ada dengan mengidentifikasi nasabah yang berisiko churn berdasarkan karakteristik nasabah.</p>

### 📌 Objective
* Melakukan deep analytics atau EDA untuk mengidentifikasi faktor-faktor utama yang berpengaruh kepada keputusan nasabah churn.
* Membangun model machine learning yang dapat memprediksi nasabah akan churn atau tidak.

### ✏️ Business Metrics
**Churn Rate**  
Persentase tingkat nasabah yang melakukan churn


## Data Description 🗄️ 
Data yang kami gunakan pada project ini berasal dari Kaggle.  
Dataset : [Predicting Churn for Bank Customers](https://www.kaggle.com/datasets/adammaus/predicting-churn-for-bank-customers)  

> Predict whether a bank's customers will churn (leave the bank) based on their banking behaviors and demographic data

Dataset terdiri dari ```10000 baris```, mengandung```14 feature``` dan ```1 target``` variable ```'Exited'```


Feature : 
* `RowNumber` - corresponds to the record (row) number 
* `CustomerId` - ontains random values
* `Surname` - the surname of a customer
* `CreditScore` - the credit score of the customer
* `Geography`- the geographical location or country where the customer is based
* `Gender` - the gender of customer, Male or Female
* `Age` - the age of the customer
* `Tenure` - the number of years that the customer has been a client of the bank
* `Balance` - the account balance of the customer
* `NumOfProducts` - the number of bank products that the customer is using
* `IsActiveMember` - whether the customer is an active member of the bank
* `EstimatedSalary` -  this binary column indicates whether the customer has exited (1) or no (0)


## === Stage 1 : EDA (Exploratory Data Analysis) ===

### Descriptive Statistics

### Univariate Analysis
#### **Histplot Numerical Features**
**Histplot Analysis :**
- Kolom `Credit Score` memiliki distribusi negative skew mendekati normal. mayoritas customer memiliki jumlah credit score di rentang 600 sampai 700, dan ditemukan outliers pada kolom ini dengan nilai 400 kebawah.
- Kolom `Age` memiliki distribusi Positive skew. mayoritas customer berusia di rentang 30 tahun sampai 40 tahun. Ditemukan pula outliers pada kolom ini dengan nilai paling ekstrem sekitar 90 tahun keatas.
- Kolom `Tenure` memiliki distribusi merata.
- Kolom `Balance` memiliki distribusi bimodal. pada kolom ini terdapat satu nilai yang mendominasi yaitu '0'
- Kolom `EstimatedSalary` memiliki distribusi merata. Dimana jumlah customer pada tiap estimated salary itu hampir sama rata, artinya tidak ada kelompok gaji yang paling mendominasi.
- Kolom `NumOfProducts` memiliki distribusi positive skew. mayoritas customer membeli product dengan nomor 1 dan 2, dan ditemukan outliers pada kolom ini dengan nilai 4


**Tindak Lanjut**
- Berdasarkan visualisasi tersebut terdapat beberapa data yang memiliki outliers, sehingga perlu dilakukan handling pada outliers.
- Melakukan Transformasi pada data dengan distribusi skew untuk mengubah distribusi data menjadi lebih mendekati distribusi normal


#### **Boxplot Numerical Features**
**Boxplot Analysis :**
- Kolom `CreditScore` ditemukan data outlier yang sebagian besar terletak di bawah batas bawah IQR.
- Kolom `Age` ditemukan data outlier yang sebagian besar terletak di atas batas atas IQR.
- Kolom `Tenure` tidak ditemukan adanya data outlier.
- Kolom `Balance` tidak ditemukan adanya data outlier.
- Kolom `EstinatedSalary` tidak ditemukan adanya data outlier.
- Kolom `NumOfProducts` ditemukan data outlier yang sebagian besar terletak di atas batas atas IQR.


**Tindak Lanjut**
- Untuk data yang mengandung outlier akan difilter dengan menggunakan metode IQR.

#### **Barplot Categorical Features**
**Barplot Analysis :**
- Dalam kolom `Geography` terdapat nilai yang paling umum yaitu 'France'
- Dalam kolom `Gender` frekuensi tertinggi terdapat pada nilai '1' dan tidak terlalu terlihat perbandingan jumlah yang tinggi diantara nilai.
- Dalam kolom `HasCrCard` didapatkan bahwa mayoritas kostumer memiliki Credit Card
- Dalam kolom `NumOfProducts`,  dua nilai yang paling sering muncul adalah '1' dan '2'.
- Dalam kolom `IsActiveMember`tidak ada nilai yang terlalu mendominasi
- Dalam kolom `Exited`terdapat nilai '0' yang paling umum, yaitu pelanggan yang tidak churn.


**Tindak Lanjut**
- Berdasarkan visualisasi tersebut, ditemukan beberapa data yang imbalance. Oleh karena itu perlu dianalisis lebih lanjut untuk mengetahui sejauh mana ketidakseimbangan data tersebut.

**Catatan Tambahan**
- Kolom RowNumber termasuk index kolom dan CustomerID merupakan identifer unik masing-masing pelanggang, sehingga keduanya tidak dimasukkan kedalam tipe data kategorik.

#### **Imbalanced Data Analysis**

- source: [Google developer machine learning 'Imbalanced Data'](https://developers.google.com/machine-learning/data-prep/construct/sampling-splitting/imbalanced-data#:~:text=A%20classification%20data%20set%20with,smaller%20proportion%20are%20minority%20classes.)

  
| Degree of imbalance | Proportion of Minority Class |
| :---                | :---                        |
| Mild                | 20-40% of the data set      |
| Moderate            | 1-20% of the data set       |
| Extreme             | <1% of the data set         |


**Hasil observasi :**

- Dalam kolom `Geography` terdapat ketidakseimbangan data, kolom Germany dan spain termasuk kedalam kateogri mild dengan proporsi masing-masing 25.1% dan 24.8%
- Dalam kolom `Gender` tidak terdapat ketidakseimbangan data.
- Dalam kolom `HasCrCard` terdapat ketidakseimbangan data pada nilai '0', termasuk kedalam kateogri mild dengan proporsi 29.4%
- Dalam kolom `NumOfProducts` terdapat ketidakseimbangan data yang masuk kedalam kategori extreme untuk kolom nilai '4' sebanyak 0.6%, dan kolim nilai '3' termasuk moderate dengan proporsi 2.7 %
- Dalam kolom `IsActiveMember` tidak terdapat ketidakseimbangan data.
- Dalam kolom `Exited` terdapat ketidakseimbangan data. kolom dengan nilai '1' memiliki proporsi 20.4% yang termasuk kedalam kategori mild.

**Tindak Lanjut :**
- Perlu dilakukannya penanganan ketidakseimbangannya data yang tertutama yang termasuk kedalam kategori extreme dan moderate di kolom NumOfProducts, kategori mild yaitu kolom `Geography`, `HasCrCard`, dan `Exited`.

#### **Outliers Table Analysis**
**Hasil observasi :**  
Pada data tipe numerik terdapat outlier pada kolom `CreditScore`, `Age`, dan `NumOfProducts`.

- Pada kolom `CreditScore` terdapat 15 data outlier, dengan nilai terjauh terdapat di bawah IQR yaitu 350000
- Pada kolom `Age` terdapat 359 data outlier, dengan nilai terjauh terdapat di atas IQR yaitu 92.
- Pada kolom `NumOfProducts` terdapat 60 data outlier, dengan nilai terjauh terdapat di atas IQR yaitu 4

### Multivariate Analysis
#### **Heatmap Correlation** 
1. Korelasi ke target (Exited)  
Beberapa feature yang kemungkinan besar relevan dan perlu dipertahankan :  
    * `Age` memiliki korelasi **positif 0.29**  
Dapat dikatakan bahwa semakin tua pelanggan, semakin tinggi kecenderungan mereka akan churn.  
    * `IsActiveMember` memiliki korelasi **negatif -0.16**  
Dapat dikatakan bahwa semakin tinggi balance yang dimiliki nasabah, semakin tinggi juga kecenderungan mereka untuk churn.  
    * `Balance` memiliki korelasi **positif 0.12**  
Dapat dikatakan bahwa pelanggan yang tidak aktif memiliki kemungkinan keluar yang lebih tinggi (hubungan berbalik)  
    * `NumOfProducts` memiliki korelasi **negatif -0.05**  
Dapat dikatakan bahwa pelanggan dengan lebih banyak produk (NumOfProduct) cenderung memiliki kemungkinan churn yang lebih rendah.<br><br>

2. Korelasi antar feature  
    * `Age` dan `IsActiveMember` memiliki korelasi **positif 0.09**  
Dapat dikatakan bahwa nasabah yang lebih tua, sedikit lebih cenderung menjadi anggota yang aktif.
    * `Balance` dan `NumOfProduct` memiliki korelasi **negatif -0.30**
Dapat dikatakan bahwa nasabah yang dengan balance atau saldo rendah cenderung memiliki lebih banyak produk.


Karena korelasi antar kolom pada dataset tersebut cenderung memiliki nilai yang rendah, yaitu berada dalam range 0.00 hingga 0.29. Kami memutuskan untuk membuat nilai `threshold` pada angka `0.05`, sehingga feature-feature dengan nilai korelasi >=0.05 kemungkinan besar akan kami pertahankan.

#### **Pair Plot of Numerical Features by Exit Status**
Berdasarkan grafik yang telah dibuat, ditemukan sedikit kecenderungan bahwa 
> nasabah dengan `CreditScore` dibawah 400 dan `EstimatedSalary` sedang ke tinggi cenderung melakukan churn. 

Meskipun terdapat pola ini, kedua feature tersebut tidak cukup dikatakan berkorelasi dengan target, sehingga feature ini tidak relevan dan tidak perlu dipertahankan.

#### **Churn Percentage by Categorical Features**
Sebelumnya telah dilakukan multivariate analysis menggunakan numerical features, sekarang kami akan melihat menganalisis feature yang termasuk ke dalam categorical features, yaitu terdapat `Geography` dan `Gender`.

Berdasarkan grafik tersebut, didapatkan insight mengenai korelasi antara fitur-fitur dan label `Exited`:
   - Pada `Geography`, terdapat **perbedaan yang signifikan** antara negara Germany dengan France dan Spain yaitu dalam proporsi nasabah yang churn (Exited=1) dan yang tidak churn (Exited=0)
   - Sementara itu, `Gender` **tidak menunjukkan perbedaan** yang signifikan dalam visualisasi diatas, yang berarti fitur ini mungkin tidak begitu relevan dalam memprediksi nasabah yang churn (Exited).
   
#### **Kesimpulan Multivariate Analysis**
Berdasarkan hasil keseluruhan analisis Multivariate tersebut, dapat diambil kesimpulan bahwa feature yang paling relevan dan harus dipertahankan adalah sebagai berikut :

* **Age**
* **IsActiveMember**
* **Balance**
* **NumOfProduct**
* **Geography**

### Business Insight

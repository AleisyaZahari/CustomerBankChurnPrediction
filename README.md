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

### Multivariate Analysis
#### **Heatmap Correlation**
Berdasarkan heatmap correlation yang telah dibuat, kita dapatkan suatu insight :  
1. Korelasi ke target (Exited)  
Beberapa feature yang kemungkinan besar relevan dan perlu dipertahankan :  
    * `Age` memiliki korelasi **positif 0.29**  
Dapat dikatakan bahwa semakin tua pelanggan, semakin tinggi kecenderungan mereka akan churn.  
    * `IsActiveMember` memiliki korelasi **negatif -0.16**  
Dapat dikatakan bahwa semakin tinggi balance yang dimiliki nasabah, semakin tinggi juga kecenderungan mereka untuk churn.  
    * `Balance` memiliki korelasi **positif 0.12**  
Dapat dikatakan bahwa pelanggan yang tidak aktif memiliki kemungkinan keluar yang lebih tinggi (hubungan berbalik)  
    * `NumOfProducts` memiliki korelasi **negatif -0.05**  
Dapat dikatakan bahwa pelanggan dengan lebih banyak produk (NumOfProduct) cenderung memiliki kemungkinan churn yang lebih rendah.

2. Korelasi antar feature  
    * `Age` dan `IsActiveMember` memiliki korelasi **positif 0.09**  
Dapat dikatakan bahwa nasabah yang lebih tua, sedikit lebih cenderung menjadi anggota yang aktif.
    * `Balance` dan `NumOfProduct` memiliki korelasi **negatif -0.30**
Dapat dikatakan bahwa nasabah yang dengan balance atau saldo rendah cenderung memiliki lebih banyak produk.


Karena korelasi antar kolom pada dataset tersebut cenderung memiliki nilai yang rendah, yaitu berada dalam range 0.00 hingga 0.29. Kami memutuskan untuk membuat nilai `threshold` pada angka `0.05`, sehingga feature-feature dengan nilai korelasi >=0.05 kemungkinan besar akan kami pertahankan.

#### **Pair Plot of Numerical Features by Exit Status**
Berdasarkan grafik yang telah dibuat, ditemukan sedikit kecenderungan bahwa nasabah dengan `CreditScore` dibawah 400 dan `EstimatedSalary` sedang ke tinggi cenderung melakukan churn. 

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
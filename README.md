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
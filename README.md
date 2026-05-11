# JCDS-0808_Remedial

# Telco Customer Churn Analysis & Prediction

[![Streamlit App](https://img.shields.io/badge/Streamlit-App-FF4B4B?style=for-the-badge&logo=streamlit)](https://telcocustomerchurnwildan.streamlit.app)
[![Tableau Dashboard](https://img.shields.io/badge/Tableau-Dashboard-E97627?style=for-the-badge&logo=tableau)]([https://public.tableau.com/views/TelcoCustomerDashboard_17706500189310/Home](https://public.tableau.com/app/profile/muhamad.wildan.trisianly/viz/TelcoCustomerDashboard_17706500189310/Home?publish=yes))
[![Presentation](https://img.shields.io/badge/Canva-Presentation-00C4CC?style=for-the-badge&logo=canva)](https://canva.link/l6yjq9bhzfy8ke0)

## 📋 Latar Belakang

Industri telekomunikasi menghadapi tingkat persaingan yang sangat tinggi dengan **churn rate global mencapai 15-25% per tahun**. Churn rate (tingkat pelanggan yang berhenti berlangganan) menjadi permasalahan krusial karena:

- **Biaya akuisisi pelanggan baru 5-10x lebih mahal** dibanding mempertahankan pelanggan existing
- Pelanggan cenderung **price-sensitive** dengan banyak alternatif provider
- Kehilangan pelanggan berdampak langsung pada **pendapatan dan sustainability bisnis**

Pendekatan konvensional yang reaktif (bertindak setelah pelanggan churn) terbukti kurang optimal. Oleh karena itu, diperlukan **pendekatan prediktif berbasis machine learning** untuk mengidentifikasi pelanggan berisiko churn secara dini.

---

## 🎯 Problem Statement

Perusahaan telekomunikasi belum memiliki sistem prediktif yang mampu mengidentifikasi pelanggan berpotensi churn secara akurat berdasarkan data historis. Padahal, data seperti:
- Karakteristik pelanggan (EDA)
- Penggunaan layanan
- Jenis paket dan kontrak
- Riwayat interaksi

  dapat dimanfaatkan untuk mengenali pola perilaku pelanggan yang berisiko churn.

 ---

  ## 🎯 Goals

1. **Menganalisis pola perilaku pelanggan** yang berkontribusi terhadap churn melalui analisis demografi dan geografi
2. **Membangun model machine learning** untuk memprediksi kemungkinan churn pelanggan secara akurat
3. **Menghasilkan insight berbasis data** untuk strategi retensi yang proaktif dan tepat sasaran
4. **Mendukung pengambilan keputusan bisnis** dengan menyediakan informasi pelanggan berisiko churn tinggi

---

### 2. **Exploratory Data Analysis (EDA)**
**Fokus Demografi:**
- Analisis profil pelanggan (gender, age, senior citizen, family status)
- Korelasi satisfaction score dengan churn

**Fokus Geografi:**
- Pemetaan distribusi churn menggunakan **Folium heatmap**
- Identifikasi top cities dengan churn terbanyak
- identifikasi top cities dengan pelanggan terbanyak

  
**Fokus Contract and Services:**
- Analisis hubungan contract type dengan churn rate.
- Identifikasi bahwa month-to-month contract memiliki churn tertinggi.
- Analisis pengaruh internet service type terhadap churn (fiber optic vs DSL vs no internet).
- Evaluasi dampak service add-ons (TechSupport, OnlineSecurity, OnlineBackup, DeviceProtection).
- Identifikasi bahwa TechSupport dan OnlineSecurity menurunkan churn signifikan.
- Analisis kombinasi contract + service untuk menemukan segmen berisiko tinggi.

  
**Fokus Monetary:**
- Analisis hubungan monthly charges dengan churn.
- Identifikasi bahwa pelanggan churn memiliki biaya bulanan lebih tinggi.
- Analisis total revenue dan CLTV antara pelanggan churn dan non-churn.
- Identifikasi bahwa pelanggan churn memiliki nilai jangka panjang lebih rendah.
- Analisis total refunds sebagai indikator ketidakpuasan sebelum churn.
- Evaluasi perilaku transaksi melalui payment method dan paperless billing.


### 3. **Machine Learning Modeling**
- Problem diformulasikan sebagai binary classification untuk memprediksi pelanggan churn dan non-churn.
- Model yang digunakan: Logistic Regression, Decision Tree, Random Forest, dan XGBoost.
- Penanganan imbalanced data dilakukan menggunakan class weight, scale_pos_weight pada XGBoost, dan evaluasi berbasis metrik yang sesuai untuk data imbalance.
- Hyperparameter tuning dilakukan menggunakan GridSearchCV.
- Model dievaluasi menggunakan ROC-AUC, PR-AUC, recall, F2-score, confusion matrix, dan cost-benefit analysis.
- Threshold optimization dilakukan untuk menyesuaikan hasil prediksi dengan kebutuhan bisnis retensi pelanggan.

### 4. **Model Interpretation**
- SHAP values digunakan untuk menjelaskan kontribusi fitur terhadap prediksi model secara overall.
- Interpretasi model diterjemahkan menjadi business insights dan rekomendasi strategi retensi pelanggan.

---


## 📊 Metrics Evaluation

### Confusion Matrix Components
- **True Negative (TN)**: Prediksi tidak churn ✓ (benar)
- **False Positive (FP)**: Prediksi churn ✗ (salah, Type I Error)
- **False Negative (FN)**: Prediksi tidak churn ✗ (salah, **Type II Error - lebih kritis**)
- **True Positive (TP)**: Prediksi churn ✓ (benar)

### Primary Metric: **F2-Score**
```
F2 = (1 + 2²) × (Precision × Recall) / (2² × Precision + Recall)
```

**Mengapa F2-Score?**
- Memberikan **bobot 2x lebih besar pada Recall**
- Meminimalkan False Negative (pelanggan churn yang terlewat)
- Lebih fokus pada deteksi pelanggan berisiko churn

**Trade-off:**
- **False Positive** → Biaya retensi tidak perlu ($10.6)
- **False Negative** → Kehilangan pelanggan ($53)
- FN **5x lebih merugikan**, sehingga harus diminimalkan

---

## 📁 Dataset Description
Untuk mendapatkan hasil analisis dan machine learning yang lebih memadai, kami mencoba mencari data tambahan yang bersumber dari link di bawah, sehingga kami menggunakan 2 sumber data yang akan digunakan pada project ini
**Source:** 
- [Kaggle - Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- [HuggingFace - Telco Customer Churn](https://huggingface.co/datasets/aai510-group1/telco-customer-churn)

**Total Records:** 7,043 customers  
**Features:** 42 columns (setelah cleaning dan feature engineering)

### Key Features:

**Demographic:**
- `age`, `gender`, `seniorcitizen`, `partner`, `dependents`

**Geographic:**
- `city`, `latitude`, `longitude`, `zipcode`, `population`

**Service Usage:**
- `internetservice`, `phoneservice`, `multiplelines`, `streamingmovies`, `streamingtv`, `streamingmusic`

**Service Add-ons:**
- `onlinesecurity`, `onlinebackup`, `deviceprotection`, `techsupport`

**Contract & Billing:**
- `contract`, `paymentmethod`, `paperlessbilling`, `monthlycharges`, `tenure`

**Financial:**

- `totalcharges`, `totalrevenue`, `cltv`, `totalrefunds`

**Target Variable:**
- `churn` (Yes/No atau 1/0)

---

## 🔍 Key Findings

### 📊 EDA Insights - Demografi

**Profil Pelanggan Berisiko Tinggi:**
1. **Senior Citizen** memiliki churn rate lebih tinggi dibandingkan pelanggan non-senior.
2. **Pelanggan tanpa partner dan dependents** cenderung lebih rentan churn karena memiliki keterikatan layanan yang lebih rendah.
3. **Satisfaction Score rendah** menjadi salah satu indikator terkuat terhadap churn.
4. Pelanggan dengan satisfaction score rendah perlu diprioritaskan dalam strategi retention karena menunjukkan potensi ketidakpuasan yang tinggi.

**Gender:**  
Tidak terdapat perbedaan churn yang signifikan antara pelanggan pria dan wanita, sehingga gender bukan faktor utama dalam mengidentifikasi risiko churn.

---

### 🗺️ EDA Insights - Geografi

**Hotspot Churn:**
1. **Beberapa city memiliki jumlah churned customers yang tinggi**, terutama pada area dengan customer base yang besar.
2. **City dengan jumlah churn tertinggi belum tentu memiliki churn rate tertinggi**, sehingga analisis perlu melihat churn count dan churn rate secara bersamaan.
3. Distribusi churn terlihat tidak merata antar wilayah, yang menunjukkan adanya potensi perbedaan kondisi pasar, kualitas layanan, atau tekanan kompetitor di area tertentu.
4. Visualisasi berbasis latitude dan longitude membantu mengidentifikasi konsentrasi churn secara geografis.

**Business Insight:**  
Area dengan konsentrasi churn tinggi dapat menjadi prioritas untuk evaluasi kualitas jaringan, campaign retention regional, dan analisis kompetitor lokal.

---

### 💡 Churn Reason Analysis

**Top Churn Drivers:**
1. **Competitor** menjadi salah satu alasan utama pelanggan berpindah layanan.
2. **Dissatisfaction** menunjukkan adanya ketidakpuasan terhadap kualitas layanan atau pengalaman pelanggan.
3. **Attitude/Support Experience** mengindikasikan bahwa interaksi dengan customer service dapat memengaruhi keputusan pelanggan untuk churn.
4. **Price-related reasons** menunjukkan sebagian pelanggan sensitif terhadap biaya layanan.
5. Alasan lainnya menunjukkan bahwa churn tidak hanya dipengaruhi satu faktor, tetapi merupakan kombinasi dari harga, kualitas layanan, kompetitor, dan pengalaman pelanggan.

**Insight:**  
Churn lebih banyak dipicu oleh kombinasi **kompetitor, kualitas layanan, dan customer experience**, sehingga strategi retention tidak cukup hanya menggunakan diskon harga.

---

### 🎯 Contract & Services Insights

**Contract Type vs Churn:**
1. **Month-to-month contract** memiliki churn rate paling tinggi dibandingkan kontrak jangka panjang.
2. **One-year dan two-year contract** menunjukkan churn rate yang lebih rendah, menandakan bahwa komitmen kontrak berperan dalam meningkatkan customer retention.
3. Pelanggan dengan kontrak jangka pendek lebih mudah berpindah karena memiliki switching barrier yang rendah.

**Services vs Churn:**
1. Pelanggan dengan **Fiber Optic** cenderung memiliki churn rate lebih tinggi dibandingkan tipe internet service lainnya.
2. Pelanggan yang tidak menggunakan **TechSupport** dan **OnlineSecurity** cenderung memiliki risiko churn lebih tinggi.
3. Service add-ons seperti **TechSupport** dan **OnlineSecurity** berasosiasi dengan churn rate yang lebih rendah.
4. Kombinasi **Fiber Optic + tanpa TechSupport/OnlineSecurity + month-to-month contract** menjadi salah satu segmen pelanggan dengan risiko churn tinggi.

**Business Insight:**  
Pelanggan month-to-month, khususnya pengguna Fiber Optic tanpa layanan pendukung, perlu menjadi target utama untuk program retention, bundling, atau upgrade layanan.

---

### 💳 Payment & Billing Insights

**Payment Method vs Churn:**
1. **Electronic check** menunjukkan churn rate paling tinggi dibandingkan metode pembayaran lainnya.
2. Metode pembayaran otomatis seperti **bank transfer** dan **credit card** cenderung memiliki churn rate lebih rendah.
3. Auto-payment dapat menjadi indikator pelanggan yang lebih stabil karena proses pembayaran lebih mudah dan konsisten.

**Paperless Billing:**
1. Pelanggan dengan **paperless billing** menunjukkan churn rate yang lebih tinggi dibandingkan non-paperless billing.
2. Paperless billing tidak selalu menjadi penyebab churn, tetapi dapat menjadi indikator segmen pelanggan yang lebih aktif, digital, dan lebih mudah membandingkan layanan kompetitor.

**Business Insight:**  
Pelanggan dengan electronic check dan paperless billing perlu dipantau lebih dekat karena dapat menjadi segmen dengan risiko churn lebih tinggi.

---

### 💰 Monetary Insights

**Revenue & Charges Pattern:**
1. Pelanggan churn cenderung memiliki **monthly charges lebih tinggi** dibandingkan pelanggan non-churn.
2. Pelanggan dengan biaya bulanan tinggi lebih rentan churn, terutama jika value layanan yang dirasakan tidak sebanding dengan biaya yang dibayar.
3. **Total revenue pelanggan churn cenderung lebih rendah** karena masa berlangganan mereka lebih pendek.
4. **Customer lifetime value pelanggan churn cenderung lebih rendah**, sehingga churn berdampak langsung terhadap potensi pendapatan jangka panjang.
5. **Total refunds** dapat menjadi sinyal adanya ketidakpuasan atau masalah layanan sebelum pelanggan churn.

**Business Insight:**  
Pelanggan dengan monthly charges tinggi perlu mendapatkan perhatian khusus melalui evaluasi value layanan, program loyalty, atau penawaran paket yang lebih sesuai.


---

## 🤖 Machine Learning Results

## 🤖 Machine Learning Results

### Model Terbaik: **RandomUnderSampler + XGBoost + Threshold Optimization**

Model terbaik pada project ini adalah kombinasi **RandomUnderSampler + XGBoost + Threshold Optimization**. Model ini dipilih berdasarkan **F2-Score**, karena tujuan utama project adalah mengidentifikasi sebanyak mungkin pelanggan yang berpotensi churn dan mengurangi pelanggan churn yang tidak terdeteksi oleh model.

Model final terdiri dari:
- **RandomUnderSampler** untuk menangani imbalance data dengan mengurangi jumlah kelas mayoritas.
- **XGBoost Classifier** sebagai model utama untuk melakukan prediksi churn.
- **Threshold Optimization** untuk menyesuaikan batas klasifikasi agar lebih sesuai dengan tujuan bisnis retensi pelanggan.

### Best Hyperparameters

```python
{
    "model__colsample_bytree": 1.0,
    "model__learning_rate": 0.05,
    "model__max_depth": 3,
    "model__n_estimators": 400,
    "model__reg_lambda": 2,
    "model__subsample": 1.0
}
```

### Best Threshold
threshold = 0.30302092

### F2-Score Comparison

| Model | Train F2-Score | Test F2-Score |
|-------|----------------|---------------|
| **Base Model** | 97.80% | 92.36% |
| **Best Model** | 94.72% | 93.56% |

Berdasarkan hasil evaluasi, Best Model berhasil meningkatkan performa pada data test, dengan F2-Score naik dari 92.36% pada Base Model menjadi 93.56% pada Best Model.

Karena project ini berfokus pada customer retention, F2-Score digunakan sebagai metrik utama karena memberikan bobot lebih besar pada recall. Dalam konteks bisnis, hal ini penting karena pelanggan churn yang tidak terdeteksi dapat menyebabkan kehilangan revenue dan hilangnya kesempatan untuk melakukan strategi retensi.

---

## 💼 Business Impact & Cost-Benefit Analysis

Untuk mengevaluasi dampak bisnis dari model, digunakan pendekatan cost-benefit berdasarkan dua jenis kesalahan prediksi, yaitu False Positive dan False Negative.

### Cost Assumption

- **False Positive (FP): $20**  
  Biaya intervensi retention yang tidak tepat sasaran, misalnya promo atau diskon kepada customer yang sebenarnya tidak churn.

- **False Negative (FN): $200**  
  Biaya kehilangan customer churn yang tidak terdeteksi, seperti kehilangan revenue, customer lifetime value, dan biaya akuisisi customer baru.

### Cost-Benefit Comparison

| Scenario | FP | FN | Total Cost |
|---------|----|----|------------|
| **Without Model - All Predicted Churn** | 1,035 | 0 | **$20,700** |
| **Without Model - All Predicted Not Churn** | 0 | 374 | **$74,800** |
| **Base Model** | 62 | 21 | **$5,440** |
| **Best Model** | 94 | 8 | **$3,480** |

### Business Interpretation

Best Model menghasilkan total cost sebesar **$3,480**, lebih rendah dibandingkan Base Model sebesar **$5,440**. Artinya, penggunaan model terbaik mampu menurunkan estimasi cost sebesar **$1,960** dibandingkan Base Model.

Penurunan cost ini terutama disebabkan oleh berkurangnya jumlah **False Negative** dari **21 menjadi 8**. Dalam konteks churn prediction, hal ini penting karena False Negative berarti customer yang sebenarnya churn tetapi tidak terdeteksi oleh model, sehingga perusahaan kehilangan kesempatan untuk melakukan retention action.

Meskipun Best Model meningkatkan jumlah **False Positive** dari **62 menjadi 94**, trade-off ini masih dapat diterima karena biaya False Positive lebih rendah dibandingkan False Negative. Dengan kata lain, memberikan campaign kepada beberapa customer yang sebenarnya tidak churn masih lebih murah dibandingkan kehilangan customer yang benar-benar churn.

Oleh karena itu, Best Model lebih sesuai untuk mendukung strategi customer retention karena mampu menekan potensi kerugian bisnis dan membantu perusahaan memprioritaskan customer dengan risiko churn tinggi.

----

## 💼 Business Impact & Cost-Benefit Analysis

Untuk mengevaluasi dampak bisnis dari model, digunakan pendekatan cost-benefit berdasarkan dua jenis kesalahan prediksi, yaitu False Positive dan False Negative.

### Cost Assumption

- **False Positive (FP): $20**  
  Biaya intervensi retention yang tidak tepat sasaran, misalnya promo atau diskon kepada customer yang sebenarnya tidak churn.

- **False Negative (FN): $200**  
  Biaya kehilangan customer churn yang tidak terdeteksi, seperti kehilangan revenue, customer lifetime value, dan biaya akuisisi customer baru.

### Cost-Benefit Comparison

| Scenario | FP | FN | Total Cost |
|---------|----|----|------------|
| **Without Model - All Predicted Churn** | 1,035 | 0 | **$20,700** |
| **Without Model - All Predicted Not Churn** | 0 | 374 | **$74,800** |
| **Base Model** | 62 | 21 | **$5,440** |
| **Best Model** | 94 | 8 | **$3,480** |

### Business Interpretation

Best Model menghasilkan total cost sebesar **$3,480**, lebih rendah dibandingkan Base Model sebesar **$5,440**. Artinya, penggunaan model terbaik mampu menurunkan estimasi cost sebesar **$1,960** dibandingkan Base Model.

Penurunan cost ini terutama disebabkan oleh berkurangnya jumlah **False Negative** dari **21 menjadi 8**. Dalam konteks churn prediction, hal ini penting karena False Negative berarti customer yang sebenarnya churn tetapi tidak terdeteksi oleh model, sehingga perusahaan kehilangan kesempatan untuk melakukan retention action.

Meskipun Best Model meningkatkan jumlah **False Positive** dari **62 menjadi 94**, trade-off ini masih dapat diterima karena biaya False Positive lebih rendah dibandingkan False Negative. Dengan kata lain, memberikan campaign kepada beberapa customer yang sebenarnya tidak churn masih lebih murah dibandingkan kehilangan customer yang benar-benar churn.

Oleh karena itu, Best Model lebih sesuai untuk mendukung strategi customer retention karena mampu menekan potensi kerugian bisnis dan membantu perusahaan memprioritaskan customer dengan risiko churn tinggi.

| Comparison | Cost Reduction | Cost Saving |
|-----------|----------------|-------------|
| **Best Model vs Base Model** | **$1,960** | **36.03%** |
| **Best Model vs All Predicted Churn** | **$17,220** | **83.19%** |
| **Best Model vs All Predicted Not Churn** | **$71,320** | **95.35%** |

---

## 💼 Business Recommendations

### 🎯 Strategi Retensi Prioritas

**1. Fokus pada Month-to-Month Customers**
- Tawarkan upgrade ke kontrak 1-2 tahun dengan benefit tambahan.
- Gunakan promo terbatas atau bundling untuk meningkatkan komitmen pelanggan.

**2. Migrasi ke Auto-Payment**
- Target pelanggan dengan metode pembayaran Electronic Check.
- Berikan cashback, loyalty point, atau potongan biaya untuk pindah ke auto-payment.

**3. Service Add-on sebagai Retention Tool**
- Tawarkan TechSupport dan OnlineSecurity kepada pelanggan berisiko tinggi.
- Gunakan free trial atau bundling untuk meningkatkan perceived value.

**4. Customer Satisfaction Program**
- Prioritaskan customer dengan satisfaction score rendah.
- Lakukan service recovery, follow-up keluhan, dan proactive customer support.

**5. Loyalty & Referral Program**
- Perkuat referral program karena customer dengan referral rendah cenderung memiliki engagement lebih lemah.
- Berikan reward untuk customer yang berhasil mengajak pengguna baru.

**6. Targeted Pricing**
- Fokus pada customer dengan monthly charges tinggi.
- Hindari diskon massal dan gunakan personalized offer berdasarkan risiko churn.

**7. Pendekatan Demografi dan Geografi**
- Buat support khusus untuk senior citizen dan customer tanpa partner/dependents.
- Audit kualitas layanan dan kompetitor pada area churn tinggi seperti San Diego dan Los Angeles.

---
## 🔎 SHAP Interpretation - Top 10 Important Features

Berdasarkan SHAP summary plot, fitur yang paling berpengaruh terhadap prediksi churn adalah:

| Rank | Feature |
|------|---------|
| 1 | Satisfaction Score |
| 2 | Online Security |
| 3 | Number of Referrals |
| 4 | Total Charges |
| 5 | Internet Service: Fiber Optic |
| 6 | Population |
| 7 | Average Monthly GB Download |
| 8 | Streaming TV |
| 9 | Contract: Two Year |
| 10 | Streaming Music |

### Business Insight

Hasil SHAP menunjukkan bahwa prediksi churn paling banyak dipengaruhi oleh **tingkat kepuasan pelanggan**, penggunaan **Online Security**, jumlah **referral**, serta karakteristik layanan seperti **Fiber Optic**, **Streaming TV**, dan **contract type**. Oleh karena itu, strategi retensi sebaiknya difokuskan pada peningkatan customer satisfaction, penawaran layanan tambahan, serta program loyalitas/referral untuk pelanggan berisiko tinggi.

---

## 📊 Model Implementation Workflow

1. **Scoring berkala** seluruh customer menggunakan model final.
2. **Gunakan threshold 0.30302092** untuk menentukan customer yang diprediksi churn.
3. **Segmentasi risiko:**
   - High Risk (>70%): personal call, service recovery, promo khusus.
   - Medium Risk (30.3%-70%): email campaign, loyalty offer, bundling layanan.
   - Low Risk (<30.3%): monitoring rutin dan standard engagement.
4. **Prioritaskan customer** dengan kombinasi month-to-month, Electronic Check, Fiber Optic tanpa TechSupport/OnlineSecurity, satisfaction score rendah, dan monthly charges tinggi.
5. **Lakukan A/B testing** untuk membandingkan efektivitas promo, bundling, personal call, dan loyalty program.
6. **Monitor ROI** dengan melihat churn rate setelah campaign, retention conversion, campaign cost, revenue saved, dan cost saving.
7. **Evaluasi model berkala** karena threshold dan performa model dapat berubah sesuai kondisi bisnis dan perilaku customer.

---

## 🛠️ Tech Stack

**Data Processing & Analysis:**
- Python 3.13
- pandas, numpy
- scipy, statsmodels

**Visualization:**
- matplotlib, seaborn
- folium (geospatial heatmap)
- Tableau Public

**Machine Learning:**
- scikit-learn
- XGBoost
- imbalanced-learn
- SHAP

**Deployment:**
- Streamlit
- pickle (model persistence)

---

## 📱 Live Demo & Resources

- **🌐 Interactive Prediction App:** StreamLit : https://telcocustomerchurnwildan.streamlit.app
- **📊 Interactive Dashboard:** Tableau : https://public.tableau.com/app/profile/muhamad.wildan.trisianly/viz/TelcoCustomerDashboard_17706500189310/Home?publish=yes
- **🎤 Project Presentation:** Canva : https://canva.link/l6yjq9bhzfy8ke0

---

## 📊 Dokumentasi Dashboard







---

## 📚 References

1. Investopedia. (2023). [Churn Rate Definition](https://www.investopedia.com/terms/c/churnrate.asp)
2. Statista. (2022). [Customer churn rate by industry](https://www.statista.com/statistics/816735/customer-churn-rate-by-industry-us/)
3. Harvard Business Review. (2014). [The Value of Keeping the Right Customers](https://hbr.org/2014/10/the-value-of-keeping-the-right-customers)
4. IBM. (2023). [Customer Churn Prediction Using Machine Learning](https://www.ibm.com/topics/customer-churn)

---



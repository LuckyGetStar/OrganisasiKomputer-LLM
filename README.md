# LEUKEMIA SUBTYPE CLASSIFICATION USING GENE EXPRESSION AND BioMedGPT-LM-7B

## 1. Deskripsi Proyek
Proyek ini merupakan implementasi Computational Biology yang bertujuan untuk mengklasifikasikan dua jenis leukemia akut, yaitu Acute Lymphoblastic Leukemia (ALL) dan Acute Myeloid Leukemia (AML), berdasarkan data ekspresi gen (Gene Expression).
Klasifikasi dilakukan dengan memanfaatkan Large Language Model (LLM), yaitu BioMedGPT-LM-7B, yang digunakan untuk menganalisis informasi ekspresi gen dan menghasilkan prediksi kelas leukemia.
Proyek ini menggunakan dataset Golub Gene Expression yang memiliki 72 sampel pasien dengan 7.129 fitur ekspresi gen. Data tersebut diproses terlebih dahulu melalui tahapan preprocessing, standardisasi, dan seleksi fitur sebelum diberikan kepada model LLM melalui teknik Prompt Engineering.
Hasil akhir berupa prediksi jenis leukemia, probabilitas klasifikasi, confidence, penjelasan model, serta visualisasi hasil eksperimen.

## 2. Latar Belakang dan Studi Kasus
Leukemia merupakan salah satu jenis kanker darah yang memiliki beberapa subtipe dengan karakteristik biologis yang berbeda. Pada proyek ini, fokus klasifikasi diarahkan pada dua jenis leukemia akut, yaitu ALL dan AML.
ALL (Acute Lymphoblastic Leukemia) merupakan leukemia yang berkaitan dengan perkembangan sel limfoid, sedangkan AML (Acute Myeloid Leukemia) berkaitan dengan perkembangan sel mieloid.
Kedua jenis leukemia tersebut membutuhkan pendekatan pengobatan yang berbeda sehingga proses identifikasi subtipe menjadi hal yang penting.
Melalui perkembangan teknologi DNA Microarray, tingkat ekspresi ribuan gen dapat diukur secara bersamaan. Informasi tersebut dapat dimanfaatkan untuk mengidentifikasi pola ekspresi gen yang membedakan pasien ALL dan AML.
Oleh karena itu, proyek ini mencoba menerapkan teknologi Large Language Model untuk melakukan klasifikasi leukemia berdasarkan profil ekspresi gen.

## 3. Tujuan Proyek
Tujuan dari proyek ini adalah:
1. Menerapkan teknologi LLM pada bidang Computational Biology.
2. Mengklasifikasikan pasien berdasarkan profil ekspresi gen menjadi ALL atau AML.
3. Melakukan preprocessing dan seleksi fitur terhadap data ekspresi gen.
4. Mengimplementasikan Prompt Engineering menggunakan pendekatan Few-Shot dan Zero-Shot.
5. Mengevaluasi hasil klasifikasi menggunakan metrik evaluasi machine learning.
6. Menampilkan hasil eksperimen melalui tabel, grafik, dan visualisasi.

## 4. Dataset yang Digunakan
Dataset yang digunakan adalah Golub Gene Expression Dataset yang diperoleh melalui Kaggle.
Sumber dataset:
https://www.kaggle.com/datasets/crawford/gene-expression

Dataset memiliki 72 sampel pasien dan 7.129 fitur ekspresi gen.
Pembagian dataset terdiri dari:
- Training Set: 38 sampel pasien.
- Independent Test Set: 34 sampel pasien.
- 
Dataset terdiri dari tiga file utama:
**a. data_set_ALL_AML_train.csv**
Berisi data ekspresi gen dari 38 sampel pasien yang digunakan untuk preprocessing, standardisasi, seleksi fitur, dan penyediaan contoh pada pendekatan Few-Shot.
**b. data_set_ALL_AML_independent.csv**
Berisi data ekspresi gen dari 34 sampel pasien yang digunakan untuk pengujian independen terhadap model.
**c. actual.csv**
Berisi label asli setiap pasien yang digunakan sebagai acuan untuk mencocokkan hasil prediksi model.
Label klasifikasi terdiri dari dua kelas, yaitu ALL dan AML.

## 5. Model LLM yang Digunakan
Model yang digunakan dalam proyek ini adalah BioMedGPT-LM-7B yang dikembangkan oleh PharMolix.
Sumber model:
https://huggingface.co/PharMolix/BioMedGPT-LM-7B

BioMedGPT-LM-7B merupakan model bahasa besar yang ditujukan untuk bidang biomedis. Model ini digunakan untuk menerima informasi ekspresi gen melalui prompt, kemudian menghasilkan prediksi klasifikasi dan penjelasan.
Model menggunakan pendekatan pretrained, sehingga proyek ini tidak melakukan pelatihan ulang atau fine-tuning terhadap bobot model.
Model dijalankan menggunakan Transformers dan PyTorch dengan dukungan GPU serta quantization 4-bit untuk mengurangi kebutuhan memori.

## 6. Lingkungan dan Teknologi
Proyek dikembangkan menggunakan Google Colab sebagai lingkungan eksekusi program berbasis Python.
Spesifikasi dan teknologi yang digunakan meliputi:
- Platform: Google Colab.
- Bahasa pemrograman: Python.
- GPU: NVIDIA Tesla T4.
- GPU Memory: 14,56 GB terdeteksi.
- Model: BioMedGPT-LM-7B.
- Framework: PyTorch.
- Model Library: Hugging Face Transformers.
- Quantization: 4-bit NF4.
- Data Processing: Pandas dan NumPy.
- Machine Learning: Scikit-learn.
- Visualisasi: Matplotlib dan Seaborn.
- Word Cloud: WordCloud.
- Model Optimization: BitsAndBytes dan Accelerate.

## 7. Tahapan Implementasi
Implementasi proyek dibagi menjadi beberapa bagian utama berdasarkan struktur notebook.
### Part 1 – Business Problem
Menentukan permasalahan yang akan diselesaikan, yaitu klasifikasi leukemia ALL dan AML berdasarkan profil ekspresi gen.
### Part 2 – Dataset Preparation
Menyiapkan dataset dari Kaggle. Pada implementasi Google Colab, dataset dimasukkan melalui proses upload file ZIP dan diekstrak secara manual.
### Part 3 – Library Installation
Menginstal library yang diperlukan untuk menjalankan proses pengolahan data, pemuatan model LLM, klasifikasi, dan visualisasi.
### Part 4 – GPU and Model Configuration
Mengatur lokasi dataset, nama model, perangkat komputasi, serta parameter eksperimen.
Konfigurasi utama yang digunakan adalah K_GENES = 10 untuk menentukan jumlah fitur gen yang dipilih dan N_SHOTS = 4 untuk jumlah contoh pada pendekatan Few-Shot.
Model menggunakan konfigurasi 4-bit NF4 agar kebutuhan memori lebih sesuai dengan GPU yang tersedia.
### Part 5 – Data Loading
Membaca ketiga file CSV menggunakan Pandas.
Dataset asli memiliki susunan gen sebagai baris dan pasien sebagai kolom. Oleh karena itu, dilakukan transpose agar setiap baris mewakili satu pasien dan setiap kolom mewakili fitur gen.
Selanjutnya, dilakukan pencocokan ID pasien dengan label asli dari actual.csv.
### Part 6 – Label Encoding
Mengubah label kategorikal menjadi representasi numerik menggunakan LabelEncoder.
Label ALL dan AML diubah menjadi nilai numerik agar dapat digunakan dalam proses preprocessing dan evaluasi.
### Part 7 – Data Preprocessing
Melakukan standardisasi menggunakan StandardScaler untuk menyamakan skala nilai ekspresi gen.
Kemudian dilakukan seleksi fitur menggunakan SelectKBest dengan metode ANOVA F-score.
Dari total 7.129 fitur gen, dipilih 10 fitur yang memiliki skor relevansi tertinggi terhadap perbedaan kelas ALL dan AML.
Proses fitting preprocessing dilakukan menggunakan data training, kemudian transformasi diterapkan pada data testing.
### Part 8 – Model Loading
Memuat tokenizer dan model BioMedGPT-LM-7B menggunakan Hugging Face Transformers.
Tokenizer berfungsi mengubah teks prompt menjadi token yang dapat diproses model, sedangkan model bertugas melakukan inferensi berdasarkan informasi yang diberikan.
Model dijalankan dalam mode evaluasi menggunakan model.eval().
### Part 9 – Prompt Engineering 1
Menerapkan pendekatan Few-Shot Learning dengan memberikan empat contoh pasien yang terdiri dari kelas ALL dan AML sebelum model melakukan klasifikasi terhadap pasien baru.
Pendekatan ini digunakan pada eksperimen terhadap independent test set.
### Part 10 – Prompt Engineering 2
Mengembangkan beberapa versi prompt, yaitu v3, v4, v5, dan v6.
Pengembangan dilakukan untuk membuat instruksi lebih ringkas, membatasi informasi yang diberikan, serta menyertakan fitur gen dengan nilai ekspresi relatif tinggi dan rendah.
Prompt v6 dirancang menggunakan pendekatan Zero-Shot dan membatasi penjelasan model agar mengacu pada fitur gen yang diberikan.
Pada bagian ini juga digunakan fungsi extract_classification_from_logits() untuk memperoleh prediksi dan probabilitas kelas dari logits model.
### Part 11 – Final Results
Menjalankan proses klasifikasi menggunakan pendekatan Zero-Shot dengan prompt v6 terhadap 38 sampel training.
Setiap pasien dianalisis secara independen. Hasil prediksi, label asli, probabilitas AML, confidence, dan penjelasan model kemudian disimpan ke dalam file CSV.
Selanjutnya, hasil tersebut digunakan untuk membuat visualisasi dan dashboard analisis.

## 8. Metode dan Teknik yang Digunakan
Beberapa metode utama yang diterapkan dalam proyek ini adalah:
**StandardScaler**
Digunakan untuk melakukan standardisasi nilai ekspresi gen berdasarkan rata-rata dan standar deviasi data training.
**SelectKBest**
Digunakan untuk memilih 10 fitur gen paling relevan berdasarkan ANOVA F-score.
**Few-Shot Learning**
Memberikan beberapa contoh berlabel kepada model sebelum melakukan klasifikasi terhadap pasien baru.
**Zero-Shot Learning**
Meminta model melakukan klasifikasi berdasarkan instruksi dan profil ekspresi gen tanpa memberikan contoh berlabel pada prompt pasien yang sedang diklasifikasikan.
**4-bit Quantization**
Mengurangi kebutuhan memori model dengan merepresentasikan bobot menggunakan konfigurasi 4-bit NF4.
**Logits Extraction**
Mengambil nilai logits model untuk menghitung probabilitas kelas ALL dan AML menggunakan fungsi softmax.

## 9. Output yang Dihasilkan
Program menghasilkan beberapa output utama sebagai berikut:
**a. Hasil Klasifikasi**
Berupa tabel yang berisi ID pasien, label asli, hasil prediksi, status ketepatan prediksi, probabilitas AML, confidence, dan penjelasan LLM.
**b. Probability and Confidence Visualization**
Menampilkan grafik probabilitas AML dan confidence setiap pasien.
**c. Word Cloud Visualization**
Menampilkan kata-kata yang sering muncul dalam penjelasan model, dengan pemisahan berdasarkan kelas ALL dan AML.
**d. Analytical Dashboard**
Menampilkan enam visualisasi, yaitu:
1. Probability Distribution.
2. Confidence Boxplot.
3. ROC Curve.
4. Probability vs Confidence Scatter Plot.
5. Explanation Length.
6. Summary Statistics.
**e. CSV Result**
Menyimpan hasil klasifikasi dalam format CSV agar dapat digunakan kembali untuk analisis dan dokumentasi.
## 10. Evaluasi Model
Evaluasi dilakukan untuk mengetahui kemampuan model dalam membedakan kelas ALL dan AML.
Metrik evaluasi yang digunakan meliputi:
**Accuracy**
Mengukur persentase prediksi yang benar dibandingkan seluruh data yang diuji.
**F1-Score**
Mengukur keseimbangan antara precision dan recall.
**AUC-ROC**
Mengukur kemampuan model dalam membedakan dua kelas berdasarkan probabilitas prediksi.
**Confusion Matrix**
Menampilkan jumlah prediksi benar dan salah pada masing-masing kelas.
Balanced Accuracy juga dapat digunakan untuk melihat rata-rata recall dari kedua kelas, terutama ketika jumlah sampel setiap kelas tidak seimbang
Evaluasi utama menggunakan independent test set yang terdiri dari 34 sampel pasien, sedangkan hasil pada training set digunakan sebagai analisis tambahan.
## 11. Struktur File Hasil Eksperimen
Hasil eksperimen disimpan dalam folder Google Drive bernama Hasil_Eksperimen_Leukemia.
File yang dihasilkan meliputi:
- resultado_llm_treino.csv: hasil klasifikasi 38 sampel training.
- barras_prob_conf.png: visualisasi probabilitas dan confidence.
- wordcloud_llm.png: visualisasi Word Cloud.
- dashboard_llm.png: dashboard analisis hasil eksperimen
Notebook utama disimpan dalam format IPYNB dan dapat dijalankan kembali melalui Google Colab.

## 12. Kesimpulan
Proyek ini menunjukkan penerapan Large Language Model dalam bidang Computational Biology, khususnya untuk klasifikasi subtipe leukemia berdasarkan profil ekspresi gen.
Melalui kombinasi preprocessing, seleksi fitur, quantization, dan Prompt Engineering, BioMedGPT-LM-7B digunakan untuk menghasilkan prediksi ALL dan AML beserta penjelasannya.
Eksperimen ini memberikan gambaran mengenai pemanfaatan LLM untuk menganalisis data biologis berdimensi tinggi. Namun, performa klasifikasi tetap perlu dievaluasi secara cermat menggunakan independent test set dan dibandingkan dengan metode machine learning konvensional.
Hasil proyek ini merupakan eksperimen komputasional untuk keperluan pembelajaran dan penelitian, bukan sistem diagnosis medis yang dapat digunakan secara langsung pada pasien.
---

## 13. Referensi dan Sumber
1. Golub Gene Expression Dataset. Kaggle. https://www.kaggle.com/datasets/crawford/gene-expression
2. PharMolix. BioMedGPT-LM-7B. Hugging Face. https://huggingface.co/PharMolix/BioMedGPT-LM-7B
3. PyTorch Documentation. https://pytorch.org/docs/
4. Hugging Face Transformers Documentation. https://huggingface.co/docs/transformers/
5. Scikit-learn Documentation. https://scikit-learn.org/stable/
